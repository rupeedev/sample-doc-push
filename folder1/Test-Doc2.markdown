# Local Scan Feature

The **Local Scan** feature allows you to synchronize documents from your local filesystem into Vibe Kanban's document management system.

## How It Works

1. **Configure Storage Path**: Set the `document_storage_path` in Team Settings to point to your local documents directory (e.g., `/Users/username/Documents/docs-testing`)

2. **Create Folders**: When you create a folder in the app, a corresponding directory is automatically created at `{storage_path}/{folder_name}/`

3. **Add Files**: Place your documents in the folder directory on your filesystem

4. **Scan**: Click the "Local Scan" button to register all supported files in the database

## Supported File Types

| Category | Extensions | Content Stored |
|----------|------------|----------------|
| Markdown | `.md`, `.markdown` | Yes |
| Text | `.txt`, `.csv`, `.json`, `.xml`, `.html` | Yes |
| Documents | `.pdf`, `.doc`, `.docx`, `.xls`, `.xlsx`, `.ppt`, `.pptx` | No (metadata only) |
| Images | `.png`, `.jpg`, `.jpeg`, `.gif`, `.svg`, `.webp` | No (metadata only) |

## Metadata Captured

For all scanned files, the following metadata is stored:

- **file_path**: Full path to the file on disk
- **file_size**: Size in bytes
- **mime_type**: MIME type (e.g., `application/pdf`, `image/png`)
- **file_type**: File extension

## Best Practices

- Use kebab-case or snake_case for filenames (e.g., `my-document.md` or `my_document.md`)
- The filename becomes the document title (converted to Title Case)
- Re-scanning updates existing documents if the file path or title matches
- Text files have their content indexed for search; binary files store only metadata
