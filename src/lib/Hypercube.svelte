<script>
  import {
    PerspectiveCamera,
    DirectionalLight,
    AmbientLight,
    Mesh,
    useFrame,
    Object3DInstance,
    OrbitControls,
    useThrelte,
    InteractiveObject,
    Line2,
  } from '@threlte/core';
  import {
    MeshStandardMaterial,
    CylinderGeometry,
    SphereGeometry,
    GridHelper,
    AxesHelper,
    Vector3
  } from 'three';
  import { LineMaterial } from 'three/examples/jsm/lines/LineMaterial'
  import { tweened } from 'svelte/motion';
  import {
    Text
  } from '@threlte/extras'
  import { spring } from 'svelte/motion'

  export let root;

  const t = tweened(3, { duration: 2000 });
  let r = 0;
  export let position = {x:-100, y: 5, z:-100}
  // Use delta to ensure motion is consistent at any frame rate
  // Learn more: https://discoverthreejs.com/book/first-steps/animation-loop/#fixed-and-dynamic-frames
  useFrame((_, delta) => {
    r += 0 * delta;
  })

  const noteScale = 15;





  const note_collection = [
    {note: 0, label: "A", color: "gold"},
    {note: 3, label: "C", color: "gold"},
    {note: 6, label: "Eb", color: "gold"},
    {note: 9, label: "Gb", color: "gold"},
    {note: 1, label: "Bb", color: "firebrick"},
    {note: 4, label: "Db", color: "firebrick"},
    {note: 7, label: "E", color: "firebrick"},
    {note: 10, label: "G", color: "firebrick"},
    {note: 2, label: "B", color: "dodgerblue"},
    {note: 5, label: "D", color: "dodgerblue"},
    {note: 8, label: "F", color: "dodgerblue"},
    {note: 11, label: "Ab", color: "dodgerblue"}
  ]

  const notes = [
    {note: "C", color: "gold", position: [0, 0, 0]},
    {note: "Eb", color: "gold", position: [1, 0, 0]},
    {note: "Bb", color: "firebrick", position: [1, 1, 0]},
    {note: "G", color: "firebrick", position: [0, 1, 0]},
    {note: "A", color: "gold", position: [0, 0, 1]},
    {note: "Gb", color: "gold", position: [1, 0, 1]},
    {note: "Db", color: "firebrick", position: [1, 1, 1]},
    {note: "E", color: "firebrick", position: [0, 1, 1]},
    {note: "F", color: "dodgerblue", position: [-1, -1, -1]},
    {note: "Ab", color: "dodgerblue", position: [2, -1, -1]},
    {note: "F", color: "dodgerblue", position: [2, 2, -1]},
    {note: "D", color: "dodgerblue", position: [-1, 2, -1]},
    {note: "D", color: "dodgerblue", position: [-1, -1, 2]},
    {note: "B", color: "dodgerblue", position: [2, -1, 2]},
    {note: "Ab", color: "dodgerblue", position: [2, 2, 2]},
    {note: "B", color: "dodgerblue", position: [-1, 2, 2]},
  ];

