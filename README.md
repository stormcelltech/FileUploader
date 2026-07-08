# Vanilla File Uploader

A lightweight, dependency-free JavaScript file uploader with a modern, React-inspired architecture. It provides a clean HTML data attribute API, built-in media library, previews, drag & drop uploads, and Laravel-friendly CSRF support.

## Features

- 🚀 Zero dependencies
- 📦 Automatic initialization
- 🖼️ Single & multiple file uploads
- 📁 Built-in media library
- 🔍 Media search with pagination
- 👀 Optional image previews
- 🖱️ Drag & drop support
- 🔒 Automatic Laravel CSRF detection
- ⚡ Duplicate input name detection
- 🎯 Framework agnostic
- 🔄 Preload existing media
- 🌐 Custom upload/update endpoint support

---

# Installation

Install using npm.

```bash
npm install stormcelltech-fileuploader
```

Import the package once in your application.

```javascript
import "stormcelltech-fileuploader";
```

The package automatically initializes every element with the `.uploader` class when the DOM has loaded.

---

# Basic Usage

```blade
@vite(['resources/js/app.js'])

<div
    id="logo-uploader"
    class="uploader"
    data-fileinputname="logo_id">
</div>
```

No additional JavaScript is required.

---

# Manual Initialization

If you don't want automatic initialization, instantiate it manually.

```html
<div id="profile-uploader"></div>
```

```javascript
import "stormcelltech-fileuploader";

document.addEventListener("DOMContentLoaded", () => {
  new FileUploader("profile-uploader");
});
```

---

# Configuration

The uploader is configured entirely through HTML data attributes.

| Attribute             | Type                   | Required | Default         | Description                                                      |
| --------------------- | ---------------------- | -------- | --------------- | ---------------------------------------------------------------- |
| `id`                  | String                 | ✅       | —               | Unique container ID.                                             |
| `data-fileinputname`  | String                 | ✅       | —               | Hidden input name used when submitting the selected media ID(s). |
| `data-uploadtype`     | `single` or `multiple` | No       | `single`        | Upload mode.                                                     |
| `data-uploadtext`     | String                 | No       | `Select Files`  | Upload button text.                                              |
| `data-preview`        | Boolean                | No       | `true`          | Enable preview rendering.                                        |
| `data-previewid`      | String                 | No       | Auto-generated  | Custom preview container ID.                                     |
| `data-hasfile`        | Integer or JSON Array  | No       | `null`          | Existing media ID(s) to preload.                                 |
| `data-hidemediatab`   | Boolean                | No       | `false`         | Hide the media library tab.                                      |
| `data-showbutton`     | Boolean                | No       | `1`             | Show or hide the upload button.                                  |
| `data-buttontype`     | `input` or `button`    | No       | `input`         | Button style.                                                    |
| `data-buttonstyle`    | String                 | No       | Package default | Custom CSS classes for the button.                               |
| `data-customupload`   | Boolean                | No       | `false`         | Automatically send uploaded image ID to a custom endpoint.       |
| `data-updateendpoint` | String                 | No       | `null`          | Endpoint used when `data-customupload="true"`.                   |

---

# Example

```html
<div
  id="gallery"
  class="uploader"
  data-fileinputname="gallery"
  data-uploadtype="multiple"
  data-uploadtext="Upload Images"
  data-preview="true"
></div>
```

---

# Preloading Existing Files

The uploader accepts **Media IDs**, not file URLs.

Single image:

```html
<div class="uploader" data-fileinputname="logo_id" data-hasfile="15"></div>
```

Multiple images:

```html
<div
  class="uploader"
  data-fileinputname="gallery"
  data-uploadtype="multiple"
  data-hasfile="[12,18,25]"
></div>
```

> **Important**
>
> `data-hasfile` **must contain Media database IDs**.
>
> Do **not** pass:
>
> - File URLs
> - Storage paths
> - File names

Incorrect:

```html
data-hasfile="/storage/logo.png"
```

Correct:

```html
data-hasfile="15"
```

---

# Custom Upload Endpoint

The uploader can automatically notify your application whenever a user uploads or selects a file.

Enable it using:

```html
<div
  id="avatar"
  class="uploader"
  data-fileinputname="avatar_id"
  data-customupload="true"
  data-updateendpoint="/profile/avatar"
></div>
```

Whenever a file is selected, the uploader sends:

```
PATCH /profile/avatar
```

Request body:

```json
{
  "imageId": 25
}
```

Headers:

```
Content-Type: application/json
Accept: application/json
X-CSRF-TOKEN: {token}
```

Expected response:

```json
{
  "status": 200,
  "message": "Avatar updated successfully."
}
```

If `status` is `200`, a success notification is displayed.

---

# Events

The uploader dispatches a custom event whenever a file is selected.

```javascript
document
  .getElementById("logo-uploader")
  .addEventListener("file:selected", (event) => {
    console.log(event.detail);
  });
```

Example event payload:

```javascript
{
    id: 15,
    filename: "logo.png",
    thumb: "https://example.com/storage/logo-thumb.png"
}
```

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
    "filename": "logo.png",
    "thumb": "https://example.com/storage/logo-thumb.png"
  }
}
```

---

## Get Media

```
GET /media/{id}/get
```

Returns a single media record.

---

## Media Library

```
GET /media/list?page=1&search=
```

Returns paginated media results.

Expected response:

```json
{
  "data": {
    "data": []
  }
}
```

---

## Delete Media

```
DELETE /media/{id}/delete
```

Deletes a media record.

---

# Laravel Example

```blade
<div
    id="featured-image"
    class="uploader"
    data-fileinputname="featured_image_id"
    data-uploadtext="Choose Featured Image"
    data-preview="true">
</div>
```

```javascript
import "stormcelltech-fileuploader";
```

That's it.

---

# Browser Support

Supports all modern browsers with:

- ES6 Modules
- Fetch API
- FormData
- XMLHttpRequest
- Custom Events

---

# License

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
