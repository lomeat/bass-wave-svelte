<script>
  export let placeholder;
  export let value;
</script>

<input {placeholder} bind:value />

<style lang="scss">
  input {
    width: 320px;
    box-sizing: border-box;
    padding: 10px 16px;
    border: 1px solid #c0e1f6;
    outline: none;
    border-radius: 10px;
    font-size: 18px;
    font-family: "Roboto Regular", sans-serif;
    transition: 0.2s ease;
    text-transform: uppercase;

    &:focus {
      border: 1px solid #58a7dc;
    }

    &:focus + #modal {
      display: block;
    }

    @media (max-width: 760px) {
      width: 95vw;
      margin-top: 20px;
    }
  }
</style>
