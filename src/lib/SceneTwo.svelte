<script>
  import {
    MeshStandardMaterial,
    BoxGeometry,
    SphereGeometry,
    BackSide
  } from 'three';
  import {
    PerspectiveCamera,
    DirectionalLight,
    AmbientLight,
    OrbitControls,
    Mesh
  } from '@threlte/core';
  import {
    GLTF,
    Float
  } from '@threlte/extras'

  const url = "https://raw.githubusercontent.com/mrdoob/three.js/dev/examples/models/gltf/MaterialsVariantsShoe/glTF/MaterialsVariantsShoe.gltf"
</script>

<PerspectiveCamera
  position={{ y: 5, z: 10 }}
  lookAt={{ y: 0 }}
>
  <OrbitControls />
</PerspectiveCamera>

<DirectionalLight shadow position={{ x: 1, y: 10, z: -1 }}/>
<AmbientLight />

<Float rotationIntensity={5}>
  <GLTF {url} scale={20} castShadow/>
</Float>

<Mesh 
  geometry={new BoxGeometry()}
  material={new MeshStandardMaterial({color: 'green'})}
  position={{ y: -2 }}
  scale={{ x: 10, y: 0.5, z: 10}}
  receiveShadow
/>

<Mesh
  geometry={new SphereGeometry()}
  material={new MeshStandardMaterial({color: 'orangered', side: BackSide})}
  scale={400}
/>