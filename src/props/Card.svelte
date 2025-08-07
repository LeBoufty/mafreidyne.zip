<script lang="ts">
  let { title, children } = $props();
</script>

<div
  class="mx-auto max-w-sm gap-x-4 rounded-xl bg-zinc-800 p-4 shadow-xl outline-cyan-500 outline-4"
>
  <h2 class="text-center text-zinc-100 font-bold text-2xl">{title}</h2>
  <hr class="m-4 text-zinc-600" />
  <p class="text-justify text-zinc-200">
    {@render children()}
  </p>
</div>
