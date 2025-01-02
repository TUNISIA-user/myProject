<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cube Following Mouse</title>
  <style>
    body { margin: 0; overflow: hidden; }
    canvas { display: block; }
  </style>
</head>
<body>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script>
    // Scene setup
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    
    const geometry = new THREE.BoxGeometry(1, 1, 1); // Create a cube (1x1x1)
    const material = new THREE.MeshBasicMaterial({ color: 0x00ff00, wireframe: true }); // Green color, wireframe style
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube); // Add the cube to the scene

    camera.position.z = 5; // Move the camera back to view the cube

    // Mouse movement tracking
    let mouseX = 0;
    let mouseY = 0;

    // Event listener to track mouse position
    document.addEventListener('mousemove', (event) => {
      mouseX = (event.clientX / window.innerWidth) * 2 - 1; // Map mouse X position to -1 to 1
      mouseY = - (event.clientY / window.innerHeight) * 2 + 1; // Map mouse Y position to -1 to 1
    });

    // Animation loop
    function animate() {
      requestAnimationFrame(animate);

      // Map mouse position to cube position
      cube.position.x = mouseX * 2; // Scale mouseX for better movement range
      cube.position.y = mouseY * 2; // Scale mouseY for better movement range

      // Rotate cube for extra fun
      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;

      renderer.render(scene, camera); // Render the scene from the camera's perspective
    }

    animate(); // Start the animation loop
  </script>
</body>
</html>
