---

# WebVR

An open virtual reality platform with the advantages of **the Web**

<div class="captioned-image-row">
  <div>
    <img data-src="media/img/web-is-open.png">
    <i>Open</i>
  </div>
  <div>
    <img data-src="media/img/web-is-connected.png">
    <i>Connected</i>
  </div>
  <div>
    <img data-src="media/img/web-is-instant.png">
    <i>Instant</i>
  </div>
</div>

<!-- NOTES -->
WebVR is...virtual reality in the browser, powered by the Internet

Open:
- Anyone can publish
- Open source culture with open standards

Connected:
- Traverse worlds

Instant:
- Click a link on Twitter or Weibo, immediate virtual experiences
---

##Goals <sup class="reference">[3]</sup>

* Detect available Virtual Reality devices
* Query the devices capabilities
* Poll the device’s position and orientation
* Display imagery on the device at the appropriate frame rate

<!-- NOTES -->
- How does WebVR work??
---

<img class="stretch" data-src="media/img/webvr.png">

Browser APIs that enable WebGL rendering to headsets and access to VR
sensors

https://w3c.github.io/webvr/

> **API** : A set of routines, protocols, and tools for building software applications

<!-- NOTES -->

WebGL:
- A JavaScript API for rendering interactive 3D and 2D graphics
  within any compatible web browser


API:
- Optimized rendering path to headsets
- Access position and rotation (pose) data

History:
- Initial WebVR API by Mozilla
- Working W3C community group

Not just a specification, it's implemented...

---

https://webvr.rocks

<div class="captioned-image-row small">
  <div>
    <img data-src="media/img/firefox-nightly.png">
    <i>Firefox Nightly</i>
  </div>
  <div>
    <img data-src="media/img/edge.jpg">
    <i>Microsoft Edge</i>
  </div>
  <div>
    <img data-src="media/img/chromium.png">
    <i>Chromium</i>
  </div>
</div>

<div class="captioned-image-row small">
  <div>
    <img data-src="media/img/chrome.jpg">
    <i>Chrome for Android</i>
  </div>
  <div>
    <img data-src="media/img/carmel.jpg">
    <i>Oculus Carmel</i>
  </div>
  <div>
    <img data-src="media/img/samsung-browser.png">
    <i>Samsung Internet</i>
  </div>
  <div>
    <img data-src="media/img/google-cardboard.png">
    <i>Mobile Polyfill</i>
  </div>
</div>

<!-- NOTES -->

- Mozilla, Google, Samsung, Microsoft, community currently iterating WebVR 1.0 API
- Firefox + Chrome WebVR 1.0 hits release channels by early 2017
- Currently behind Nightly, custom builds, and flags
- Mobile Polyfill: use device motion / orientation sensors to polyfill on smartphones
- What is the end goal...

---

## Metaverse

<!-- .slide: data-background="media/img/metaverse.jpg" -->

<!-- NOTES -->
- Metaverse: a shared virtual-reality space where users can interact
  with the virtual envrionment and other users
- Requiring decentralized/open/connected space, the Web is best platform to fully realize
- Where do we begin?

---
## (Possible) Solutions

<div class="captioned-image-row medium">
  <div>
    <img data-src="media/img/WebGL_Logo.png">
  </div>
  <div>
    <img data-src="media/img/threejs-logo.png">
  </div>
    <div>
    <img data-src="media/img/Unity.png">
  </div>
</div>

<!-- NOTES -->
- WebGL: A JavaScript API for rendering interactive 3D and 2D graphics
  within any compatible web browser
- three.js: A JavaScript API to create and display 3D computer graphics, that
  is built on top of WebGL
- Unity: Cross-platform game engine primarily aimed for video games and simulations

- You could use native WebGL, but let's see what that requires...

