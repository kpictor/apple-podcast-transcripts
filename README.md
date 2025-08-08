# <img src="/favicons/favicon-96x96.png?raw=true" height="32px" alt=""/> Apple Podcast Transcript Viewer

This is a simple UI tool for viewing and exporting Apple Podcast transcripts. No software installation is needed; it runs entirely in your web browser. It should work on any Mac with the Podcasts app.

**Live version: [https://alexbeals.com/projects/podcasts/](https://alexbeals.com/projects/podcasts/)**

![Screenshot of the Apple Podcast Transcript Viewer](/images/og.png)

## How It Works

The Apple Podcasts app on macOS stores transcript data locally on your machine when you view a transcript in the app. This tool takes advantage of that local cache.

1.  **Open the Podcasts App:** In the macOS Podcasts app, go to the episode you want and view its transcript. This will ensure the data is cached locally.
2.  **Locate the Data Folder:** Open Finder, press `Cmd+Shift+G`, and paste the following path:
    ```
    ~/Library/Group Containers/243LU875E5.groups.com.apple.podcasts
    ```
3.  **Drag and Drop:** Drag the entire contents of that folder onto the Apple Podcast Transcript Viewer website.

All processing happens locally in your browser; no files are ever uploaded to a server.

## Features

*   **View Transcripts:** See the full transcript for any podcast episode.
*   **Copy and Paste:** Easily copy parts of the transcript.
*   **Export:**
    *   Export multiple transcripts as a single Markdown file.
    *   Export multiple transcripts as a zip file containing individual Markdown files.
*   **Search by Name:** The tool now supports directly searching for podcasts by name within the Docker application.

## Local Development

To run this tool locally for development, you'll need to set up a simple web server.

```bash
python3 -m http.server
```

Then, open your browser to `http://localhost:8000`.

## Docker Usage

You can also run this application in a Docker container.

```bash
# Build the Docker image
docker build -t apple-podcast-transcripts .

# Run the Docker container
docker run -p 8000:8000 apple-podcast-transcripts
```

Then, open your browser to `http://localhost:8000`.

## Technical Details

The tool uses `sql.js` to read the podcast metadata from the local SQLite database. A clever hack (see the source code) was required to get `sql.js` to work with the Write-Ahead Logging (WAL) file that the Podcasts app uses.

