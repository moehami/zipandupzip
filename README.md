# File Archiver GitHub Action

A versatile GitHub Action to either **compress** files/directories into a `.zip` archive or **uncompress** a `.zip` archive.

## Features

* **Zip Operation:** Compress a specified file or directory into a `.zip` archive.
* **Unzip Operation:** Extract contents from a `.zip` archive to a target directory.
* **Optional Overwriting:** Control whether unzipping overwrites existing files.
* **Optional Commit:** Automatically commit the resulting archive or extracted files back to the repository.

## Usage

### 1. Compression (Zipping) Example

This workflow compresses the `build/` directory into `release.zip` and commits it.

```yaml
name: Create Release Zip

on:
  workflow_dispatch:
    inputs:
      build_path:
        description: 'Path to the directory to zip'
        required: true
        default: 'dist' # Example default

jobs:
  zip_project:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Build project (replace with your build steps)
        run: |
          mkdir -p dist
          echo "My project content" > dist/index.html
          echo "console.log('App started');" > dist/app.js

      - name: Create project zip archive
        uses: your-username/file-archiver-action@v1 # Replace with your repo name and version
        with:
          operation: 'zip'
          archive_path: 'project-release.zip'
          source_path: 'dist'
          commit_changes: 'true'
          commit_message: 'Action: Created project-release.zip'

      - name: Check output
        run: ls -lh