---
## Creating a rotating cube in WebGL<sup class="reference">[4]</sup>
<div class="row-content">
  <div>
    <video data-autoplay loop src="media/video/rotating_cube_webgl.mov"></video>
  </div>
  <div class="code-block">
  <pre> <code class="html">
  <!doctype html>
  <html>
     <body>
        <canvas width = "570" height = "570" id = "my_Canvas"></canvas>

        <script>

           /*============= Creating a canvas =================*/
           var canvas = document.getElementById('my_Canvas');
           gl = canvas.getContext('experimental-webgl');

           /*============ Defining and storing the geometry =========*/

           var vertices = [
              -1,-1,-1, 1,-1,-1, 1, 1,-1, -1, 1,-1,
              -1,-1, 1, 1,-1, 1, 1, 1, 1, -1, 1, 1,
              -1,-1,-1, -1, 1,-1, -1, 1, 1, -1,-1, 1,
              1,-1,-1, 1, 1,-1, 1, 1, 1, 1,-1, 1,
              -1,-1,-1, -1,-1, 1, 1,-1, 1, 1,-1,-1,
              -1, 1,-1, -1, 1, 1, 1, 1, 1, 1, 1,-1,
           ];

           var colors = [
              5,3,7, 5,3,7, 5,3,7, 5,3,7,
              1,1,3, 1,1,3, 1,1,3, 1,1,3,
              0,0,1, 0,0,1, 0,0,1, 0,0,1,
              1,0,0, 1,0,0, 1,0,0, 1,0,0,
              1,1,0, 1,1,0, 1,1,0, 1,1,0,
              0,1,0, 0,1,0, 0,1,0, 0,1,0
           ];

           var indices = [
              0,1,2, 0,2,3, 4,5,6, 4,6,7,
              8,9,10, 8,10,11, 12,13,14, 12,14,15,
              16,17,18, 16,18,19, 20,21,22, 20,22,23
           ];

           // Create and store data into vertex buffer
           var vertex_buffer = gl.createBuffer ();
           gl.bindBuffer(gl.ARRAY_BUFFER, vertex_buffer);
           gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(vertices), gl.STATIC_DRAW);

           // Create and store data into color buffer
           var color_buffer = gl.createBuffer ();
           gl.bindBuffer(gl.ARRAY_BUFFER, color_buffer);
           gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(colors), gl.STATIC_DRAW);

           // Create and store data into index buffer
           var index_buffer = gl.createBuffer ();
           gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, index_buffer);
           gl.bufferData(gl.ELEMENT_ARRAY_BUFFER, new Uint16Array(indices), gl.STATIC_DRAW);

           /*=================== Shaders =========================*/

           var vertCode = 'attribute vec3 position;'+
              'uniform mat4 Pmatrix;'+
              'uniform mat4 Vmatrix;'+
              'uniform mat4 Mmatrix;'+
              'attribute vec3 color;'+//the color of the point
              'varying vec3 vColor;'+

              'void main(void) { '+//pre-built function
                 'gl_Position = Pmatrix*Vmatrix*Mmatrix*vec4(position, 1.);'+
                 'vColor = color;'+
              '}';

           var fragCode = 'precision mediump float;'+
              'varying vec3 vColor;'+
              'void main(void) {'+
                 'gl_FragColor = vec4(vColor, 1.);'+
              '}';

           var vertShader = gl.createShader(gl.VERTEX_SHADER);
           gl.shaderSource(vertShader, vertCode);
           gl.compileShader(vertShader);

           var fragShader = gl.createShader(gl.FRAGMENT_SHADER);
           gl.shaderSource(fragShader, fragCode);
           gl.compileShader(fragShader);

           var shaderProgram = gl.createProgram();
           gl.attachShader(shaderProgram, vertShader);
           gl.attachShader(shaderProgram, fragShader);
           gl.linkProgram(shaderProgram);

           /* ====== Associating attributes to vertex shader =====*/
           var Pmatrix = gl.getUniformLocation(shaderProgram, "Pmatrix");
           var Vmatrix = gl.getUniformLocation(shaderProgram, "Vmatrix");
           var Mmatrix = gl.getUniformLocation(shaderProgram, "Mmatrix");

           gl.bindBuffer(gl.ARRAY_BUFFER, vertex_buffer);
           var position = gl.getAttribLocation(shaderProgram, "position");
           gl.vertexAttribPointer(position, 3, gl.FLOAT, false,0,0) ;

           // Position
           gl.enableVertexAttribArray(position);
           gl.bindBuffer(gl.ARRAY_BUFFER, color_buffer);
           var color = gl.getAttribLocation(shaderProgram, "color");
           gl.vertexAttribPointer(color, 3, gl.FLOAT, false,0,0) ;

           // Color
           gl.enableVertexAttribArray(color);
           gl.useProgram(shaderProgram);

           /*==================== MATRIX =====================*/

           function get_projection(angle, a, zMin, zMax) {
              var ang = Math.tan((angle*.5)*Math.PI/180);//angle*.5
              return [
                 0.5/ang, 0 , 0, 0,
                 0, 0.5*a/ang, 0, 0,
                 0, 0, -(zMax+zMin)/(zMax-zMin), -1,
                 0, 0, (-2*zMax*zMin)/(zMax-zMin), 0
              ];
           }

           var proj_matrix = get_projection(40, canvas.width/canvas.height, 1, 100);

           var mov_matrix = [1,0,0,0, 0,1,0,0, 0,0,1,0, 0,0,0,1];
           var view_matrix = [1,0,0,0, 0,1,0,0, 0,0,1,0, 0,0,0,1];

           // translating z
           view_matrix[14] = view_matrix[14]-6;//zoom

           /*==================== Rotation ====================*/

           function rotateZ(m, angle) {
              var c = Math.cos(angle);
              var s = Math.sin(angle);
              var mv0 = m[0], mv4 = m[4], mv8 = m[8];

              m[0] = c*m[0]-s*m[1];
              m[4] = c*m[4]-s*m[5];
              m[8] = c*m[8]-s*m[9];

              m[1]=c*m[1]+s*mv0;
              m[5]=c*m[5]+s*mv4;
              m[9]=c*m[9]+s*mv8;
           }

           function rotateX(m, angle) {
              var c = Math.cos(angle);
              var s = Math.sin(angle);
              var mv1 = m[1], mv5 = m[5], mv9 = m[9];

              m[1] = m[1]*c-m[2]*s;
              m[5] = m[5]*c-m[6]*s;
              m[9] = m[9]*c-m[10]*s;

              m[2] = m[2]*c+mv1*s;
              m[6] = m[6]*c+mv5*s;
              m[10] = m[10]*c+mv9*s;
           }

           function rotateY(m, angle) {
              var c = Math.cos(angle);
              var s = Math.sin(angle);
              var mv0 = m[0], mv4 = m[4], mv8 = m[8];

              m[0] = c*m[0]+s*m[2];
              m[4] = c*m[4]+s*m[6];
              m[8] = c*m[8]+s*m[10];

              m[2] = c*m[2]-s*mv0;
              m[6] = c*m[6]-s*mv4;
              m[10] = c*m[10]-s*mv8;
           }

           /*================= Drawing ===========================*/
           var time_old = 0;

           var animate = function(time) {

              var dt = time-time_old;
              rotateZ(mov_matrix, dt*0.005);//time
              rotateY(mov_matrix, dt*0.002);
              rotateX(mov_matrix, dt*0.003);
              time_old = time;

              gl.enable(gl.DEPTH_TEST);
              gl.depthFunc(gl.LEQUAL);
              gl.clearColor(0.5, 0.5, 0.5, 0.9);
              gl.clearDepth(1.0);

              gl.viewport(0.0, 0.0, canvas.width, canvas.height);
              gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
              gl.uniformMatrix4fv(Pmatrix, false, proj_matrix);
              gl.uniformMatrix4fv(Vmatrix, false, view_matrix);
              gl.uniformMatrix4fv(Mmatrix, false, mov_matrix);
              gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, index_buffer);
              gl.drawElements(gl.TRIANGLES, indices.length, gl.UNSIGNED_SHORT, 0);

              window.requestAnimationFrame(animate);
           }
           animate(0);

        </script>

     </body>
  </html>
  </code></pre>  
  </div>
