# GitHub OAuth Specification

## Purpose
Replace manual PAT entry with GitHub OAuth for secure, user-friendly authentication.

## Scope

**Included:**
- GitHub OAuth authorization flow
- Token exchange and storage (encrypted)
- Fetch GitHub username on connect
- List user repositories from GitHub API
- Link/unlink repositories to team

**Excluded:**
- GitHub App installation (uses OAuth App)
- Webhook integration
- GitHub Actions integration

## Components

**Backend (Rust):**
- `crates/server/src/routes/oauth.rs` - OAuth routes (authorize, callback)
- `crates/db/src/models/github_connection.rs` - Update to store oauth_token
- `crates/db/migrations/` - Migration to add encryption support

**Frontend (React):**
- `frontend/src/pages/TeamGitHub.tsx` - Update connect flow
- `frontend/src/hooks/useGitHubConnection.ts` - Add OAuth methods

**Environment:**
- `GITHUB_CLIENT_ID` - OAuth App client ID
- `GITHUB_CLIENT_SECRET` - OAuth App client secret
- `GITHUB_REDIRECT_URI` - Callback URL

## API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/oauth/github/authorize` | Returns GitHub OAuth URL |
| GET | `/api/oauth/github/callback` | Handles OAuth callback, exchanges code for token |
| GET | `/api/teams/{id}/github/available-repos` | Lists repos from GitHub API |

## Database Changes

**Update `github_connections` table:**
- `oauth_token` - Store OAuth access token (encrypted)
- `token_type` - "pat" or "oauth"
- Remove plain `access_token` field (migrate to encrypted)

## UI Changes

**TeamGitHub page:**
- Replace PAT input with "Connect with GitHub" button
- Add "Fetch Repositories" button to load repos from GitHub
- Show repository selector to link repos
- Keep disconnect functionality
