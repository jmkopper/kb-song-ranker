<script>
  import Sorter from './Sorter.svelte'
  import {kbSongs} from './kbsongs.js';
</script>

<main>
  <h1>Kate Bush Song Ranker</h1>

  <div class="card">
    <Sorter list={kbSongs}/>
  </div>
</main>
