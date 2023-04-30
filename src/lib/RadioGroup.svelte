<script lang="ts">
  import RadioButton from "./RadioButton.svelte";

  export let radioGroupName: string;
  export let radioNames: string[];
  export let handleRadioChange: (e: Event) => unknown;
  export let selectedRadio: string;
</script>

<div>
  <p>Selected radio is {selectedRadio}</p>
  {#each radioNames as radioValue}
    <RadioButton
      labelText={radioValue}
      checked={radioValue === selectedRadio}
      {radioGroupName}
      {radioValue}
      {handleRadioChange}
    />
  {/each}
</div>
