<script lang="ts">
  import RadioGroup from "./lib/RadioGroup.svelte";

  const methods = ["GET", "POST", "PUT", "PATCH", "DELETE"];
  const defaultHeaders = '{"Content-Type": "application-json"}';

  let method = "GET";
  function handleMethodChange(e) {
    method = e.target.value;
  }

  let address = "";
  function handleAddressInput(e) {
    address = e.target.value;
  }

  let reqHeaders = defaultHeaders;
  function handleHeaderInput(e) {
    reqHeaders = e.target.value;
  }

  let reqBody = "";
  function handleBodyInput(e) {
    reqBody = e.target.value;
  }

  let status;
  let results;
  async function handleSubmit(e) {
    e.preventDefault();
    try {
      let response;

      if (method === "GET") {
        response = await fetch(address);
      } else {
        response = await fetch(address, {
          method,
          body: reqBody,
          headers: JSON.parse(reqHeaders),
        });
      }
      status = response.status;

      try {
        const json = await response.json();
        results = json ? JSON.stringify(json) : null;
      } catch (error) {
        results = response.statusText;
      }
    } catch (error) {
      console.error(error);
      results = error.message;
    }
  }
</script>

<main>
  <div>
    <form on:submit={handleSubmit}>
      <RadioGroup
        radioGroupName="methods"
        radioNames={methods}
        selectedRadio={method}
        handleRadioChange={handleMethodChange}
      />

      <p>Address is {address}</p>
      <input value={address} on:input={handleAddressInput} />

      <p>Header input is {reqHeaders}</p>
      <textarea value={reqHeaders} on:input={handleHeaderInput} />

      <p>Body input is {reqBody}</p>
      <textarea value={reqBody} on:input={handleBodyInput} />

      <button type="submit">Submit</button>
    </form>
  </div>
  <div>
    {#if results}
      {#if status}
        {status}
      {/if}
      {results}
    {/if}
  </div>
</main>
