<div class="details">
  <div class="container">
    <h2>The Details</h2>
    <div class="content">
      <div>
        <h3>When</h3>
        <div class="img top">
          <img src="img/us/bourbon-street.jpg" alt="" />
        </div>
        <p>
          September 3, 2022<br />
          5 - 8pm
        </p>
      </div>
      <div>
        <h3>Where</h3>
        <div class="img">
          <img src="img/east-west.jpg" alt="" />
        </div>
        <p>
          East West <br />
          2306 2nd Ave N <br />
          Birmingham, AL 35203
        </p>
      </div>
    </div>
  </div>
</div>


<style>
  h2, h3, p {
    text-align: center;
  }
  .content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 2rem;
  }

  .content > div {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
  }

  .content .img {
    height: 180px;
    width: 180px;
    border-radius: 100%;
    overflow: hidden;
  }
  .content .img img {
    height: 100%;
    width: 100%;
    object-fit: cover;
  }
  .content .img.top img {
    object-position: top;
  }

  @media (max-width: 600px) {
    .content {
      grid-template-columns: 1fr;
    }
  }
</style>