<script>
  export let name;
</script>

<h1>Hello, {name}</h1>

<style lang="scss">
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
  }
</style>
