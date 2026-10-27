# N8N API Authentication Workflow

## Overview
This workflow demonstrates three API authentication mechanisms in n8n: HTTP Basic Authentication, header-based Bearer Token Authentication, and GitHub OAuth 2.0. The workflow was tested using a manual trigger and HTTP Request nodes.

## Workflow sequence
`Manual Trigger` -> `HTTP_BasicAuth` -> `HTTP_BearerAuth` -> `HTTP_OAuth2`

## Node descriptions

### 1. Manual Trigger
Starts the workflow when **Execute workflow** is clicked in the n8n editor.

### 2. HTTP_BasicAuth
- Method: `GET`
- Endpoint: `https://postman-echo.com/basic-auth`
- Authentication: Generic Credential Type -> Basic Auth
- Credential: `trainee_user` (stored in n8n credentials)
- Verified output: `authenticated: true`

### 3. HTTP_BearerAuth
- Method: `GET`
- Endpoint: `https://postman-echo.com/headers`
- Authentication: Generic Credential Type -> Header Auth
- Credential: `trainee_bearer_token` (stored in n8n credentials)
- Verified output: the API echoed the configured `Authorization: Bearer ...` header.

### 4. HTTP_OAuth2
- Method: `GET`
- Endpoint: `https://api.github.com/user`
- Authentication: Predefined Credential Type -> GitHub OAuth2 API
- Credential: `GitHub account 3` (authorized using GitHub OAuth)
- Verified output: GitHub user profile returned, including `login`, `id`, and profile URL.

## How to run
1. Import the exported n8n workflow JSON into n8n, or open the existing workflow.
2. Configure your own credentials for all three HTTP Request nodes; exported workflow JSON does not include the credential secrets.
3. For GitHub OAuth, register an OAuth application with the exact n8n callback URL displayed by the credential editor and authorize it.
4. Click **Execute workflow**.
5. Confirm green checkmarks on the trigger and all three HTTP Request nodes.
6. Inspect the node outputs for the expected authentication responses.

## Verification summary
| Test | Expected | Observed | Result |
| --- | --- | --- | --- |
| Basic authentication | Authenticated response | `authenticated: true` | PASS |
| Bearer header authentication | Authorization header echoed | Bearer authorization header returned | PASS |
| GitHub OAuth 2.0 | Authorized user profile | GitHub profile JSON returned | PASS |
| End-to-end workflow | All nodes complete | Four green checkmarks, one item per connection | PASS |

## Security notes
- Store usernames, passwords, tokens, client IDs and client secrets in n8n credentials, not inside workflow node code or exported JSON.
- Screenshots of the Bearer echo endpoint can expose the test token. The supplied evidence PDF masks the token value.
- Do not share GitHub OAuth client secrets or access tokens.
- This workflow demonstrates authentication methods, not a production authorization or token-lifecycle audit.

## Submission files
- Exported n8n workflow JSON (export separately from n8n).
- `N8N_API_Authentication_Evidence.pdf` (screenshots and concise evidence descriptions).
- This `README.md`.
