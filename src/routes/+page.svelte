<script>
  let muted = true;
  let hidden = true;
  let paused = true;
  const numVids = 26;
  let index = 0;
  let vids = shuffle(createArray(numVids));
  console.log(vids);
  $: vidSrc = `https://cowhca.github.io/mamba-stories/vid${vids[index]}.mp4`;
  let start = true;

  function createArray(n) {
    let toReturn = [];
    for (let i = 1; i <= n; i++) {
      toReturn.push(i);
    }
    return toReturn;
  }

  function shuffle(array) {
    let currentIndex = array.length,
      randomIndex;

    // While there remain elements to shuffle.
    while (currentIndex != 0) {
      // Pick a remaining element.
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex--;

      // And swap it with the current element.
      [array[currentIndex], array[randomIndex]] = [
        array[randomIndex],
        array[currentIndex],
      ];
    }

    return array;
  }
</script>

<h1
  class="text-2xl sm:text-5xl text-center rounded-sm bg-laker-gold text-laker-purple font-bold w-2/3 sm:w-1/3 mx-auto p-2 mt-8"
>
  Mamba Stories
</h1>
<h2 class="text-md sm:text-xl text-white text-center my-4">
  Inspiration from stories about the Kobe Bryant
</h2>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="flex justify-center">
  <p
    id="inspire"
    on:click={() => {
      if (start) {
        muted = false;
        hidden = false;
        paused = false;
        start = false;
      } else {
        muted = true;
        index = (index + 1) % numVids;
        muted = false;
      }
    }}
    class="text-2xl text-black cursor-pointer hover:shadow-[4px_4px_0px_0px_rgba(34,197,94,0.3)] p-2 bg-green-500 inline rounded-md mb-2"
  >
    Inspire
  </p>
</div>
{#key vidSrc}
  <video
    class="h-[70vh] w-auto mx-auto"
    bind:paused
    class:hidden
    autoplay
    controls
    bind:muted
    loop
  >
    <source src={vidSrc} />
    <track kind="captions" />
  </video>
{/key}
<!-- <a
  href="https://connorcallahan.info"
  class="fixed text-white bottom-0 right-0 p-2 bg-slate-800 rounded-tl-md"
>
  <img src="https://cowhca.github.io/assets/profile_pic.png" alt="profile" />
  by Connor Callahan
</a> -->

<a
  target="_blank"
  rel="noopener"
  class="border-t border-l border-slate-600 rounded-tl text-gray-400 tracking-tighter sm:tracking-widest fixed right-0 bottom-0 flex flex-row items-center"
  href="https://connorcallahan.info"
>
  <img
    class="rounded-full h-6 sm:h-8 m-2"
    src="https://cowhca.github.io/assets/profile_pic.png"
    alt="Me smiling"
  />
  <p class="hidden sm:block text-sm pr-1">by Connor Callahan</p>
</a>
