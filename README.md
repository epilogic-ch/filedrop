# File drop

Version 1.0

This is a simple file drop zone. It is based on 
[https://css-tricks.com/drag-and-drop-file-uploading/](https://css-tricks.com/drag-and-drop-file-uploading/)
documentation. References to jQuery have been removed and callback methods have
been added.

## How to use

Add following references in `<head>` of your html page:

``` html
<script type="text/javascript" src="filedrop.js"></script>
<link type="text/css" rel="stylesheet" href="filedrop.css"></link>
```

Add a drop zone using following code:

``` html
<div id="my-filedrop" class="fd-container">
    <div class="fd-drop-zone">
        <svg class="fd-drop-icon" xmlns="http://www.w3.org/2000/svg" width="50" height="43" viewBox="0 0 50 43">
            <path d="M48.4 26.5c-.9 0-1.7.7-1.7 1.7v11.6h-43.3v-11.6c0-.9-.7-1.7-1.7-1.7s-1.7.7-1.7 1.7v13.2c0 .9.7 1.7 1.7 1.7h46.7c.9 0 1.7-.7 1.7-1.7v-13.2c0-1-.7-1.7-1.7-1.7zm-24.5 6.1c.3.3.8.5 1.2.5.4 0 .9-.2 1.2-.5l10-11.6c.7-.7.7-1.7 0-2.4s-1.7-.7-2.4 0l-7.1 8.3v-25.3c0-.9-.7-1.7-1.7-1.7s-1.7.7-1.7 1.7v25.3l-7.1-8.3c-.7-.7-1.7-.7-2.4 0s-.7 1.7 0 2.4l10 11.6z"></path>
        </svg>
        <input class="fd-drop-input" type="file" name="pdffile" id="pdffile" data-multiple-caption="[count] files selected" multiple="true" />
        <label for="pdffile"></label> <!-- important : place label just after file input (CSS rules expect following order) -->
        <button class="fd-drop-upload-btn" type="button" onclick="filedrop.submit('#my-filedrop')">Upload</button>
    </div>
    <div class="fd-base-label"><strong>Choose a file</strong><span class="fd-dragndrop"> or drag it here</span></div>
    <div class="fd-uploading">Uploading…</div>
    <div class="fd-success">Done! <a href="javascript:void(0)" onclick="filedrop.reset('#my-filedrop')" class="fd-restart" role="button">Upload more?</a></div>
    <div class="fd-error">Error! <a href="javascript:void(0)" onclick="filedrop.reset('#my-filedrop')" class="fd-restart" role="button">Try again?</a><span></span>.</div>
    <div class="fd-oversize">Error, file is to big! <a href="javascript:void(0)" onclick="filedrop.reset('#my-filedrop')" class="fd-restart" role="button">Try other?</a><span></span>.</div>
</div>
```

The `my-filedrop` references should be updated, specially if you plan to add several file
drop zones in your page.

In order to initialize the drop zone, use following code:

``` javascript
filedrop.init({
    url: "uri:dummy",
    selector: '#my-filedrop'
});
```

## `filedrop` init options

| Option        | Description                                                                                                                                                        |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `url`         | Upload url                                                                                                                                                         |
| `selector`    | Selector of file drop zones                                                                                                                                        |
| `method`      | Upload method. Default is `POST`                                                                                                                                   |
| `maxFilesize` | Max uploadable file size (bytes)                                                                                                                                   |
| `timeout`     | Max upload request duration (milliseconds)                                                                                                                         |
| `autoSubmit`  | Flag `true`/`false` that indicates if upload should be launched automatically after file selection or file upload. When disabled, button "Upload" is made visible. |
| `onDrop`      | Callback method called when files are selected or dropped in zone. See details below.                                                                              |
| `onSubmit`    | Callback method called before submit. This method can be used to extend the form data or cancel upload. See details below.                                         |
| `onSuccess`   | Callback method called when files are uploaded successfully. See details below.                                                                                    |
| `onError`     | Callback method called when files upload failed. See details below.                                                                                                |
| `onComplete`  | Callback method called when files upload is finished (whenever it succeeded or failed). See details below.                                                         |

## Callbacks

### onDrop

Callback method called when files are selected or dropped in zone. Drop zone is reset when method return `false`.


Syntax:

``` javascript
onDrop: function(dropzone, files) {
    // ...
    // return false;  // -> reset the drop zone
}
```

| Parameter     | Description                    |
|---------------|--------------------------------|
| `dropzone`    | Drop zone element              |
| `files`       | List of selected/dropped files |

### onSubmit

Callback method called before submit. Submit is canceled when method return `false`.

Syntax:

``` javascript
onSubmit: function(dropzone, formdata) {
    // ...
    // return false;  // -> cancel the submit
}
```

| Parameter     | Description                                                                                                                                         |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `dropzone`    | Drop zone element                                                                                                                                   |
| `formdata`    | Form data going to be uploaded. The formdata contains files that will be uploaded. It can be extended using `formdata.append('fieldname', <value>)` |

### onSuccess

Callback method called when file is selected or dropped in zone.

Syntax:

``` javascript
onSuccess: function(dropzone, response) {
    // ...
}
```

| Parameter     | Description                    |
|---------------|--------------------------------|
| `dropzone`    | Drop zone element              |
| `response`    | Upload request response        |

### onError

Callback method called when files upload failed.

Syntax:

``` javascript
onError: function(dropzone, error) {
    // ...
}
```

| Parameter     | Description                    |
|---------------|--------------------------------|
| `dropzone`    | Drop zone element              |
| `error`       | Upload request error           |

### onComplete

Callback method called when files upload is finished (whenever it succeeded or failed).

Syntax:

``` javascript
onComplete: function(dropzone, error) {
    // ...
}
```

| Parameter     | Description                    |
|---------------|--------------------------------|
| `dropzone`    | Drop zone element              |
