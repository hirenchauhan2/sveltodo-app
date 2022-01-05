<script>
  import { createEventDispatcher } from "svelte";

  export let filter = 1;

  const dispatch = createEventDispatcher();

  const onFilterChange = (event) => {
    const value = event.target.value;

    dispatch("filterChange", { filter: value });
  };
</script>

<div>
  <h4 class="text-lg font-semibold">Filters</h4>

  <div class="inline-flex flex-row items-center gap-2 border rounded text-xs">
    <label
      class="inline-block cursor-pointer p-2 {filter === 1
        ? 'font-semibold border bg-gray-200'
        : ''}"
    >
      <input
        type="radio"
        class="hidden"
        bind:group={filter}
        name="filter"
        value={1}
        on:change={onFilterChange}
      /> All
    </label>

    <label
      class="inline-block cursor-pointer p-2 {filter === 2
        ? 'font-semibold border bg-gray-200'
        : ''}"
    >
      <input
        type="radio"
        class="hidden"
        bind:group={filter}
        name="filter"
        value={2}
        on:change={onFilterChange}
      /> Active
    </label>

    <label
      class="inline-block cursor-pointer p-2 {filter === 3
        ? 'font-semibold border bg-gray-200'
        : ''}"
    >
      <input
        type="radio"
        class="hidden"
        bind:group={filter}
        name="filter"
        value={3}
        on:change={onFilterChange}
      /> Completed
    </label>
  </div>
</div>
