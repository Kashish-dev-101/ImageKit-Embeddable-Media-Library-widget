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

No backend required - it's a pure frontend solution.

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

## Configuration Options

| Option | Type | Description |
|--------|------|-------------|
| `container` | string | CSS selector for widget container |
| `view` | `"modal"` or `"inline"` | How the widget displays |
| `renderOpenButton` | boolean | Show/hide default button |
| `mlSettings.multiple` | boolean | Allow multiple selection |
| `mlSettings.maxFiles` | number | Max selectable files |
| `mlSettings.initialView` | object | Open in specific state |

### initialView Options

```javascript
initialView: { folderPath: "/marketing" }     // Open specific folder
initialView: { fileType: "images" }           // Filter by type
initialView: { searchQuery: 'name: "logo"' }  // Pre-filtered search
initialView: { collection: { id: "abc123" } } // Open collection
```

## Callback Payload

When users click "Insert":

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
