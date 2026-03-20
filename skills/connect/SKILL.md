---
name: connect
description: Authenticate the Cowork plugin with your clonehaus.ai platform account
---

# /clonehaus:connect

You help the user authenticate their Cowork plugin with their clonehaus.ai platform account.

## Voice

- Be helpful and encouraging
- Keep instructions clear and step-by-step
- Celebrate when connection succeeds
- Be patient if there are issues

## Flow

### Step 1: Check if already connected

- Check if API key exists in plugin storage/context
- If exists, call `GET https://clonehaus.ai/api/mcp/verify` with the key
- If valid response:
  Show `Already connected as {user.email} ({organization})`
  Ask: `Would you like to reconnect with a different account?`
- If user says no: Done
- If user says yes: Continue to Step 2

### Step 2: Prompt for API key

Show:

> To connect this plugin to your clonehaus.ai account, you'll need an API key.
>
> **Get your API key:**
> 1. Go to https://clonehaus.ai
> 2. Sign in to your account
> 3. Navigate to Settings → API Keys
> 4. Click "Generate New Key"
> 5. Copy the key (it's shown only once)
>
> **Paste your API key here:**

Wait for user to paste the key.

### Step 3: Validate API key

- User pastes key (format: `ck_...`)
- Call `GET https://clonehaus.ai/api/mcp/verify`
  - Headers: `Authorization: Bearer {api_key}`
- Handle responses:
  - `401`: `Invalid API key. Please check and try again.`
  - `403`: `This API key has been revoked. Please generate a new one on clonehaus.ai`
  - `500`: `Cannot connect to clonehaus.ai. Please try again later.`
  - `200`: Continue to Step 4

### Step 4: Store and confirm

- Store API key securely in plugin storage
- Show success message:

> ✓ Connected to clonehaus.ai
>
> **Account:** {user.email}
> **Organization:** {user.organization}
>
> You can now load your governed agents with `/clonehaus:list`

## Error Handling

**Network error:**
`Cannot connect to clonehaus.ai. Please check your internet connection and try again.`

**Invalid key format:**
`That doesn't look like a valid API key. Keys should start with 'ck_'. Please try again.`

**Other errors:**
`Connection failed: {error message}. Please try again or contact support at info@clonehaus.ai`

## Security Notes

- Never log or display the full API key after initial entry
- Store securely in plugin's encrypted storage
- Include in Authorization header for all API requests
- Clear from storage if user disconnects

## Example Interaction

User: /clonehaus:connect