</div>

<!-- NOTES -->
- A lot of graphics programming
- Screen Buffer, Matrices (Model, View, Projection)
- What about Three.JS?
---

## Creating a rotating cube in Three.JS<sup class="reference">[5]</sup>
<div class="row-content">
  <div>
    <video data-autoplay loop src="media/video/rotating_cube_threejs.mov"></video>
  </div>
  <div class="code-block">
    <pre> <code class="html">
      <!doctype html>
      <html>
      <head>
          <title>Rotating logo - WebGL experiment</title>
      </head>
      <body>
          <div id="container"></div>
          <script src="js/three.min.js"></script>
          <script type="text/javascript">

            var scene, camera, renderer;

            var WIDTH  = window.innerWidth;
            var HEIGHT = window.innerHeight;

            var SPEED = 0.01;

            function init() {
                scene = new THREE.Scene();

                initCube();
                initCamera();
                initRenderer();

                document.body.appendChild(renderer.domElement);
            }

            function initCamera() {
                camera = new THREE.PerspectiveCamera(70, WIDTH / HEIGHT, 1, 10);
                camera.position.set(0, 3.5, 5);
                camera.lookAt(scene.position);
            }

            function initRenderer() {
                renderer = new THREE.WebGLRenderer({ antialias: true });
                renderer.setSize(WIDTH, HEIGHT);
            }

            function initCube() {
                cube = new THREE.Mesh(new THREE.CubeGeometry(2, 2, 2), new THREE.MeshNormalMaterial());
                scene.add(cube);
            }

            function rotateCube() {
                cube.rotation.x -= SPEED * 2;
                cube.rotation.y -= SPEED;
                cube.rotation.z -= SPEED * 3;
            }

            function render() {
                requestAnimationFrame(render);
                rotateCube();
                renderer.render(scene, camera);
            }

            init();
            render();

          </script>
      </body>
      </html>
    </code></pre>  
  </div>
</div>

<!-- NOTES -->
- Easier to understand, but still a bit heavy
- Still need to setup scene before setting up content
---

<!-- .slide: data-background-video="media/video/boilerplate.mp4" data-state="state--bg-dark" data-background-video-loop="true"-->

<div class="slide__boilerplate">
  <p>Import WebVR polyfill</p>
  <p>Set up camera</p>
  <p>Set up lights</p>
  <p>Initialize scene</p>
  <p>Declare and pass canvas</p>
  <p>Listen to window resize</p>
  <p>Install VREffect</p>
  <p>Instantiate renderer</p>
  <p>Create render loop</p>
  <p>Preload assets</p>
  <p>Figure out responsiveness</p>
  <p>Deal with metatags and mobile</p>
</div>

<!-- NOTES -->
- It's still too difficult to create WebVR experiences
- Huge obstacle if doing small prototypes and experiments
- Boilerplate needs updating with new versions of WebVR, three.js, and browser quirks
- Encapsulate all of that into one line...