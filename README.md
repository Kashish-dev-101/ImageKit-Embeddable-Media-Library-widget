# ImageKit Media Library Widget Demo

Embed ImageKit's [Media Library](https://imagekit.io/docs/dam/embeddable-media-library-widget) into your web application. Browse, search, and select assets without leaving your app.

## Live Demo

**[Try it here →](https://kashish-dev-101.github.io/ImageKit-Embeddable-Media-Library-widget/widget.html)**

## What is This?

The Media Library Widget lets you integrate ImageKit's [Digital Asset Management (DAM)](https://imagekit.io/docs/dam/overview) into any web app. Users can:

- Browse folders and collections
- Search for assets
- Select single or multiple files
- Insert them into your application

The widget runs in the browser. Users log in with their ImageKit credentials (or via SSO / signature-based login — see [Login options](#login-options)).

## Quick Start

### 1. Add the Script

```html
<script src="https://unpkg.com/imagekit-media-library-widget/dist/imagekit-media-library-widget.min.js"></script>
```

### 2. Create a Container

```html
<div id="container"></div>
```

### 3. Initialize the Widget

```javascript
const config = {
  container: "#container",
  view: "modal",
  renderOpenButton: true,
  mlSettings: {
    multiple: true,
    maxFiles: 10,
  },
};

function callback(payload) {
  if (payload.eventType === "INSERT") {
    console.log("Selected files:", payload.data);
  }
}

const widget = new IKMediaLibraryWidget(config, callback);
```

That's it! Click the button and start selecting assets.

## Using the `open()` Method

For custom buttons with different behaviors:

```javascript
// Initialize without default button
const widget = new IKMediaLibraryWidget({
  container: "#container",
  renderOpenButton: false,
}, callback);

// Custom button - opens filtered to images only
document.getElementById("pickImages").addEventListener("click", () => {
  widget.open({
    mlSettings: {
      initialView: { fileType: "images" },
      multiple: true,
      maxFiles: 5,
    },
  });
});
```

> **Note:** `mlSettings` passed to `open()` **completely replace** the `mlSettings` from the constructor — they are not merged. Repeat every setting you want to keep.

## Configuration Options

| Option | Type | Description |
|--------|------|-------------|
| `container` **(required)** | string \| HTMLElement | CSS selector or DOM element where the widget is rendered |
| `className` | string | Custom CSS class for the container |
| `dimensions` | object | `{ height, width }` of the container |
| `view` | `"modal"` \| `"inline"` | Overlay or embedded display. Default `"modal"` |
| `renderOpenButton` | boolean | Show the default "Open Media Library" button. Set `false` when using custom triggers. Default `true` |
| `mlSettings` | object | Media Library behaviour (below) |

### mlSettings Options

| Option | Type | Description |
|--------|------|-------------|
| `initialView` | object | Initial state when the widget opens (only **one** property — see below) |
| `multiple` | boolean | Allow multiple selection. Default `true` |
| `maxFiles` | number | Max assets per insert (only when `multiple: true`) |
| `toolbar.showCloseButton` | boolean | Default `true` |
| `toolbar.showInsertButton` | boolean | Default `true` |
| `toolbar.showAccountSwitcher` | boolean | Show "Switch account" for users with access to more than one account. Default `false` |
| `queryParams` | object | Extra query parameters appended to the widget URL |
| `widgetImagekitId` | string | ImageKit ID to open; widget stays on this account and hides "Switch account" |
| `loginViaSSO` | boolean | Automatically initiate SSO login |

### initialView Options

Only one property at a time. For complex filtering use `searchQuery`.

```javascript
initialView: { searchQuery: 'name: "logo"' }  // Lucene-like query, same as the List & Search Assets API
initialView: { folderPath: "/marketing" }     // Open specific folder (must start with /)
initialView: { fileId: "abc123" }             // Open file detail view
initialView: { collection: {} }               // All collections
initialView: { collection: { id: "abc123" } } // Specific collection
initialView: { fileType: "images" }           // "images" | "videos" | "cssJs" | "others"
```

## Login Options

- **ImageKit login** — users enter their ImageKit email and password when the widget opens (skipped if already logged in in that browser).
- **SSO** — set `mlSettings.widgetImagekitId` and `mlSettings.loginViaSSO: true` to use an existing SSO session.
- **Signature-based login (enterprise)** — signature built from the account's private key and the user's email; contact your ImageKit Customer Success Manager.

## Switching Accounts

Set `mlSettings.toolbar.showAccountSwitcher: true`. The option appears only when the user has access to more than one account, and is hidden when `widgetImagekitId` is set or a signed login link is used. From widget version 2.5.0, "Switch account" and "Log out" share one account menu.

## Callback Payload

When users click "Insert" (each item in `data` follows the [List & Search Assets API](https://imagekit.io/docs/api-reference/digital-asset-management-dam/list-and-search-assets) schema; abridged below):

```javascript
{
  eventType: "INSERT",
  data: [
    {
      fileId: "abc123",
      name: "image.jpg",
      url: "https://ik.imagekit.io/your_id/image.jpg",
      filePath: "/folder/image.jpg",
      fileType: "image"
    }
  ]
}
```

## Project Files

```
├── widget.html   # Demo page
├── widget.css    # Styles
└── README.md
```

## Use Cases

- **CMS Integration** - Let editors pick images without leaving the editor
- **Admin Dashboards** - Manage media assets inline
- **E-commerce** - Select product images
- **Blog Platforms** - Insert images into posts

## Resources

- [ImageKit Embeddable Media Library Widget Documentation](https://imagekit.io/docs/dam/embeddable-media-library-widget)
- [ImageKit Dashboard](https://imagekit.io/dashboard)

## License

ISC

---
