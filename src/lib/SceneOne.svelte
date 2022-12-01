<script>
  import {
    PerspectiveCamera,
    DirectionalLight,
    AmbientLight,
    Mesh,
    useFrame,
    Object3DInstance,
    OrbitControls
  } from '@threlte/core';
  import {
    MeshStandardMaterial,
    CylinderGeometry,
    SphereGeometry,
    GridHelper,
    AxesHelper
  } from 'three';
  import { tweened } from 'svelte/motion';
  import { Note, Scale, Interval } from 'tonal';
  import { chromas, pcset } from "@tonaljs/pcset";
  import { transposeFrom } from "@tonaljs/note";
  import {
    Text
  } from '@threlte/extras'

  const t = tweened(3, { duration: 2000 });
  let r = 0;
  export let cameraPosition = { x: -100, y: 5, z: -100 }

  // Use delta to ensure motion is consistent at any frame rate
  // Learn more: https://discoverthreejs.com/book/first-steps/animation-loop/#fixed-and-dynamic-frames
  useFrame((_, delta) => {
    r += 0 * delta;
  })

  const noteScale = 15;
  const my_names = [0, 1, 2, 3, 4,5,6,7,8].map(Interval.fromSemitones);
  const my_note = Note.transpose("C", "3m");
  console.log(my_note);

  const diminished_square = (root) => {
    return [root, Note.transpose(root, "3m"), Note.transpose(root, "5d"), Note.transpose(root, "6M")]
  }

const get_squares = (root) => {
  return [diminished_square(Note.transpose(root, "4P")), diminished_square(root), diminished_square(Note.transpose(root, "5P")), diminished_square(Note.transpose(root, "2M"))]
}


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
    {note: "B", color: "dodgerblue", position: [2, 2, -1]},
    {note: "D", color: "dodgerblue", position: [-1, 2, -1]},
    {note: "D", color: "dodgerblue", position: [-1, -1, 2]},
    {note: "B", color: "dodgerblue", position: [2, -1, 2]},
    {note: "Ab", color: "dodgerblue", position: [2, 2, 2]},
    {note: "B", color: "dodgerblue", position: [-1, 2, 2]},
  ];

const cyls = [
  {}
]
</script>



<PerspectiveCamera
  position={cameraPosition}
  lookAt={{ x:0, y: 0, z: 0 }}
>
  <OrbitControls />
</PerspectiveCamera>

<DirectionalLight />
<AmbientLight />

<Mesh 
  geometry={new CylinderGeometry(1,1,20,24)}
  material={new MeshStandardMaterial({color: 'grey'})}
  position={{ x: $t, y: 10 }}
  rotation={{ y: r, z: r }}
  interactive
>
</Mesh>


{#each notes as note}
<Mesh 
  geometry={new SphereGeometry(3)}
  material={new MeshStandardMaterial({color: note.color})}
  position={{ x: note.position[0]*noteScale, y:note.position[1]*noteScale, z:note.position[2]*noteScale }}
  rotation={{ y: r, z: r }}
  interactive
>
</Mesh>

<input type="text">
<Text 
text={note.note}
lookAt = bind:cameraPosition
outlineColor= "black"
fontSize = 12
scale= 5
position={{ x: note.position[0]*noteScale, y:note.position[1]*noteScale, z:note.position[2]*noteScale }}
>
</Text>
{/each}
