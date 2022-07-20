<script>
  export let cssClass = '';
</script>

<div class={`border ${cssClass}`}>
  <img src="img/wildflowers.jpg" alt="" />
  <div class="overlay"></div>
</div>

<style>
  .border {
    height: 115px;
    margin: 2rem 0 3rem;
    width: 100%;
    position: relative;
  }
  .border.mb-0 {
    margin-bottom: 0;
  }
  .border img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    background: rgba(255,255,255,.3);
  }

  .border::before {
    position: absolute;
    content: '';
    width: 100%;
    height: 40px;
    top: 0;
    left: 0;
    background-image: linear-gradient(to bottom, white, transparent);
  }
</style>