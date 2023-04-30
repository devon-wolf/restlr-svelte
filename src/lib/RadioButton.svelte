<script lang="ts">
  export let labelText: string;
  export let radioGroupName: string;
  export let radioValue: string;
  export let handleRadioChange: (e: Event) => unknown;
  export let checked: boolean;
</script>

<label>
  <input
    type="radio"
    name={radioGroupName}
    value={radioValue}
    {checked}
    on:change={handleRadioChange}
  />
  <span>{labelText}</span>
</label>
