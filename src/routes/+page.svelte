<script lang="ts">
  import { onMount } from "svelte";
  import Card from "../props/Card.svelte";
  import FancyLink from "../props/FancyLink.svelte";

  let randomImg = $state();
  let randomImgID = $state();

  async function getRandomImg() {
    const response = await fetch(
      "https://danbooru.mafreidyne.zip/posts/random.json",
    );
    const data = await response.json();
    randomImg = data["preview_file_url"] as string;
    randomImgID = data["id"];
  }

  onMount(() => {
    getRandomImg();
  });
</script>

<div class="col-span-3 m-4">
  <h1 class="text-center text-mafreidyne font-black text-8xl m-4">
    mafreidyne.zip
  </h1>
  <h3 class="text-center text-zinc-400 italic font-bold text-2xl">
    Nuclear-powered freakhouse of fun
  </h3>
  <br />
  <Card title="Danbooru">
    <div class="flex items-center justify-center">
      <a href="https://danbooru.mafreidyne.zip/posts/{randomImgID}/">
        <img
          src={randomImg as string}
          alt="Random pic from danbooru.mafreidyne.zip"
          class="m-4"
        />
      </a>
    </div>
    <p class="text-zinc-50 text-justify">
      Find your new favorite Persona-themed stupid reaction pic from
      <bold class="font-bold">mafreidyne.zip</bold>'s own danbooru instance. No,
      this is not for gooning.
    </p>
    <div class="flex items-center justify-center m-2">
      <FancyLink
        title="danbooru.mafreidyne.zip"
        link="https://danbooru.mafreidyne.zip/"
      />
    </div>
    <p class="text-zinc-500 text-justify italic text-sm">
      I do not claim ownership or credit for any of the pictures hosted on the
      website, it is intended as a tool to easilly find pictures that else
      would've been found by the abhorrent search feature from Reddit.
    </p>
  </Card>
</div>
