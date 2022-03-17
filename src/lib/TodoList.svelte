<script>
  import TodoItem from "./TodoItem.svelte";

  export let todos = [];
</script>

<div
  class="w-1/2 mx-auto border border-zinc-800 rounded-lg mt-6 divide-y divide-zinc-800"
>
  {#each todos as todo (todo.id)}
    <TodoItem {todo} on:complete on:delete />
  {:else}
    <p class="p-4">No todos..!</p>
  {/each}
</div>
