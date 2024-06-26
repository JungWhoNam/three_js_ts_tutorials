This repo contains resources for three.js with TS. This sample project will create a wireframe cube with OrbitControls, dat.gui, and stats panel.

I followed these tutorials:
* https://threejs.org/docs/#manual/en/introduction/Installation.
* https://sbcode.net/threejs/create-threejs-boilerplate/

# Install
```shell
git clone https://github.com/JungWhoNam/three_js_ts_tutorials.git

cd three_js_ts_tutorials

# install required packages as shown in the package.json file
npm install
```
> See below if interested in starting a project from scratch.

# Develop
```shell
npm run dev
```
Visit http://localhost:5173

# Build
```shell
# build the production version 
npm run build

# preview it locally in the browser
npm run preview
```
Visit http://localhost:4173/

# Or create a project from scratch
```shell
# if have not, install node.js from https://nodejs.org/en

# create a new project using vite
npm create vite@latest
# 1. type a project name
# 2. select `Vanilla`
# 3. select `TypeScript`

# cd to the new folder

# install required packages as shown in the package.json file
npm install

# three.js
npm install three --save-dev
npm install @types/three --save-dev

# dat.gui
npm install dat.gui@latest --save-dev
npm install @types/dat.gui@latest --save-dev
```

## .gitignore
`vite` creates one when you run `npm create vite@latest`.

## ./index.html
```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>three.js + TS</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.ts"></script>
  </body>
</html>
```

## ./src/style.css
```css
body {
  overflow: hidden;
  margin: 0px;
}
```

## ./src/main.ts
```typescript
import './style.css'
import * as THREE from 'three'
import { OrbitControls } from 'three/addons/controls/OrbitControls.js'
import Stats from 'three/addons/libs/stats.module.js'
import { GUI } from 'dat.gui'

const scene = new THREE.Scene()

const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
camera.position.z = 1.5

const renderer = new THREE.WebGLRenderer()
renderer.setSize(window.innerWidth, window.innerHeight)
document.body.appendChild(renderer.domElement)

window.addEventListener('resize', () => {
  camera.aspect = window.innerWidth / window.innerHeight
  camera.updateProjectionMatrix()
  renderer.setSize(window.innerWidth, window.innerHeight)
})

new OrbitControls(camera, renderer.domElement)

const geometry = new THREE.BoxGeometry()
const material = new THREE.MeshNormalMaterial({ wireframe: true })

const cube = new THREE.Mesh(geometry, material)
scene.add(cube)

const stats = new Stats()
document.body.appendChild(stats.dom)

const gui = new GUI()

const cubeFolder = gui.addFolder('Cube')
cubeFolder.add(cube.rotation, 'x', 0, Math.PI * 2)
cubeFolder.add(cube.rotation, 'y', 0, Math.PI * 2)
cubeFolder.add(cube.rotation, 'z', 0, Math.PI * 2)
cubeFolder.open()

const cameraFolder = gui.addFolder('Camera')
cameraFolder.add(camera.position, 'z', 0, 20)
cameraFolder.open()

function animate() {
  requestAnimationFrame(animate)

  // cube.rotation.x += 0.01
  // cube.rotation.y += 0.01

  renderer.render(scene, camera)

  stats.update()
}

animate()
```
