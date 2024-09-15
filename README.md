<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Take a Photo</title>
    <style>
        #photo-box {
            width: 300px;
            height: 200px;
            border: 2px dashed #ccc;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            text-align: center;
        }

        #photo-box img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none; /* Initially, the image will be hidden */
        }
    </style>
</head>
<body>

<div id="photo-box">
    <p id="placeholder-text">Click to take a photo</p>
    <img id="photo-preview" alt="Photo Preview">
    <input type="file" id="file-input" accept="image/*" capture="camera" style="display:none;">
</div>

<script>
    const photoBox = document.getElementById('photo-box');
    const fileInput = document.getElementById('file-input');
    const photoPreview = document.getElementById('photo-preview');
    const placeholderText = document.getElementById('placeholder-text');

    // When the box is clicked, trigger the file input
    photoBox.addEventListener('click', () => {
        fileInput.click();
    });

    // When a photo is selected/taken, display it in the box
    fileInput.addEventListener('change', (event) => {
        const file = event.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = function(e) {
                // Hide the placeholder text and show the image preview
                placeholderText.style.display = 'none';
                photoPreview.style.display = 'block';
                photoPreview.src = e.target.result;
            };
            reader.readAsDataURL(file); // Read the photo as a Data URL to display it
        }
    });
</script>

</body>
</html>
