# GitHub Document Sync Flow

## User Flow
```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   GitHub    │     │   TeamGitHub │     │  Documents  │
│   Page      │────>│   Link Repo  │────>│   Folder    │
└─────────────┘     └──────────────┘     └─────────────┘
                           │
                           v
                    ┌──────────────┐
                    │ Select Repo  │
                    │ from List    │
                    └──────────────┘
                           │
                           v
                    ┌──────────────┐
                    │ Configure    │
                    │ Sync Path    │
                    └──────────────┘
```

## Sync Operations
```
┌─────────────────────────────────────────────────────────┐
│                    PUSH TO GITHUB                        │
├─────────────────────────────────────────────────────────┤
│  Documents DB  ──>  Convert to MD  ──>  Git Commit/Push │
│                                                          │
│  1. Read documents from folder                          │
│  2. Convert content to markdown files                   │
│  3. Create/update files in repo path                    │
│  4. Commit and push changes                             │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                    PULL FROM GITHUB                      │
├─────────────────────────────────────────────────────────┤
│  Git Clone/Pull  ──>  Parse MD  ──>  Update Documents   │
│                                                          │
│  1. Fetch files from repo path                          │
│  2. Parse markdown content                              │
│  3. Create/update documents in DB                       │
│  4. Handle conflicts (last-modified wins)               │
└─────────────────────────────────────────────────────────┘
```

## Data Flow
```
┌──────────┐    ┌───────────────┐    ┌──────────────┐
│ Frontend │───>│ Backend API   │───>│ GitHub API   │
│          │    │               │    │              │
│ TeamGitHub    │ POST /sync    │    │ Contents API │
│ Page     │<───│ push/pull     │<───│ Commits API  │
└──────────┘    └───────────────┘    └──────────────┘
                       │
                       v
                ┌───────────────┐
                │  Documents DB │
                │  (SQLite)     │
                └───────────────┘
```
