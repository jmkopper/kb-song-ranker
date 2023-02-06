<script>
  function shuffle(array) {
    // Fisher-Yates shuffle
    let currentIndex = array.length,  randomIndex;
    while (currentIndex != 0) {
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex--;
      [array[currentIndex], array[randomIndex]] = [
        array[randomIndex], array[currentIndex]];
    }
    return array;
  }

  let kbSongs = [
    "Wuthering Heights",
    "The Man with the Child in His Eyes",
    "Hammer Horror",
    "Wow",
    "Breathing",
    "Babooshka",
    "Army Dreamers",
    "December Will Be Magic Again",
    "Sat in Your Lap",
    "The Dreaming",
    "There Goes a Tenner",
    "Running Up That Hill",
    "Cloudbusting",
    "Hounds of Love",
    "The Big Sky",
    "Don't Give Up",
    "Experiment IV",
    "The Sensual World",
    "This Woman's Work",
    "Love and Anger",
    "Rocket Man",
    "Rubberband Girl",
    "Moments of Pleasure",
    "The Red Shoes",
    "The Man I Love",
    "And So Is Love",
    "King of the Mountain",
    "Lyra",
    "Deeper Understanding",
  ];
  let toMerge = shuffle(kbSongs);
  let merged = [];
  let mergedFlag = false;
  let mergeDequeue = toMerge.map(e => [e]);
  let leftMergeSet = mergeDequeue.shift();
  let rightMergeSet = mergeDequeue.shift();

  function checkMerged() {
    if (leftMergeSet.length == 0 && rightMergeSet.length == 0 && mergeDequeue.length == 0) {
      mergedFlag = true;
    } else if (leftMergeSet.length == 0 && rightMergeSet.length == 0) {
      mergeDequeue.push(merged);
      merged = [];
      leftMergeSet = mergeDequeue.shift();
      rightMergeSet = mergeDequeue.shift();
      mergeDequeue = mergeDequeue;
    } else if (leftMergeSet.length == 0) {
      merged.push(rightMergeSet.pop());
      merged = merged;
      checkMerged();
    } else if (rightMergeSet.length == 0) {
      merged.push(leftMergeSet.pop());
      merged = merged;
      checkMerged();
    }
  }

  function merge(first) {
    if (first === "left") {
      merged.push(leftMergeSet.shift());
    } else {
      merged.push(rightMergeSet.shift());
    }
    leftMergeSet = leftMergeSet;
    rightMergeSet = rightMergeSet;
    merged = merged;
    checkMerged();
  }
</script>

{#if !mergedFlag}
  <h2>Which do you like better?</h2>
  <button on:click={() => merge("left")}>
    {leftMergeSet[0]}
  </button>
  <br />
  <br />
  <button on:click={() => merge("right")}>
    {rightMergeSet[0]}
  </button>
  {:else}
  <div style="display: inline-block; text-align: left;">
    <ol>
    {#each merged as m}
      <li>{m}</li>
    {/each}
    </ol>
  </div>
{/if}
