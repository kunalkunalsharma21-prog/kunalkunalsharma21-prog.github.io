<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>3D Model Viewer</title>
  
  <!-- Import the model-viewer component -->
  <script type="module" src="https://ajax.googleapis.com/ajax/libs/model-viewer/3.4.0/model-viewer.min.js"></script>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      background: #121212;
      color: #ffffff;
      font-family: sans-serif;
    }
    model-viewer {
      width: 80vw;
      height: 70vh;
      background-color: #1e1e1e;
      border-radius: 12px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
    }
  </style>
</head>
<body>

  <h1>Interactive 3D Model</h1>
  
  <!-- 
    Replace 'src' with your own .glb or .gltf file link or local path.
    Example free model: NASA's astronaut GLB file 
  -->
  <model-viewer 
    src="https://modelviewer.dev/shared-assets/models/Astronaut.glb"
    alt="A 3D model of an astronaut"
    auto-rotate 
    camera-controls 
    ar 
    shadow-intensity="1">
  </model-viewer>

</body>
</html>

