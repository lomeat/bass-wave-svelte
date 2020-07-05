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

<!-- <Input placeholder="Label name..." bind:value={label} />
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
<button on:click={downloadImage}>Download</button> -->

<div class="container">
  <img src={logo} alt="logo" class="logo" />
  <div class="wrapper">
    <div class="input-wrapper">
      <Input bind:value={label} placeholder="Label name..." />
    </div>
    <div class="image-wrapper">
      {#if fileUrl}
        <img class="image-background" alt="img" src={fileUrl} />
      {:else}
        <img class="image-background" alt="img" src={file} />
      {/if}
      <div class="image-label">
        {label}
        <img src={icon} alt="icon" class="image-icon" />
      </div>
    </div>
    <div class="button-wrapper">
      <label class="upload">
        Upload
        <input
          style="display:none;"
          accept="image/*"
          type="file"
          on:change|preventDefault={e => uploadImage(e)} />
      </label>
      <button class="download" on:click={downloadImage}>Download</button>
    </div>
  </div>
</div>

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
    box-sizing: border-box;
  }

  .container {
    width: 720px;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 70px auto 0 auto;

    @media (max-width: 760px) {
      width: 300px;
    }
  }

  img.logo {
    @media (max-width: 760px) {
      width: 50vw;
    }
  }

  .input-wrapper {
    display: flex;
    justify-content: space-between;
    padding-top: 60px;
    @media (max-width: 760px) {
      flex-direction: column;
    }
  }

  .image-wrapper {
    margin: 32px 0;
    position: relative;
  }

  img.image-background {
    width: 100%;
    border: 0;
    background-color: #69b4e6;
    margin: 0;
    padding: 0;
  }

  .image-label {
    color: white;
    font-size: 32px;
    width: 100%;
    box-sizing: border-box;
    font-family: "HN", sans-serif;
    font-weight: 600;
    text-transform: uppercase;
    padding: 10px 18px;
    position: absolute;
    bottom: 4px;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
    @media (max-width: 760px) {
      font-size: 4vw;
      padding: 2vw 2.3vw;
    }
  }

  img.image-icon {
    position: absolute;
    top: -16px;
    left: 582px;
    @media (max-width: 760px) {
      top: -25%;
      left: 78%;
      width: 20vw;
    }
  }

  .button-wrapper {
    display: flex;
    justify-content: space-between;
  }

  label.upload {
    background: #69b4e6;
    padding: 13px 32px;
    border-radius: 10px;
    border: 0;
    color: white;
    font-family: "Roboto Medium", sans-serif;
    font-size: 20px;
    outline: none;
    transition: 0.1s ease;
    cursor: pointer;
    &:hover {
      background: #5492bb;
    }
  }

  button.download {
    background: #69b4e6;
    padding: 13px 32px;
    border-radius: 10px;
    border: 0;
    color: white;
    margin: 0;
    font-family: "Roboto Medium", sans-serif;
    font-size: 20px;
    outline: none;
    transition: 0.1s ease;
    cursor: pointer;
    &:hover {
      background: #5492bb;
    }
  }
</style>
