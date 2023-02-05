<script>
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
    "Cloudbursting",
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
  let count = 0
  const increment = () => {
    count += 1
  }

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
</script>

<button on:click={increment}>
  count is {count}
</button>
