<!-- Button to open camera -->
<button id="cameraButton">Open Camera</button>

<!-- Video stream to display camera preview -->
<video id="video" autoplay playsinline muted style="display: none;"></video>

<!-- Button to capture the photo -->
<button id="captureButton" style="display: none;">Capture Photo</button>

<!-- Image preview -->
<img id="preview" alt="Image Preview" />

<script>
    // Get references to the elements
    const cameraButton = document.getElementById('cameraButton');
    const video = document.getElementById('video');
    const captureButton = document.getElementById('captureButton');
    const preview = document.getElementById('preview');

    let stream;

    // When the camera button is clicked, access the camera
    cameraButton.addEventListener('click', async () => {
        try {
            // Check if we already have a stream
            if (!stream) {
                // Request access to the camera
                stream = await navigator.mediaDevices.getUserMedia({ video: true });
                video.srcObject = stream;
            }
            video.style.display = 'block';
            captureButton.style.display = 'inline-block';
            cameraButton.style.display = 'none';
        } catch (error) {
            console.error('Error accessing camera:', error);
            alert('Could not access the camera. Please allow camera access.');
        }
    });

    // Ensure the video metadata is loaded before enabling capture
    video.addEventListener('loadedmetadata', () => {
        // Only show the capture button if the video is ready
        if (video.videoWidth && video.videoHeight) {
            captureButton.disabled = false;
        }
    });

    // When the capture button is clicked, take a photo
    captureButton.addEventListener('click', () => {
        // Create a canvas to capture the photo
        const canvas = document.createElement('canvas');
        const width = video.videoWidth;
        const height = video.videoHeight;

        if (width && height) {
            canvas.width = width;
            canvas.height = height;

            // Draw the current frame from the video onto the canvas
            const context = canvas.getContext('2d');
            context.drawImage(video, 0, 0, canvas.width, canvas.height);

            // Convert the canvas image to a data URL and display it
            const dataUrl = canvas.toDataURL('image/png');
            preview.src = dataUrl;

            // Hide video and capture button, show camera button again
            video.style.display = 'none';
            captureButton.style.display = 'none';
            cameraButton.style.display = 'inline-block';
        } else {
            alert('Video not ready yet. Please try again.');
        }
    });
</script>
