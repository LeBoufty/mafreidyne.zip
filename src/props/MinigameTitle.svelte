<script lang="ts">
  import { scale } from "svelte/transition";
  import { cubicOut } from "svelte/easing";

  const transitionConfig = { duration: 300, easing: cubicOut, start: 200 };

  let { title } = $props();
  let visible = $state(false);
  setTimeout(() => {
    visible = true;
  }, 1);
  setTimeout(() => {
    transitionConfig.start = 0;
    visible = false;
  }, 1000);
</script>

{#key title}
  {#if visible}
    <h2
      class="text-minigame-title text-4xl"
      transition:scale={transitionConfig}
    >
      {title}
    </h2>
  {/if}
{/key}
