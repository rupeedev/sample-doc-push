# GitHub OAuth Flow

## User Authentication Flow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           GitHub OAuth Flow                                  │
└─────────────────────────────────────────────────────────────────────────────┘

┌──────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  User    │     │   Frontend   │     │   Backend    │     │   GitHub     │
└────┬─────┘     └──────┬───────┘     └──────┬───────┘     └──────┬───────┘
     │                  │                    │                    │
     │ 1. Click         │                    │                    │
     │ "Connect GitHub" │                    │                    │
     │─────────────────>│                    │                    │
     │                  │                    │                    │
     │                  │ 2. GET /api/oauth/ │                    │
     │                  │ github/authorize   │                    │
     │                  │───────────────────>│                    │
     │                  │                    │                    │
     │                  │                    │ 3. Build OAuth URL │
     │                  │                    │ with client_id,    │
     │                  │                    │ redirect_uri,      │
     │                  │                    │ scope, state       │
     │                  │                    │                    │
     │                  │ 4. Return auth URL │                    │
     │                  │<───────────────────│                    │
     │                  │                    │                    │
     │ 5. Redirect to   │                    │                    │
     │ GitHub Login     │                    │                    │
     │<─────────────────│                    │                    │
     │                  │                    │                    │
     │ 6. Login & Authorize                  │                    │
     │──────────────────────────────────────────────────────────>│
     │                  │                    │                    │
     │ 7. Redirect with code                 │                    │
     │<──────────────────────────────────────────────────────────│
     │                  │                    │                    │
     │ 8. Callback URL  │                    │                    │
     │ with auth code   │                    │                    │
     │─────────────────>│                    │                    │
     │                  │                    │                    │
     │                  │ 9. POST /api/oauth/│                    │
     │                  │ github/callback    │                    │
     │                  │ {code, state}      │                    │
     │                  │───────────────────>│                    │
     │                  │                    │                    │
     │                  │                    │ 10. Exchange code  │
     │                  │                    │ for access_token   │
     │                  │                    │───────────────────>│
     │                  │                    │                    │
     │                  │                    │ 11. Return token   │
     │                  │                    │<───────────────────│
     │                  │                    │                    │
     │                  │                    │ 12. Store token    │
     │                  │                    │ in DB (encrypted)  │
     │                  │                    │ ┌────────────┐     │
     │                  │                    │ │github_     │     │
     │                  │                    │ │connections │     │
     │                  │                    │ └────────────┘     │
     │                  │                    │                    │
     │                  │                    │ 13. Fetch user info│
     │                  │                    │───────────────────>│
     │                  │                    │                    │
     │                  │                    │ 14. Return username│
     │                  │                    │<───────────────────│
     │                  │                    │                    │
     │                  │ 15. Success +      │                    │
     │                  │ connection data    │                    │
     │                  │<───────────────────│                    │
     │                  │                    │                    │
     │ 16. Show         │                    │                    │
     │ Connected Status │                    │                    │
     │<─────────────────│                    │                    │
     │                  │                    │                    │
```

## Repository Fetch Flow

```
┌──────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  User    │     │   Frontend   │     │   Backend    │     │   GitHub     │
└────┬─────┘     └──────┬───────┘     └──────┬───────┘     └──────┬───────┘
     │                  │                    │                    │
     │ 1. View repos    │                    │                    │
     │─────────────────>│                    │                    │
     │                  │                    │                    │
     │                  │ 2. GET /api/teams/ │                    │
     │                  │ {id}/github/repos  │                    │
     │                  │───────────────────>│                    │
     │                  │                    │                    │
     │                  │                    │ 3. Get stored token│
     │                  │                    │ from DB            │
     │                  │                    │                    │
     │                  │                    │ 4. GET /user/repos │
     │                  │                    │ Authorization:     │
     │                  │                    │ Bearer {token}     │
     │                  │                    │───────────────────>│
     │                  │                    │                    │
     │                  │                    │ 5. Return repos    │
     │                  │                    │<───────────────────│
     │                  │                    │                    │
     │                  │ 6. Return repo list│                    │
     │                  │<───────────────────│                    │
     │                  │                    │                    │
     │ 7. Display repos │                    │                    │
     │<─────────────────│                    │                    │
```
