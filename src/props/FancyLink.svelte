<script lang="ts">
  let { title, link } = $props();
</script>

<a
  class="max-w-sm gap-x-4 rounded-xl bg-gradient-to-r from-cyan-500 to-fuchsia-500 p-4 shadow-xl hover:bg-gradient-to-r hover:from-cyan-600 hover:to-fuchsia-600"
  href={link}
>
  <h2 class="text-center text-zinc-100 font-bold text-2xl">{title}</h2>
</a>
