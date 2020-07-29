<script>
  import { onMount } from 'svelte'
  export let profession
  // these automatically update when `time`
  // changes, because of the `$:` prefix
  let time = new Date()
  $: hours = time.getHours()
  $: minutes = time.getMinutes()
  $: seconds = time.getSeconds()
  onMount(() => {
    const interval = setInterval(() => {
      time = new Date()
    }, 1000)

    return () => {
      clearInterval(interval)
    }
  })
  let count = 0
  function increment() {
    count++
  }
</script>

<style>
  button {
    /* margin-left: 50%; */
    background-color: aqua;
  }
  svg {
    width: 100%;
    height: 100%;
  }

  .clock-face {
    stroke: #333;
    fill: white;
  }

  .minor {
    stroke: #999;
    stroke-width: 0.5;
  }

  .major {
    stroke: #333;
    stroke-width: 1;
  }

  .hour {
    stroke: #333;
  }

  .minute {
    stroke: #666;
  }

  .second,
  .second-counterweight {
    stroke: rgb(180, 0, 0);
  }

  .second-counterweight {
    stroke-width: 3;
  }
  my-tag {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    background-color: azure;
  }

  h2 {
    color: #ff3e00;
    text-transform: uppercase;
    /* font-size: 14px; */
    font-weight: 100;
  }

  @media (min-width: 640px) {
    my_tag {
      max-width: none;
    }
  }
</style>

<svg viewBox="-50 -50 100 100">
  <circle class="clock-face" r="48" />

  <!-- markers -->
  {#each [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55] as minute}
    <line class="major" y1="35" y2="45" transform="rotate({30 * minute})" />

    {#each [1, 2, 3, 4] as offset}
      <line
        class="minor"
        y1="42"
        y2="45"
        transform="rotate({6 * (minute + offset)})" />
    {/each}
  {/each}

  <!-- hour hand -->
  <line
    class="hour"
    y1="2"
    y2="-20"
    transform="rotate({30 * hours + minutes / 2})" />

  <!-- minute hand -->
  <line
    class="minute"
    y1="4"
    y2="-30"
    transform="rotate({6 * minutes + seconds / 10})" />

  <!-- second hand -->
  <g transform="rotate({6 * seconds})">
    <line class="second" y1="10" y2="-38" />
    <line class="second-counterweight" y1="10" y2="2" />
  </g>
</svg>
<my-tag>
  <h2>I work as a {profession}</h2>
  <button on:click={increment}>{count}</button>
</my-tag>
