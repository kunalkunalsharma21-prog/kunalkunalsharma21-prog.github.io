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

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Three.js 3D Viewer</title>
  <style>
    body { margin: 0; overflow: hidden; background: #111; }
    canvas { display: block; }
  </style>
</head>
<body>

  <!-- Import maps polyfill & Three.js libraries -->
  <script type="importmap">
    {
      "imports": {
        "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
        "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
      }
    }
  </script>

  <script type="module">
    import * as THREE from 'three';
    import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
    import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';

    // 1. Scene, Camera, Renderer
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 1.5, 3);

    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.toneMapping = THREE.ACESFilmicToneMapping;
    document.body.appendChild(renderer.domElement);

    // 2. Controls (Orbit / Drag to rotate)
    const controls = new OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;

    // 3. Lighting
    const ambientLight = new THREE.AmbientLight(0xffffff, 1.5);
    scene.add(ambientLight);

    const dirLight = new THREE.DirectionalLight(0xffffff, 2.5);
    dirLight.position.set(5, 10, 7);
    scene.add(dirLight);

    // 4. Load 3D Model (.glb / .gltf)
    const loader = new GLTFLoader();
    const modelUrl = 'https://raw.githubusercontent.com/KhronosGroup/glTF-Sample-Models/master/2.0/Duck/glTF-Binary/Duck.glb';

    loader.load(
      modelUrl,
      (gltf) => {
        const model = gltf.scene;
        scene.add(model);
      },
      (xhr) => {
        console.log((xhr.loaded / xhr.total * 100) + '% loaded');
      },
      (error) => {
        console.error('An error happened loading the model:', error);
      }
    );

    // 5. Handle Resize
    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // 6. Animation Loop
    function animate() {
      requestAnimationFrame(animate);
      controls.update();
      renderer.render(scene, camera);
    }
    animate();
  </script>
</body>
</html>
