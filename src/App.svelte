<script>
  import Input from "./Input.svelte";

  let logo = "./img/logo.png";
  let example = "./img/example.jpg";
  let icon = "./img/icon.png";
  let icon2x = "./img/icon2x.png";

  let label = "experimental";
  let file = example;
  let fileUrl = null;
</script>

<Input placeholder="Hello" bind:value={label} />

<style lang="scss">
  @font-face {
    font-family: "HN";
    src: local("HN"), local("Helvetica Neue Condensed Bold"),
      url("/fonts/Helvetica-Neue.ttf") format("truetype");
  }

  :global(body) {
    margin: 0;
    padding: 0;
  }

  :global(*) {
    margin: 0;
    padding: 0;
    user-select: none;
    outline: none;
  }

  h1 {
    color: $color;
    font-family: "HN", sans-serif;
  }
</style>
