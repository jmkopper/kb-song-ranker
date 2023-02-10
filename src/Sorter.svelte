<script>
  export let list;
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

  let toMerge = shuffle(list);
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
    {leftMergeSet[0].name}
  </button>
  <br />
  <br />
  <button on:click={() => merge("right")}>
    {rightMergeSet[0].name}
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
