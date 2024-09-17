<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Camera Capture</title>
    <style>
        #preview {
            margin-top: 10px;
            max-width: 100%;
            height: auto;
        }
    </style>
</head>
<body>
    <h1>Take a Photo and Preview</h1>
    
    <!-- Button that opens camera -->
    <button id="cameraButton">Open Camera</button>
    
    <!-- Hidden input for camera capture -->
    <input type="file" accept="image/*" capture="camera" id="cameraInput" style="display: none;">
    
    <!-- Image preview -->
    <img id="preview" alt="Image Preview" />

    <script>
        // Get references to the elements
        const cameraButton = document.getElementById('cameraButton');
        const cameraInput = document.getElementById('cameraInput');
        const preview = document.getElementById('preview');

        // When the button is clicked, trigger the file input
        cameraButton.addEventListener('click', () => {
            cameraInput.click();
        });

        // When an image is selected (after capturing with camera)
        cameraInput.addEventListener('change', (event) => {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    preview.src = e.target.result;
                };
                reader.readAsDataURL(file);
            }
        });
    </script>
</body>
</html>

