# How to Give Claude Access to Private GitHub Repos

There are three methods, from simplest to most capable.

---

## Method 1: Personal Access Token (Simplest, Use This First)

Create a fine-grained token that only has read access to the repos you choose.

### Step 1: Create the Token

1. Go to: https://github.com/settings/tokens?type=beta
   (Settings -> Developer Settings -> Personal Access Tokens -> Fine-grained tokens)

2. Click "Generate new token"

3. Configure it:
   - Token name: `claude-readonly` (or whatever you want)
   - Expiration: 30 days (or shorter -- you can always make a new one)
   - Repository access: "Only select repositories" -- pick the ones you want
   - Permissions:
     - Contents: Read-only
     - Metadata: Read-only
     - That's it. Nothing else needed.

4. Click "Generate token"

5. COPY THE TOKEN IMMEDIATELY. You won't see it again.

### Step 2: Give It to Claude

In any conversation where you want me to access private repos, paste the token
and say something like:

    "Here's my GitHub PAT: ghp_xxxxxxxxxxxx
     Use it to read my private repos."

I'll use it like this in API calls:

```bash
curl -s -H "Authorization: token ghp_xxxxxxxxxxxx" \
  "https://api.github.com/repos/MRJR0101/PRIVATE_REPO/contents/"
```

### Security Notes

- Fine-grained tokens with "Only select repositories" limit blast radius
- Read-only Contents + Metadata is the minimum needed
- Set short expiration (7-30 days) and rotate
- The token appears in the conversation history -- if that bothers you, revoke
  it after the session and create a new one next time
- NEVER commit tokens to repos or put them in handoff documents
- Claude does not persist tokens between conversations

### Rate Limits

Authenticated requests get 5,000/hour (vs 60/hour unauthenticated). More than
enough for auditing even large accounts.

---

## Method 2: Claude Desktop + GitHub CLI (Best for Local Work)

If you're using Claude Desktop with Desktop Commander, you can authenticate
through the GitHub CLI on your machine. Claude never sees the token directly.

### Step 1: Install and Auth GitHub CLI

```powershell
# Install gh (if not already installed)
winget install GitHub.cli

# Authenticate (opens browser)
gh auth login
```

### Step 2: Claude Uses gh Commands

In Claude Desktop conversations, I can use Desktop Commander to run:

```powershell
# List your repos (including private)
gh repo list MRJR0101 --limit 50

# Clone a private repo for inspection
gh repo clone MRJR0101/PrivateRepo C:\Dev\PROJECTS\PrivateRepo

# View repo contents without cloning
gh api repos/MRJR0101/PrivateRepo/contents/

# Get a specific file
gh api repos/MRJR0101/PrivateRepo/contents/README.md | 
  python -c "import json,sys,base64; d=json.load(sys.stdin); print(base64.b64decode(d['content']).decode('utf-8'))"

# View recent commits
gh api repos/MRJR0101/PrivateRepo/commits --jq '.[].commit.message'
```

### Security Notes

- The token lives in gh's credential store, not in the conversation
- Claude Desktop sees the command output, not the token itself
- This is the most secure method for ongoing use
- Works with all repo operations including clone, push (if you allow it)

---

## Method 3: GitHub MCP Server (Most Integrated, Experimental)

There are MCP (Model Context Protocol) servers for GitHub that let Claude
interact with repos through a structured tool interface rather than raw API
calls.

### Option A: Official GitHub MCP (if available in your Claude setup)

Check your Claude.ai connector settings for a GitHub integration. If available,
connect it and Claude gets structured tools like:

- list_repos
- get_file_contents
- search_code
- create_issue
- etc.

### Option B: Self-Hosted GitHub MCP Server

For Claude Desktop, you can run a local MCP server:

```powershell
# Install the GitHub MCP server
npm install -g @modelcontextprotocol/server-github

# Add to Claude Desktop config (claude_desktop_config.json)
```

Add this to your Claude Desktop MCP configuration:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_xxxxxxxxxxxx"
      }
    }
  }
}
```

This gives Claude structured GitHub tools without needing to pass tokens in
conversation.

### Security Notes

- MCP server approach keeps the token in a config file, not in chat
- Can be more restrictive about what operations are allowed
- Still experimental -- check current MCP docs for latest setup

---

## Which Method Should You Use?

| Scenario | Best Method |
|----------|-------------|
| Quick one-off audit in Claude.ai | Method 1 (PAT in chat) |
| Ongoing Claude Desktop work | Method 2 (gh CLI) |
| Heavy GitHub integration | Method 3 (MCP server) |
| Maximum security | Method 2 (token never in chat) |

---

## What I Can Do With Access

Once authenticated, I can:

- Read all file contents from private repos
- Get full recursive file trees
- Read commit history and diffs
- Check CI/CD status and workflow runs
- Read issues and pull requests
- Audit repo settings (branch protection, etc.)
- Compare branches
- Read release notes

What I CANNOT do (with read-only permissions):

- Push code
- Create/delete branches
- Modify repo settings
- Delete anything
- Access secrets or environment variables stored in GitHub

---

## Quick Test

After creating a token, test it works:

```powershell
# Replace with your token
$token = "ghp_xxxxxxxxxxxx"

# Test: list your repos including private ones
curl -s -H "Authorization: token $token" `
  "https://api.github.com/user/repos?per_page=10&type=all" |
  python -c "import json,sys; [print(f'{r[\"name\"]:30s} private={r[\"private\"]}') for r in json.load(sys.stdin)]"
```

If you see your private repos listed, it's working.
