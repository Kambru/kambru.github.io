<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
    <title>Marker AR Tracker</title>

    <!-- A-Frame: WebGL scene framework -->
    <script src="https://aframe.io/releases/1.5.0/aframe.min.js"></script>
    <!-- AR.js: camera + marker tracking via computer vision (getUserMedia + WebGL).
         No WebXR and no ARCore/ARKit involved, so this runs in Firefox for Android. -->
    <script src="https://cdn.jsdelivr.net/gh/AR-js-org/AR.js@3.4.5/aframe/build/aframe-ar.js"></script>

    <style>
      html, body { margin: 0; height: 100%; overflow: hidden; font-family: sans-serif; }

      #overlay {
        position: fixed;
        top: 0; left: 0; right: 0;
        z-index: 999;
        padding: 10px 14px;
        background: rgba(0, 0, 0, 0.55);
        color: #fff;
        font-size: 14px;
        line-height: 1.4;
        text-align: center;
        pointer-events: none;
      }

      #overlay a {
        color: #7fd3ff;
        pointer-events: auto;
      }
    </style>
  </head>
  <body>
    <div id="overlay">
      Point the camera at a <strong>Hiro</strong> marker to see the model appear.<br />
      No marker handy? <a href="https://cdn.jsdelivr.net/gh/AR-js-org/AR.js@3.4.5/data/images/HIRO.jpg" target="_blank" rel="noopener">Open the marker image</a>
      on another screen (or print it) and point this camera at it.
    </div>

    <a-scene
      embedded
      vr-mode-ui="enabled: false"
      renderer="logarithmicDepthBuffer: true; precision: medium;"
      arjs="sourceType: webcam; debugUIEnabled: false; detectionMode: mono_and_matrix;"
    >
      <a-assets>
        <a-asset-item
          id="model"
          src="https://cdn.jsdelivr.net/gh/KhronosGroup/glTF-Sample-Models@master/2.0/Duck/glTF-Binary/Duck.glb"
        ></a-asset-item>
      </a-assets>

      <!-- Built-in "hiro" pattern marker: no training/compilation step needed. -->
      <a-marker preset="hiro">
        <a-entity
          gltf-model="#model"
          position="0 0 0"
          scale="0.4 0.4 0.4"
          animation="property: rotation; to: 0 360 0; loop: true; dur: 6000; easing: linear"
        ></a-entity>
      </a-marker>

      <a-entity camera></a-entity>
    </a-scene>
  </body>
</html>
