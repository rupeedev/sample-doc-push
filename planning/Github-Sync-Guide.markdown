# GitHub Document Sync Guide

## Overview

The GitHub Sync feature allows you to synchronize documents between your Vibe Kanban team folders and GitHub repositories. This enables version control, backup, and collaboration through Git.

## How Sync Works

The Sync operation performs two actions in sequence:

1. **Pull** - Downloads any changes from GitHub to your local folder
2. **Push** - Uploads your local documents to GitHub

This ensures your local and remote copies stay in sync, similar to how `git pull && git push` works.

## Getting Started

### Step 1: Connect GitHub Account

1. Navigate to your team's **GitHub** page from the sidebar
2. Click **Connect with GitHub**
3. Authorize the application in the popup window
4. Your GitHub username will appear when connected

### Step 2: Link a Repository

1. Click **Link Repository**
2. Select a repository from your GitHub account
3. The repository will appear in the Linked Repositories table

### Step 3: Configure Sync

1. Click **Setup Sync** on your linked repository
2. Select a **Team Folder** - documents from this folder will be synced
3. Set the **GitHub Path** - the directory in the repo where documents will be stored (e.g., `docs`)
4. Click **Save Configuration**

### Step 4: Sync Documents

Once configured, you'll see these action buttons:

| Icon | Action | Description |
|------|--------|-------------|
| ↻ | Sync | Pull remote changes, then push local changes |
| ⚙ | Settings | Modify sync configuration |
| 🗑 | Unlink | Remove repository link |

Click the **Sync** button (↻) to synchronize your documents with GitHub.

## Sync Status Indicators

| Badge | Meaning |
|-------|---------|
| **Configured** (blue) | Sync is set up and ready |
| **Not configured** | Sync needs to be set up |

The **Last Synced** column shows when the most recent sync occurred.

## Document Storage

Documents are stored as Markdown files (`.md`) in your specified GitHub path:

```
repository/
└── docs/                    # Your configured sync path
    ├── document-1.md
    ├── document-2.md
    └── planning-notes.md
```

## Best Practices

1. **Sync regularly** - Keep your documents up to date by syncing frequently
2. **Use descriptive folder names** - Makes it easier to identify synced content
3. **Check sync results** - The success message shows how many files were pulled and pushed
4. **One folder per repo** - Each repository links to a single team folder

## Troubleshooting

### Sync fails with error
- Check your GitHub connection is still valid
- Verify you have write access to the repository
- Ensure the sync path doesn't conflict with existing files

### Documents not appearing
- Confirm the document is in the correct team folder
- Check that the document has been saved
- Try syncing again

### Changes not reflected on GitHub
- Wait a few seconds for GitHub to process the commit
- Refresh the GitHub page
- Check the repository's commit history

## Technical Details

- Documents are synced using the GitHub Contents API
- Each sync creates a commit in the repository
- File names are preserved from your Vibe Kanban documents
- Only Markdown content is synced (binary files excluded)
