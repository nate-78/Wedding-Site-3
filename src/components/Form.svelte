<script>
  import Input from "./Input.svelte";

  let name = '';
  let honeypotLastName = '';
  let emailOrCell = '';
  let attending = '';
  let numGuests = '';

  let showNumGuests = false;

  let showSubmitMsg = false;
  let successMessage = "Thanks for letting us know!";
  let errorMsg = "";


  function onInputChange(evt, field) {
    let v = evt.target.value;
    if (field == 'first-name') {
      name = v;
    } else if (field == 'last-name') {
      honeypotLastName = v;
    } else if (field == 'email-phone') {
      emailOrCell = v;
    } else if (field == 'num-guests') {
      numGuests = v;
    }
  }


  function onSelectChange(evt) {
    attending = evt.target.value;
    if (evt.target.value == 'yes') {
      showNumGuests = true;
    } else {
      showNumGuests = false;
    }
  }


  const submitForm = (event) => {
    event.preventDefault();
    
    // check honeypot 
    if (honeypotLastName != '') {
      console.log('honeypot triggered!', name, honeypotLastName, emailOrCell, attending, numGuests);
      return false; // don't send form 
    }

    let data = new FormData(event.target);
    console.log(data);
    fetch(event.target.action, {
      method: 'POST',
      body: data,
      headers: {
        'Accept': 'application/json'
      }
    }).then(response => {
      console.log(response);
      if (response.ok) {
        showSubmitMsg = true;
        errorMsg = "";
      } else {
        response.json().then(data => {
          if (Object.hasOwn(data, 'errors')) {
            errorMsg = data["errors"].map(error => error["message"]).join(", ")
          } else {
            errorMsg = "Oops! There was a problem submitting your form."
          }
        });
      }
    });
  };
</script>


<div id="rsvp">
  <hr />
  <h2>RSVP</h2>
  <div class="form">
    <!-- show success message if form has been submitted -->
    {#if showSubmitMsg}
      <div>
        <div class="center">
          <p>
            {successMessage}
          </p>
        </div>
      </div>
    {:else} <!-- the RSVP form -->
      <form on:submit={submitForm} action="https://formspree.io/f/mlezqnwl">
        <div class="form-control">
          <Input label="Name" fieldName="first-name" required="true" change={(e) => onInputChange(e, 'first-name')} />
        </div>
        <div class="form-control last-name">
          <label for="last-name">Last Name</label>
          <input type="text" name="last-name" id="last-name" change={(e) => onInputChange(e, 'last-name')} />  
        </div>
        <div class="form-control">
          <Input label="Email or Cell #" fieldName="email-phone" required="true" change={(e) => onInputChange(e, 'email-phone')} />
        </div>
        <div class="form-control">
          <select id="attending" name="attending" on:change={(e) => onSelectChange(e)}>
            <option value="">Will you be attending?</option>
            <option value="yes">Yes, I'll be there!</option>
            <option value="no">Sorry, can't make it.</option>
          </select>
        </div>
        {#if showNumGuests}
          <div class="form-control">
            <Input label="Number of Guests (including you!)" 
              fieldName="num-guests" required="true" 
              type="text" change={(e) => onInputChange(e, 'num-guests')} />
          </div>
        {/if}
        <div class="form-action">
          <button type="submit" class="btn">Submit</button>
        </div>

        {#if errorMsg != ""}
          <div class="row">
            <div class="col">
              <p class="error">
                {errorMsg}
              </p>
            </div>
          </div>
        {/if}
      </form>
    {/if}
    
  </div>
</div>


<style>
  hr {
    margin: 3rem auto;
    width: 90%;
    max-width: 260px;
    border: none;
    border-top: 3px solid var(--font-color-dark);
  }
  h2 {
    text-align: center;
  }
  .form {
    background: var(--white);
    border-radius: 3px;
    width: 100%;
    max-width: 570px;
    margin: auto;
    padding: 2rem 1rem;
  }
  .form-control {
    width: 100%;
    margin-bottom: 1.5rem;
  }
  .form-control.last-name {
    display: none; /* this is the honeypot ;) */
  }
  .form-action {
    margin-top: 3rem;
  }
  select {
    height: 50px;
    font-size: 1rem;
    width: 100%;
    border: none;
    border-bottom: 3px solid var(--font-color-dark);
    font-family: var(--font-sans);
  }

  .center {
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>