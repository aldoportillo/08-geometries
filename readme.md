# Geometries

## What is a geometry?

A geometry starts with vertices which are coordinates, and they are used to create faces. This creates meshes, but without faces they make particles.

Each vertex has:

- position
- uv coordinates (2 values per coordinate)
- normals
- size (1 element in array)
- and more

## Built-in Geometries

- [BoxGeometry](https://threejs.org/docs/#api/en/geometries/BoxGeometry)
- [PlaneGeometry](https://threejs.org/docs/#api/en/geometries/PlaneGeometry)
- [CircleGeometry](https://threejs.org/docs/#api/en/geometries/CircleGeometry)
- [ConeGeometry](https://threejs.org/docs/#api/en/geometries/ConeGeometry)
- [CylinderGeometry](https://threejs.org/docs/#api/en/geometries/CylinderGeometry)
- [RingGeometry](https://threejs.org/docs/#api/en/geometries/RingGeometry)
- [TorusGeometry](https://threejs.org/docs/#api/en/geometries/TorusGeometry)
- [TorusKnotGeometry](https://threejs.org/docs/#api/en/geometries/TorusKnotGeometry)
- [DodecahedronGeometry](https://threejs.org/docs/#api/en/geometries/DodecahedronGeometry)
- [OctahedronGeometry](https://threejs.org/docs/#api/en/geometries/OctahedronGeometry)
- [Tetrahedron](https://threejs.org/docs/#api/en/geometries/Tetrahedron)
- [SphereGeometry](https://threejs.org/docs/#api/en/geometries/SphereGeometry)
- [ShapeGeometry](https://threejs.org/docs/#api/en/geometries/ShapeGeometry)
- [TubeGeometry](https://threejs.org/docs/#api/en/geometries/TubeGeometry)
- [ExtrudeGeometry](https://threejs.org/docs/#api/en/geometries/ExtrudeGeometry)
- [LatheGeometry](https://threejs.org/docs/#api/en/geometries/LatheGeometry)
- [TextGeometry](https://threejs.org/docs/#api/en/geometries/TextGeometry)

## Box Geometry

Parameters

- width (X)
- height (Y)
- depth (Z)
- widthSegments - how may triangles we have on the x segment (1 is 2 triangles, 2 is 8 triangles)
- heightSegments - how may triangles we have on the y segment
- depthSegments - how may triangles we have on the z segment

Why would we need more triangles? No use when it comes to the box. Maybe a plane? Lets say you're trying to map a mountain

```javascript
//You can use

const material = new THREE.MeshBasicMaterial({ color: 0xff0000, wireframe: true })

//To view triangle segments

```

## Buffer Geometry

Using Vanilla JS you can use a typed array to store geometry data.

### Float32Array

```javascript
// Method 1:

//Create Float32Array
const positionsArray = new Float32Array(9);

//First Vertex: xyz
positionsArray[0] = 0
positionsArray[1] = 0
positionsArray[2] = 0

//Second Vertex: xyz
positionsArray[3] = 0
positionsArray[4] = 1
positionsArray[5] = 0

//Second Vertex: xyz
positionsArray[6] = 1
positionsArray[7] = 0
positionsArray[8] = 0

//Method 2:

const positionsArray = new Float32Array([
    0, 0, 0,//First Vertex
    0, 1, 0,//Second Vertex
    1, 0, 0 //Third Vertex
])
```

### Use Float32Array to create BufferAttribute

```javascript

const geometry = new THREE.BufferGeometry()

const positionsAttribute = new THREE.BufferAttribute(positionsArray, 3)

geometry.setAttribute('position', positionsAttribute)

```

```javascript

const geometry = new THREE.BufferGeometry()

const count = 500;

const positionsArray = new Float32Array(count * 3 * 3) //Multiply by first three because each triangle has 3 vertexes and multiply for each 3 to get the triangles

for(let i = 0; i < count * 3 * 3; i++){
    positionsArray[i] = Math.random() - 0.5;
}

const positionsAttribute = new THREE.BufferAttribute(positionsArray, 3)

geometry.setAttribute('position', positionsAttribute)

```

### Indexes

You will notice that some faces do share a vertex, so you pass in indexes. Which will optimize the render to be easier on the GPU.
