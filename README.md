# html5-file-upload
HTML5 file upload plugin for jQuery

##How it works:
For older browsers that don't support the html5 file api, it gracefully degrades to the standard file input is rendered.  
Files are submitted like normal using multipart/form-data encoding.  For example, in PHP, the uploaded files are accessible using 
the $_FILES global array.

For modern browsers, this plugin will upgrade html file input field to be an html5 file upload with image preview and drag-n-drop functionality.  

Since the file input is read-only, this poses a problem for the drag-n-drop images.  Most HTML5 file upload plugins handle this by
performing an AJAX submission.  Depending on the situation, this might not be the desired solution.  The file upload might be one
of many form fields with complex backend validation. (aka Symfony Forms)

The plugin will add a hidden field called **__html5fileupload** to the form and set its value to true.  And it will base64 encode the image data
and send that on submission. On the backend, if the field __html5fileupload is present, it can decode the image data from the form field 
value.  If the field isn't present, that means it was an older browser, and the file will be present in the $_FILES global.

I will provide a helper php class and a symfony form type to automate this.


##Example Markup:

    <form method="POST" enctype="multipart/form-data">
        <input type="file" name="file" data-preview="#preview" data-dropzone="#dropzone" false>
        <ul id="preview"></ul>
        <div id="dropzone">Drop Zone</div>
        <input type="submit">
    </form>
    
    <script>
        $('input[type=file]').html5file();
    </script>
    
    
Attributes on file input:

  **multiple** - Allows for multiple files to be uploaded.  <input type="file" multiple>   
  **data-preview** - A jQuery selector for the dom element that will be the container for the file previews  
  **data-dropzone** - A jQuery selector for the dom element that will be the container for the dropzone  
  
Plugin Options:   
When initializing the plugin, you can pass a options object  **multiple**, **preview**, **dropzone** are all the same as the attributes above. 
**previewTemplate** - a string used to generate the preview items  

Preview Template   
The default preview template is:

    <li>
      <div class="file-preview-name">{{name}}</div>
      <div class="file-size">{{size}}</div>
      <div class="file-type">{{type}}</div>
      <div class="file-preview-img">{{img}}</div>
    </li>

You can pass in any string, and it will interpolate the values for name, size, type, and img



  
  
  
