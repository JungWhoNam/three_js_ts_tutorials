This repo contains resources for three.js with TS.

I followed these tutorials:
* https://threejs.org/docs/#manual/en/introduction/Installation.
* https://sbcode.net/threejs/create-threejs-boilerplate/

# Create a boilerplate
```shell
# if have not, install node.js from https://nodejs.org/en

# create a new project using vite
npm create vite@latest
# 1. type a project name
# 2. select `Vanilla`
# 3. select `TypeScript`
```
# Installation and Run
```shell
# cd to the new folder

# install required packages as shown in the package.json file
npm install

# three.js
npm install three --save-dev

# three.js in TS
npm install @types/three --save-dev
```

```shell
npm run dev
```

If everything went well, you'll see a URL like http://localhost:5173 appear in your terminal, and can open that URL to see your web application.

# Sample Project
This will create a spinning wireframe cube.

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

const geometry = new THREE.BoxGeometry()
const material = new THREE.MeshNormalMaterial({ wireframe: true })

const cube = new THREE.Mesh(geometry, material)
scene.add(cube)

function animate() {
  requestAnimationFrame(animate)

  cube.rotation.x += 0.01
  cube.rotation.y += 0.01

  renderer.render(scene, camera)
}

animate()
```

## .gitignore
`vite` creates one when you run `npm create vite@latest`.