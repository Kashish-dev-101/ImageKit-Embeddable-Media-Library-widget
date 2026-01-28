# ImageKit Embeddable Media Library Widget

This repository contains a demo implementation of the ImageKit Embeddable Media Library Widget. It demonstrates how to integrate ImageKit DAM into a web application to browse, select, and insert media assets using a clean and minimal setup.

The project uses vanilla HTML, CSS, and JavaScript to showcase widget configuration, asset selection handling, and dynamic rendering of selected images.

## Live Demo

https://kashish-dev-101.github.io/ImageKit-Embeddable-Media-Library-widget

## Overview

The ImageKit Embeddable Media Library Widget allows applications to embed ImageKit DAM directly into their interface. Users can browse folders, search assets, select single or multiple files, and insert them into the application using a callback driven workflow.

This project focuses on demonstrating core widget capabilities in a simple and understandable way.

## Features

• Modal based Media Library integration  
• Multiple asset selection support  
• Insert event handling using widget callbacks  
• Dynamic image rendering after selection  
• Runtime ImageKit transformations for optimization  
• Minimal and responsive layout  

## Technology Stack

• HTML  
• CSS  
• JavaScript  
• ImageKit Media Library Widget  

## Implementation Details

### Widget Initialization

The Media Library Widget is loaded using the official ImageKit CDN and initialized with configurable options such as container, view type, selection behavior, and toolbar visibility.

The widget opens in modal view and renders inside a defined container element.

### Asset Selection Handling

When the user clicks the Insert button, the widget triggers a callback event. The callback listens for the INSERT event type and receives the selected assets as payload data.

Each selected asset is processed and rendered dynamically on the page.

### Image Optimization

Selected images are rendered using ImageKit URLs with transformations applied at runtime. This ensures optimized delivery and consistent dimensions across all rendered assets.

Example transformations include resizing images to fixed width and height for uniform display.


## Usage Scenarios

This implementation can be used as a reference for:

• CMS image selection workflows  
• Admin dashboards  
• Blog editors  
• Digital asset management tools  
• Internal content platforms  

## Documentation Reference

For complete configuration options and advanced usage, refer to the official ImageKit documentation:

https://imagekit.io/docs/dam/embeddable-media-library-widget








