# Vanilla File Uploader

A robust, dependency-free vanilla JavaScript file upload component utilizing an immutable, React-inspired state-to-view architecture. Replaces heavy framework overhead while maintaining a predictable unidirectional data flow.

## Features

- 🚀 **Zero Dependencies** — Pure vanilla JS.
- 📦 **Declarative HTML Dataset API** — Configure your instances directly in HTML.
- 🖼️ **Media Library & Upload Tabs** — Toggles seamlessly with search and pagination support.
- 🔒 **CSRF Protected** — Automatically finds and applies Laravel-style CSRF tokens.
- ⚡ **Anti-Collision Guard** — Detects duplicate form input names safely during development.

---

## Installation

Install the package via npm:

```bash
npm install stormcelltech-fileuploader
```

## Usage

1. HTML Configuration
   Place a target wrapper element in your HTML with configuration dataset properties.

```html
<div
  id="logo-uploader"
  class="uploader"
  data-fileinputname="logo_id"
  data-uploadtext="Select Logo"
  data-uploadtype="single"
  data-preview="true"
  data-hasfile="12"
></div>
```

2. Initialization
   Import the module into your application. The package will automatically boot any elements with the .uploader class once the DOM loads.

```js
import "stormcelltech-fileuploader";
```

```html
@vite(['resources/js/app.js'])

<div id="manual-uploader" class="uploader" data-fileinputname="avatar"></div>
```

Put this anywhere in your blade

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

## Customer initialization

In your `resources/js/app.js`

```
<div id="custom-profile-upload"></div>
// Just importing and instantiating it once here handles everything!
// When this file runs, it looks for all '.uploader' elements on the current page.
<script>
    document.addEventListener('DOMContentLoaded', () => {
        // This is safe because the package binds itself to the window object!
        const profileUploader = new FileUploader('custom-profile-upload');
    });
</script>
```

# Configuration Data Attributes Matrix This technical reference outlines the

absolute data attribute API schema required by the `FileUploader.js` client
engine. The runtime engine parses these attributes to build the component state,
handle database hydration, and toggle UI states. --- ## 3. Core Specification
Matrix The following parameters must be declared as standard HTML5 attributes on
the container DOM element designated with the `class="uploader"` marker: |
Attribute Name | Expected Data Type | Required | Default Value | Functional
Impact & Component Scope | | :------------------- | :----------------- |
:------: | :-------------- |
:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
| | `id` | `String` | **Yes** | _None_ | Unique DOM layout identifier. Used by
the internal runtime registry (`FileUploader.instances`) to manage scoped event
dispatching. | | `data-fileinputname` | `String` | **Yes** | _None_ | Dictates
the `name` attribute value applied to the hidden HTML `<input />` tag that
stores the database entity ID. | | `data-hasfile` | `Integer\|Array` | No |
`null` | **Hydration Value:** Holds the primary database integer ID of the asset
(or a JSON-serialized array of IDs for multi-mode). Prompts the engine to pull
matching asset metadata. | | `data-uploadtype` | `String` | No | `'single'` |
Structurally controls the file array constraints. Supported tokens are
`'single'` or `'multiple'`. | | `data-uploadtext` | `String` | No | `'Select
File'` | UI Typography Override. Customizes the main text string value rendered
inside the primary drag-and-drop landing action wrapper. | | `data-preview` |
`String` | No | `'true'` | Textual boolean toggle (`'true'`/`'false'`). Dictates
whether file thumbnail blocks and interactive image modules render inside the
workspace. | | `data-hidemediatab` | `String` | No | `'false'` | Textual boolean
toggle (`'true'`/`'false'`). When `'true'`, strips out the historical file
library browser, restricting the interface to fresh file uploads only. | --- ##
⚠️ Critical Data Integrity Rule Never pass a URL or file path to `data-hasfile`.
It expects a database Media ID integer. Passing a non-integer string breaks
backend framework form hydration. ## Backend Requirements The component
communicates natively via standard endpoints: - [x] Upload (`POST
/media/upload`): Receives `multipart/form-data`. Expects a JSON response
containing `{ data: { id: 1, thumb: 'url', filename: 'name.jpg' } }`. - [x]
Fetch Details (`GET /media/{id}/get`): Expects details for hydration rendering.

- [x] List Library (`GET /media/list?page=1&search=`): Returns paginated archive
      results. - [x] Delete (`DELETE /media/{id}/delete`): Clears file from
      disk/database. ## License This project is licensed under the **MIT License**.

```text MIT License Copyright (c) 2026 Your Name or Company Permission is hereby
granted, free of charge, to any person obtaining a copy of this software and
associated documentation files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use, copy, modify,
merge, publish, distribute, sublicense, and/or sell copies of the Software, and
to permit persons to whom the Software is furnished to do so, subject to the
following conditions: The above copyright notice and this permission notice
shall be included in all copies or substantial portions of the Software. THE
SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
