# Vanilla File Uploader

A lightweight, dependency-free JavaScript file uploader with a modern, predictable state architecture inspired by React. It provides an easy-to-use HTML dataset API while remaining framework agnostic.

## Features

- 🚀 Zero dependencies
- 📦 Simple HTML data attribute configuration
- 🖼️ Single and multiple file uploads
- 📁 Built-in media library with search and pagination
- 👀 Optional image/file preview
- 🔒 Automatic CSRF token detection (Laravel compatible)
- ⚡ Duplicate input name detection during development
- 🎯 Framework agnostic

---

## Installation

Install via npm.

```bash
npm install stormcelltech-fileuploader
```

Then import it into your application.

```javascript
import "stormcelltech-fileuploader";
```

The uploader automatically initializes every element with the `.uploader` class after the DOM has loaded.

---

# Basic Usage

## HTML

```html
<div
  id="logo-uploader"
  class="uploader"
  data-fileinputname="logo_id"
  data-uploadtext="Select Logo"
  data-uploadtype="single"
  data-preview="true"
></div>
```

For Laravel Blade:

```blade
@vite(['resources/js/app.js'])

<div
    id="logo-uploader"
    class="uploader"
    data-fileinputname="logo_id">
</div>
```

That's all that's required.

---

# Manual Initialization

If you don't want automatic initialization, you can create an uploader manually.

```html
<div id="profile-uploader"></div>
```

```javascript
import "stormcelltech-fileuploader";

document.addEventListener("DOMContentLoaded", () => {
  const uploader = new FileUploader("profile-uploader");
});
```

---

# Configuration

The uploader is configured entirely through HTML data attributes.

| Attribute            | Type                     | Required | Default       | Description                                                    |
| -------------------- | ------------------------ | -------- | ------------- | -------------------------------------------------------------- |
| `id`                 | String                   | ✔        | —             | Unique element ID.                                             |
| `data-fileinputname` | String                   | ✔        | —             | Name of the hidden input that stores the selected media ID(s). |
| `data-hasfile`       | Integer or JSON Array    | ❌       | `null`        | Existing media ID(s) used to preload uploaded files.           |
| `data-uploadtype`    | String                   | ❌       | `single`      | `single` or `multiple`.                                        |
| `data-uploadtext`    | String                   | ❌       | `Select File` | Upload button text.                                            |
| `data-preview`       | Boolean (`true`/`false`) | ❌       | `true`        | Enable or disable file previews.                               |
| `data-hidemediatab`  | Boolean (`true`/`false`) | ❌       | `false`       | Hide the media library tab and only allow uploads.             |

---

## Example

```html
<div
  id="gallery"
  class="uploader"
  data-fileinputname="gallery"
  data-uploadtype="multiple"
  data-uploadtext="Upload Images"
  data-preview="true"
  data-hidemediatab="false"
></div>
```

---

# Preloading Existing Files

To preload files, provide the database media ID using `data-hasfile`.

Single file:

```html
<div class="uploader" data-fileinputname="logo_id" data-hasfile="12"></div>
```

Multiple files:

```html
<div
  class="uploader"
  data-fileinputname="gallery"
  data-uploadtype="multiple"
  data-hasfile="[12,15,18]"
></div>
```

> **Important**
>
> `data-hasfile` must contain **Media database IDs**, **not file URLs or file paths**.

---

# Backend API

The uploader expects the following endpoints.

## Upload

```
POST /media/upload
```

Expected response:

```json
{
  "data": {
    "id": 1,
    "thumb": "https://example.com/storage/thumb.jpg",
    "filename": "image.jpg"
  }
}
```

---

## Get Media

```
GET /media/{id}/get
```

Returns the media information used for hydration.

---

## List Media

```
GET /media/list?page=1&search=
```

Returns paginated media results.

---

## Delete Media

```
DELETE /media/{id}/delete
```

Deletes the selected media.

---

# Laravel Example

```blade
<div
    id="featured-image"
    class="uploader"
    data-fileinputname="featured_image_id"
    data-uploadtype="single"
    data-preview="true"
    data-uploadtext="Choose Featured Image">
</div>
```

```javascript
import "stormcelltech-fileuploader";
```

No additional JavaScript is required.

---

# Browser Support

Supports all modern browsers that implement:

- ES6 Modules
- Fetch API
- FormData
- Custom Events

---

# License

This project is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2026 Storm Cell Tech

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
