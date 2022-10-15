<script>
  let muted = true;
  let hidden = true;
  let paused = true;

  function createArray(n) {
    let toReturn = [];
    for (let i = 1; i <= n; i++) {
      toReturn.push(i);
    }
    return toReturn;
  }

  let vids = shuffle(createArray(27));
  console.log(vids);
  let index = 0;
  let showStartButton = true;
  $: vidSrc = `https://cowhca.github.io/mamba-stories/vid${vids[index]}.mp4`;

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
  class="text-5xl text-center rounded-sm bg-laker-gold text-laker-purple font-bold w-1/3 mx-auto p-2 mt-8"
>
  Mamba Stories
</h1>
<h2 class="text-xl text-white text-center my-4">
  Gain inspiration from stories about the Black Mamba
</h2>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="flex justify-center">
  <p
    id="start"
    on:click={() => {
      muted = false;
      hidden = false;
      paused = false;
      showStartButton = false;
    }}
    class="text-2xl text-black cursor-pointer hover:shadow-[4px_4px_0px_0px_rgba(34,197,94,0.3)] p-2 bg-green-500 inline rounded-md"
    class:hidden={!showStartButton}
  >
    Start
  </p>
  <p
    on:click={() => {
      muted = true;
      index++;
      muted = false;
    }}
    class="text-2xl text-black cursor-pointer hover:shadow-[4px_4px_0px_0px_rgba(34,197,94,0.3)] p-2 bg-green-500 inline rounded-md mb-2"
    class:hidden={showStartButton}
  >
    Random
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
  class="border-t border-l border-slate-600 rounded-tl text-gray-400 tracking-widest fixed right-0 bottom-0 flex flex-row items-center"
  href="https://connorcallahan.info"
>
  <img
    class="rounded-full h-8 m-2"
    src="https://cowhca.github.io/assets/profile_pic.png"
    alt="Me smiling"
  />
  <p class="text-sm pr-1">by Connor Callahan</p>
</a>
