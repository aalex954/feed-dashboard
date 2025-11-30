# Feed Dashboard

A modern, responsive web-based dashboard for monitoring live camera and video feeds. Ships with demo feeds to get started quickly, and is easily customizable for traffic cameras, security feeds, or any streaming sources.

![Dashboard Preview](https://img.shields.io/badge/Status-Live-brightgreen) ![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)

![feed-dashboard](https://github.com/user-attachments/assets/b95e66d3-3338-4126-bd6a-cb28455ba95b)


## Features

### Multiple Feed Types
- **Snapshot Images** - Auto-refreshing JPEG/PNG camera images with configurable refresh intervals
- **HLS Streams** - Live video streams using HLS (.m3u8) format with full playback controls
- **Iframe Embeds** - Embed full web pages or other streaming sources

### Flexible Layout
- **1 to 5 column grid layouts** - Choose the best layout for your screen size
- **Collapsible sidebar** - Hide the control panel for a fullscreen viewing experience
- **Responsive design** - Works on desktop, tablet, and mobile devices
- **Maximized view** - Click any feed to view it in a fullscreen overlay

### Persistent Configuration
- All settings saved to browser localStorage
- Camera feeds, layout preferences, and sidebar state are remembered
- No server or account required

### Config File Import/Export
- **Import** camera configurations from JSON files
- **Export** your current setup to share or backup
- **Merge** imports to add cameras without replacing existing ones
- Secure validation prevents malicious configs

### 🔗 URL Parameter Support
Control the dashboard via URL parameters for bookmarking or sharing specific views:

| Parameter | Aliases | Values | Description |
|-----------|---------|--------|-------------|
| `columns` | `cols`, `layout` | `1` - `5` | Set the number of grid columns |
| `sidebar` | `panel` | `show`, `hide`, `true`, `false`, `1`, `0` | Show or hide the sidebar |

**Examples:**
```
Dashboard.html?columns=4
Dashboard.html?cols=5&sidebar=hide
Dashboard.html?layout=2&panel=visible
```

## Usage

### Quick Start
1. Open `Dashboard.html` in any modern web browser
2. The dashboard loads with demo feeds (HLS streams, auto-refreshing images, and iframe examples)
3. Use the sidebar to add, remove, or toggle camera visibility
4. Click any feed to view it maximized

### Adding a Camera Feed

1. In the **Add / Edit feeds** section, enter:
   - **Camera name** - A friendly name for the feed
   - **Feed URL** - The URL to the camera image, HLS stream, or webpage
   - **Type** - Choose between:
     - *Snapshot image* - For static images that refresh periodically
     - *Full page / stream (iframe)* - For embedding webpages
     - *HLS (.m3u8 stream)* - For live video streams
   - **Refresh (s)** - Refresh interval in seconds (for snapshot images only)
2. Click **Add camera to dashboard**

### Managing Feeds

- **Show/Hide** - Use the checkbox next to each feed to toggle visibility
- **Remove** - Click the "Remove" button to delete a feed
- **Reset** - Click "Reset to sample feeds" to restore default cameras

### Changing Layout

- Use the **Layout** dropdown in the header to select 1-5 columns
- Click **Hide Panel** / **Show Panel** to toggle the sidebar

### Importing/Exporting Configuration

#### Export Config
1. Click **Export Config** in the Import/Export section
2. A JSON file will be downloaded with your current camera setup

#### Import Config (Replace)
1. Click **Choose config file to import...**
2. Select a valid JSON config file
3. All existing cameras will be replaced with the imported ones

#### Merge Import
1. Click **Merge Import**
2. Select a JSON config file
3. New cameras are added; duplicates (by URL) are skipped

#### Config File Format
```json
{
  "name": "My Camera Setup",
  "subtitle": "Optional dashboard subtitle",
  "version": "1.0",
  "columns": 3,
  "cameras": [
    {
      "id": "camera-1",
      "name": "Front Door Camera",
      "url": "https://example.com/camera1.jpg",
      "type": "image",
      "refreshMs": 10000,
      "visible": true,
      "notes": "Optional description"
    },
    {
      "id": "camera-2",
      "name": "Live Stream",
      "url": "https://example.com/stream.m3u8",
      "type": "hls",
      "refreshMs": 0,
      "visible": true,
      "notes": ""
    }
  ]
}
```

#### Security Features
- **File size limit**: Max 1MB
- **URL validation**: Only http/https protocols allowed
- **Type validation**: Only `image`, `iframe`, `hls` types accepted
- **Input sanitization**: HTML tags stripped, lengths limited
- **Camera limit**: Maximum 100 cameras per config

## Camera Feed Sources

### Default Demo Feeds

The dashboard ships with demo feeds to help you get started:
- **HLS Streams** - Big Buck Bunny and Apple's bipbop test streams
- **Auto-refreshing Images** - Picsum random images (refreshes every 10 seconds)
- **Iframe Embed** - Wikipedia page demonstrating iframe capability

### Adding Your Own Cameras

The dashboard works with any publicly accessible camera feed:
- Direct image URLs (JPEG, PNG, GIF)
- HLS video streams (.m3u8)
- Any webpage via iframe embed

## Technical Details

### Dependencies
- **hls.js** - For HLS video stream playback (loaded via CDN)

### Browser Support
- Chrome, Firefox, Safari, Edge (modern versions)
- Requires JavaScript enabled
- LocalStorage for saving preferences

### File Structure
```
CameraFeedDashboard/
├── Dashboard.html        # Main application (single-file, self-contained)
└── README.md             # This file
```

## Customization

### Changing Default Cameras

Edit the `DEFAULT_CAMERAS` array in the `<script>` section of `Dashboard.html`:

```javascript
const DEFAULT_CAMERAS = [
    {
        id: "unique-id",
        name: "Camera Display Name",
        url: "https://example.com/camera.jpg",
        type: "image",        // "image", "iframe", or "hls"
        refreshMs: 15000,     // Refresh interval in milliseconds
        visible: true,
        notes: "Optional description"
    },
    // ... more cameras
];
```

### Styling

All CSS is contained in the `<style>` section and uses CSS custom properties (variables) for easy theming:

```css
:root {
    --bg: #0f172a;
    --accent: #38bdf8;
    --text-main: #e5e7eb;
    --text-muted: #9ca3af;
    /* ... */
}
```

