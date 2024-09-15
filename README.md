<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Camera Access Example</title>
</head>
<body>

<h2>Capture an Image with Your Camera</h2>

<!-- Video element to display the live camera feed -->
<video id="cameraStream" width="320" height="240" autoplay></video>

<!-- Button to capture the current frame from the video -->
<button id="captureButton">Capture</button>

<!-- Canvas to hold the captured image -->
<canvas id="canvas" width="320" height="240" style="display:none;"></canvas>

<!-- Preview for the captured image -->
<img id="preview" style="max-width: 100%; height: auto; margin-top: 10px;">

<script>
    const video = document.getElementById('cameraStream');
    const canvas = document.getElementById('canvas');
    const context = canvas.getContext('2d');
    const captureButton = document.getElementById('captureButton');
    const preview = document.getElementById('preview');

    // Function to request camera access and stream the video
    function startCamera() {
        navigator.mediaDevices.getUserMedia({ video: true })
        .then(function(stream) {
            video.srcObject = stream;
        })
        .catch(function(error) {
            console.error("Error accessing the camera: ", error);
        });
    }

    // Capture button event listener
    captureButton.addEventListener('click', function() {
        // Draw the current video frame to the canvas
        context.drawImage(video, 0, 0, canvas.width, canvas.height);

        // Convert the canvas image to a data URL and display it
        const imageDataURL = canvas.toDataURL('image/png');
        preview.src = imageDataURL;
    });

    // Start the camera stream when the page loads
    window.addEventListener('load', startCamera);
</script>

</body>
</html>

