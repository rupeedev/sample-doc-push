# GitHub Document Sync - Feature Specification

## Purpose
Sync team documents with a linked GitHub repository, enabling backup, versioning, and collaboration through Git.

## Scope

### Included
- Fetch user repositories from GitHub API
- Link repository to team
- Configure sync folder path in repo
- Push documents to GitHub (manual trigger)
- Pull documents from GitHub (manual trigger)

### Excluded
- Automatic/scheduled sync
- Conflict resolution UI
- Branch selection (uses default branch)
- Binary file sync

## Components

### Backend (Rust)
- `crates/server/src/routes/github_sync.rs` - New sync routes
- `crates/db/src/models/github_connection.rs` - Add sync_path field

### Frontend (React)
- `frontend/src/pages/TeamGitHub.tsx` - Add repo selection, sync buttons
- `frontend/src/hooks/useGitHubConnection.ts` - Add sync methods

## API Endpoints

### GET /api/teams/:teamId/github/repos/available
Fetch repositories from GitHub that user can access

### POST /api/teams/:teamId/github/repos
Link a repository to the team (existing)

### PATCH /api/teams/:teamId/github/repos/:repoId
Update sync configuration (sync_path)

### POST /api/teams/:teamId/github/sync/push
Push documents from a folder to linked repo

### POST /api/teams/:teamId/github/sync/pull
Pull documents from linked repo to folder

## Database Changes

### github_repositories table
Add column: `sync_path TEXT` - Path in repo to sync documents (e.g., "docs/team")
Add column: `last_synced_at DATETIME` - Last sync timestamp

## UI Changes

### TeamGitHub Page
- Repository dropdown to select from available repos
- Sync path input field
- Push/Pull buttons per linked repository
- Sync status indicator
