<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Webcam Attendance</title>
</head>
<body>
  <h1>Webcam Attendance System</h1>
  
  <div>
    <video id="videoFeed" width="640" height="480" autoplay></video>
  </div>

  <script>
    // Function to start webcam feed and request camera access
    async function startWebcam() {
      try {
        const videoFeed = document.getElementById('videoFeed');
        const stream = await navigator.mediaDevices.getUserMedia({ video: true });

        videoFeed.srcObject = stream;
      } catch (error) {
        console.error('Error accessing the camera:', error);
      }
    }

    // Check if browser supports getUserMedia
    if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
      startWebcam();
    } else {
      alert('Sorry, your browser does not support the getUserMedia API');
    }
  </script>
</body>
</html>

   
