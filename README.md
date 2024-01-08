<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Webcam Attendance</title>
  <style>
    video {
      width: 100%;
      height: auto;
    }
    #capture-btn {
      display: block;
      margin: 20px auto;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Webcam Attendance</h1>
  <video id="videoElement" autoplay></video>
  <button id="capture-btn">Capture Attendance</button>

  <script>
    const video = document.getElementById('videoElement');

    // Prompt user for camera access
    navigator.mediaDevices.getUserMedia({ video: true })
      .then(stream => {
        video.srcObject = stream;
      })
      .catch(err => {
        console.error('Error accessing the camera:', err);
      });

    // Function to capture attendance
    document.getElementById('capture-btn').addEventListener('click', () => {
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      ctx.drawImage(video, 0, 0, canvas.width, canvas.height);

      // Convert the captured image to base64
      const imageData = canvas.toDataURL('image/png');

      // You can send this imageData to a server for attendance processing or save it locally
      console.log('Attendance captured:', imageData);
      // Alternatively, you can perform further operations like sending data to a server using fetch or AJAX
      // Example:
      // fetch('/attendance', {
      //   method: 'POST',
      //   body: JSON.stringify({ image: imageData }),
      //   headers: {
      //     'Content-Type': 'application/json'
      //   }
      // })
      // .then(response => response.json())
      // .then(data => {
      //   console.log('Attendance sent:', data);
      // })
      // .catch(error => {
      //   console.error('Error sending attendance:', error);
      // });
    });
  </script>
</body>
</html>
