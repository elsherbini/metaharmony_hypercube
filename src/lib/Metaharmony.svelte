<script>
  import { Note, Scale, Interval } from 'tonal';
  import { chromas, pcset } from "@tonaljs/pcset";
  import { transposeFrom } from "@tonaljs/note";

const diminished_square = (root) => {
    return [root, Note.transpose(root, "3m"), Note.transpose(root, "5d"), Note.transpose(root, "6M")]
  }

const get_squares = (root) => {
  return [diminished_square(Note.transpose(root, "4P")), diminished_square(root), diminished_square(Note.transpose(root, "5P")), diminished_square(Note.transpose(root, "2M"))]
}

</script>