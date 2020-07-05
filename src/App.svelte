<script>
  export let name;
</script>

<h1>Hello, {name}</h1>

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