const lines = [
  {name:"CG", color:"#D55E00", points: [[0, 0, 0], [0, 1*noteScale, 0]]},
  {name:"AE", color:"#D55E00", points: [[0, 0, 1*noteScale], [0, 1*noteScale, 1*noteScale]]},
  {name:"GbDb", color:"#D55E00", points: [[1*noteScale, 0, 1*noteScale], [1*noteScale, 1*noteScale, 1*noteScale]]},
  {name:"EbBb", color:"#D55E00", points: [[1*noteScale, 0, 0], [1*noteScale, 1*noteScale, 0]]},
  {name:"CA", color:"gold", points: [[0, 0, 0], [0, 0, 1*noteScale]]},
  {name:"AGb", color:"gold", points: [[1*noteScale, 0, 1*noteScale], [0, 0, 1*noteScale]]},
  {name:"GbDb", color:"gold", points: [[1*noteScale, 0, 1*noteScale], [1*noteScale, 0, 0]]},
  {name:"EbBb", color:"gold", points: [[0, 0, 0], [1*noteScale, 0, 0]]},
  {name:"CA", color:"firebrick", points: [[0, 1*noteScale, 0], [0, 1*noteScale, 1*noteScale]]},
  {name:"AGb", color:"firebrick", points: [[1*noteScale, 1*noteScale, 1*noteScale], [0, 1*noteScale, 1*noteScale]]},
  {name:"GbDb", color:"firebrick", points: [[1*noteScale, 1*noteScale, 1*noteScale], [1*noteScale, 1*noteScale, 0]]},
  {name:"EbBb", color:"firebrick", points: [[0, 1*noteScale, 0], [1*noteScale, 1*noteScale, 0]]},
    {name:"CA", color:"dodgerblue", points: [[-1*noteScale, -1*noteScale, -1*noteScale], [-1*noteScale, -1*noteScale, 2*noteScale]]},
  {name:"AGb", color:"dodgerblue", points: [[2*noteScale, -1*noteScale, 2*noteScale], [-1*noteScale, -1*noteScale, 2*noteScale]]},
  {name:"GbDb", color:"dodgerblue", points: [[2*noteScale, -1*noteScale, 2*noteScale], [2*noteScale, -1*noteScale, -1*noteScale]]},
  {name:"EbBb", color:"dodgerblue", points: [[-1*noteScale, -1*noteScale, -1*noteScale], [2*noteScale, -1*noteScale, -1*noteScale]]},
  {name:"CA", color:"dodgerblue", points: [[-1*noteScale, 2*noteScale, -1*noteScale], [-1*noteScale, 2*noteScale, 2*noteScale]]},
  {name:"AGb", color:"dodgerblue", points: [[2*noteScale, 2*noteScale, 2*noteScale], [-1*noteScale, 2*noteScale, 2*noteScale]]},
  {name:"GbDb", color:"dodgerblue", points: [[2*noteScale, 2*noteScale, 2*noteScale], [2*noteScale, 2*noteScale, -1*noteScale]]},
  {name:"EbBb", color:"dodgerblue", points: [[-1*noteScale, 2*noteScale, -1*noteScale], [2*noteScale, 2*noteScale, -1*noteScale]]},
  {name:"CG", color:"dodgerblue", points: [[-1*noteScale, -1*noteScale, -1*noteScale], [-1*noteScale, 2*noteScale, -1*noteScale]]},
  {name:"AE", color:"dodgerblue", points: [[-1*noteScale, -1*noteScale, 2*noteScale], [-1*noteScale, 2*noteScale, 2*noteScale]]},
  {name:"GbDb", color:"dodgerblue", points: [[2*noteScale, -1*noteScale, 2*noteScale], [2*noteScale, 2*noteScale, 2*noteScale]]},
  {name:"EbBb", color:"dodgerblue", points: [[2*noteScale, -1*noteScale, -1*noteScale], [2*noteScale, 2*noteScale, -1*noteScale]]},
  {name:"EbBb", color:"forestgreen", points: [[0, 0, 0], [-1*noteScale, -1*noteScale, -1*noteScale]]},
  {name:"EbBb", color:"forestgreen", points: [[1*noteScale, 0, 0], [2*noteScale, -1*noteScale, -1*noteScale]]},
  {name:"EbBb", color:"forestgreen", points: [[0, 0, 1*noteScale], [-1*noteScale, -1*noteScale, 2*noteScale]]},
  {name:"EbBb", color:"forestgreen", points: [[ 1*noteScale, 0, 1*noteScale], [2*noteScale, -1*noteScale, 2*noteScale]]},
    {name:"EbBb", color:"#612B8F", points: [[0, 1*noteScale, 0], [-1*noteScale, 2*noteScale, -1*noteScale]]},
  {name:"EbBb", color:"#612B8F", points: [[1*noteScale, 1*noteScale, 0], [2*noteScale, 2*noteScale, -1*noteScale]]},
  {name:"EbBb", color:"#612B8F", points: [[0, 1*noteScale, 1*noteScale], [-1*noteScale, 2*noteScale, 2*noteScale]]},
  {name:"EbBb", color:"#612B8F", points: [[ 1*noteScale, 1*noteScale, 1*noteScale], [2*noteScale, 2*noteScale, 2*noteScale]]}
]

const { camera } = useThrelte()
const scale = spring(1)
</script>



<PerspectiveCamera
  {position}
>
  <OrbitControls
  on:change={e=>{position=$camera.position}}
  >
  </OrbitControls>
</PerspectiveCamera>

<DirectionalLight />
<AmbientLight />

{#each lines as lin}
<Line2
  points={lin.points}
  material={new LineMaterial({
    color: lin.color,
    worldUnits: true,
    lineWidth: 0.4
  })}
/>
{/each}
{#each notes as note}
<Mesh 
  scale={$scale}
  geometry={new SphereGeometry(3)}
  material={new MeshStandardMaterial({color: note.color})}
  position={{ x: note.position[0]*noteScale, y:note.position[1]*noteScale, z:note.position[2]*noteScale }}
  rotation={{ y: r, z: r }}
  interactive
  on:pointerenter={() => ($scale = 1.5)}
	on:pointerleave={() => ($scale = 1)}
>

</Mesh>

<input type="text">
<Text 
text={note.note}
lookAt = {position}
color= {note.color}
fontSize = 9
scale= 4
position={{ x: note.position[0]*noteScale, y:note.position[1]*noteScale, z:note.position[2]*noteScale }}
>
</Text>
{/each}



