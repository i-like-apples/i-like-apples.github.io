<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Camera Input Example</title>
</head>
<body>

<h2>Upload or Capture an Image</h2>

<!-- Input field for image selection or camera capture -->
<input type="file" accept="image/*" capture="camera" id="cameraInput">

<!-- Preview for the uploaded image -->
<img id="preview" style="display:none; max-width: 100%; height: auto; margin-top: 10px;">

<script>
    // Get the input and preview elements
    const cameraInput = document.getElementById('cameraInput');
    const preview = document.getElementById('preview');

    // Add event listener for when an image is selected
    cameraInput.addEventListener('change', function(event) {
        const file = event.target.files[0];

        if (file) {
            const reader = new FileReader();

            reader.onload = function(e) {
                // Set the preview image src to the file's data URL
                preview.src = e.target.result;
                preview.style.display = 'block';
            };

            // Read the file as a data URL
            reader.readAsDataURL(file);
        }
    });
</script>

</body>
</html>




