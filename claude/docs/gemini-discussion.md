# Gemini Discussion: Teamwork API Authentication

## Question

> In Teamwork settings, I have an API token. Is this what I should include in my authentication headers when making calls to the API, as in my Bearer token?

## Answer

Based on the screenshot from Teamwork Projects, the answer is **no** — you generally do not use that API token as a "Bearer" token in the standard OAuth sense.

Instead, Teamwork typically uses **Basic Authentication**. Here is how you should handle that token in your headers:

---

## How to Use the Teamwork API Token

When making calls to the Teamwork API, you must pass the token through the `Authorization` header, but the format differs from a Bearer token.

### 1. Header Format

You use the Basic auth scheme. The standard requires a Base64-encoded string of `your_api_token:password`.

**The Trick:** Since the token itself acts as the credential, you use the token as the username and a dummy string (like `X` or `123`) as the password.

### 2. Implementation

Most modern HTTP clients (like Postman or Axios) will handle the encoding for you if you select "Basic Auth." If you are writing the raw header, it looks like this:

```
Authorization: Basic <Base64-encoded-string>
```

Example: If your token is `T12345`, you would encode the string `T12345:X` to Base64 and send that.

### Comparison at a Glance

| Auth Type | Header Syntax | Used for... |
|---|---|---|
| Bearer Token | `Authorization: Bearer <token>` | OAuth 2.0 / Personal Access Tokens (PATs) |
| Teamwork Token | `Authorization: Basic <encoded_token>` | Legacy/Direct API Access in Teamwork |

> **Security Note:** Once you reveal your token, treat it like a password. If you ever accidentally commit it to a public GitHub repo or share it, use "Turn OFF the API" or "Regenerate" to invalidate the old one.

---

## Code Examples

### Python (using `requests`)

The `requests` library has a built-in `auth` parameter that automatically formats the header as `Basic <Base64-encoded-string>`.

```python
import requests

# Your details from the Teamwork settings
api_token = "your_api_token_here"
password = "X"  # Teamwork accepts any string here, "X" is standard
domain = "yourcompany"  # The subdomain of your Teamwork URL

url = f"https://{domain}.teamwork.com/projects.json"

response = requests.get(
    url,
    auth=(api_token, password)  # This handles the Base64 encoding for you
)

print(response.json())
```

### JavaScript (using `fetch`)

In JavaScript, you manually encode the string using `btoa()` to create the header.

```javascript
const apiToken = "your_api_token_here";
const password = "X";
const domain = "yourcompany";

// Encode the credentials to Base64
const encodedCredentials = btoa(`${apiToken}:${password}`);

const url = `https://${domain}.teamwork.com/projects.json`;

fetch(url, {
    method: 'GET',
    headers: {
        'Authorization': `Basic ${encodedCredentials}`,
        'Content-Type': 'application/json'
    }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

### curl

The `-u` flag handles the colon and Base64 encoding automatically.

```bash
curl -u "{your-api-token}:X" \
     -H "Content-Type: application/json" \
     -X GET "https://{your-subdomain}.teamwork.com/projects.json"
```

**Command breakdown:**

- `-u "{your-api-token}:X"` — Basic auth flag; `X` is the dummy password required by Teamwork's API
- `-H "Content-Type: application/json"` — tells the server you expect a JSON response
- `-X GET` — specifies the HTTP method (GET is the default, but explicit is good practice)
- The `.json` suffix on Teamwork endpoints tells the API which format to return

**Pretty-print output with `jq`:**

```bash
curl -u "T12345:X" "https://mycompany.teamwork.com/projects.json" | jq
```

> **Gotcha:** If your API token contains special characters, wrap the entire `token:X` string in double quotes to prevent your terminal from misinterpreting them.

---

## Testing in Postman

Postman handles the Base64 encoding automatically under "Basic Auth."

1. **Open a New Request** — create a new GET tab
2. **Enter Your URL** — `https://{your-company}.teamwork.com/projects.json`
3. **Go to the Auth Tab** — click the Authorization tab under the URL bar
4. **Select Type** — choose **Basic Auth** from the dropdown
5. **Enter Credentials:**
   - Username: your API token
   - Password: `X`
6. **Send** — hit the blue Send button

To see what Postman generated, click the **Headers** tab after selecting Basic Auth. You will see:

| Key | Value |
|---|---|
| Authorization | `Basic <YourEncodedString>` |

### Troubleshooting

| Error | Likely Cause |
|---|---|
| `401 Unauthorized` | API token is incorrect, or the Password field was left empty |
| `404 Not Found` | Wrong subdomain — must match what you see in your browser when logged in |
| SSL Errors | Make sure you are using `https://` not `http://` |

---

## URL Format

Always use your specific Teamwork site address:

```
https://{your-company-name}.teamwork.com/
```

Using the generic `www.teamwork.com` will fail to authenticate because the API won't know which account's data to return.

---

## Follow-Up: MCP Authentication Issue

> I'm having trouble authenticating to the MCP server. API authentication seems pretty easy. Here is my code: [tasks-by-date branch](https://github.com/TheAPIGuysDev/teamwork-mcp/tree/tasks-by-date)

### Gemini's Response

Authenticating a Model Context Protocol (MCP) server for Teamwork can be tricky because you're balancing two different "handshakes":

1. **AI Client → MCP Server** (e.g., Claude Desktop or Cursor connecting to your server process)
2. **MCP Server → Teamwork API** (your server calling Teamwork on behalf of the AI)

Based on the code structure typical for `teamwork-mcp`, the issue usually lies in how environment variables are passed to the server process.

---

### 1. The "Bearer" vs "Basic" Confusion

As discussed earlier, Teamwork's API uses Basic Auth (`Token + "X"`), but many MCP implementations allow you to provide a Personal Access Token or Bearer Token if they've implemented a wrapper.

Since you are running this as a local STDIO server, authentication isn't handled in request headers in your code — it's handled by the **environment variables you provide when the server starts**.

---

### 2. How to Fix Your MCP Configuration

If you are using Claude Desktop or Cursor, update your `claude_desktop_config.json`. The server doesn't "see" your token unless it is explicitly passed into the process environment via the `env` block:

```json
{
  "mcpServers": {
    "teamwork": {
      "command": "node",
      "args": ["/path/to/your/teamwork-mcp/build/index.js"],
      "env": {
        "TEAMWORK_API_TOKEN": "your_actual_token_here",
        "TEAMWORK_DOMAIN": "yourcompany"
      }
    }
  }
}
```

---

### 3. Common Code Pitfalls in `tasks-by-date`

**Check the variable name:** Does your code look for `process.env.TEAMWORK_API_TOKEN` or `process.env.API_TOKEN`? They must match exactly.

**The "X" Password:** If your MCP server builds the fetch request manually, ensure it's doing the Base64 encoding:

```javascript
// Inside your MCP server tool logic
const auth = btoa(`${process.env.TEAMWORK_API_TOKEN}:X`);
```

---

### 4. Debugging a "401 Unauthorized"

**Restart the client:** Claude and Cursor only read the config file on startup. If you changed the token, you must fully quit and restart the app.

**Check the logs:** MCP servers log errors to a local file.

| Platform | Log Location |
|---|---|
| macOS | `~/Library/Logs/Claude/mcp.log` |
| Windows | `%APPDATA%\Claude\logs\mcp.log` |