<section class="intro">
  <div class="container">
    <div class="content">
      <div class="left">
        <img src="img/us/restaurant.jpg" alt="" />
        <div class="logo">
          <img src="img/L&N2.png" alt="Lindsay & Nathan" />
        </div>
      </div>
      <div class="right">
        
        <h1>
          <img src="img/L&N.png" alt="Lindsay & Nathan" />
        </h1>
        <p>
          We're getting married, y'all!
        </p>
        <a href="#rsvp" class="btn">RSVP</a>
      </div>
    </div>
  </div>
</section>


<style>
  .content {
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-template-columns: 3fr 2fr;
    grid-gap: 2rem;
    align-items: center;
  }
  .right {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    width: 100%;
    flex-direction: column;
  }
  .left img {
    height: 100%;
    width: 100%;
    object-fit: cover;
  }
  h1 {
    text-align: center;
  }
  p {
    font-family: var(--font-serif);
    font-size: 24px;
  }

  .logo {
    display: none;
  }

  @media (max-width: 767px) {
    .content {
      grid-template-columns: 1fr;
    }
    .logo {
      display: flex;
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      padding: 0 15%;
      justify-content: center;
    }

    h1 {
      display: none;
    }
  }
</style>