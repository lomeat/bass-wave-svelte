<script>
  import Input from "./Input.svelte";

  let logo = "./img/logo.png";
  let example = "./img/example.jpg";
  let icon = "./img/icon.png";
  let icon2x = "./img/icon2x.png";

  let label = "experimental";
  let file = example;
  let fileUrl = null;

  const uploadImage = e => {
    const reader = new FileReader();
    const newFile = e.target.files[0];

    reader.onloadend = () => {
      file = newFile;
      fileUrl = reader.result;
    };

    reader.readAsDataURL(newFile);
  };

  const downloadImage = () => {
    const canvas = document.createElement("canvas");
    const ctx = canvas.getContext("2d");
    canvas.width = 1920;
    canvas.height = 1080;

    const backImg = new Image();
    backImg.src = fileUrl ? fileUrl : file;
    backImg.onload = () => {
      ctx.drawImage(backImg, 0, 0, canvas.width, canvas.height);

      ctx.fillStyle = "rgba(0, 0, 0, 0.5)";
      ctx.fillRect(0, 934, 1920, 166);

      ctx.fillStyle = "white";
      ctx.font = "bold 90px HN";
      ctx.fillText(label.toUpperCase(), 32, 1040);
    };

    const iconImg = new Image();
    iconImg.src = icon2x;
    iconImg.onload = () => {
      ctx.drawImage(iconImg, 1560, 890, 351, 237);

      const link = document.createElement("a");
      link.download = "bass-wave.jpg";
      link.href = canvas.toDataURL("image/jpg");
      link.click();
    };
  };
</script>

<Input placeholder="Label name..." bind:value={label} />
{#if fileUrl}
  <img style="width: 200px;" src={fileUrl} />
{:else}
  <img src={file} style="width: 200px;" />
{/if}
<label>
  Upload
  <input
    style="display: none;"
    accept="image/*"
    type="file"
    on:change|preventDefault={e => uploadImage(e)} />
</label>
<button on:click={downloadImage}>Download</button>

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
