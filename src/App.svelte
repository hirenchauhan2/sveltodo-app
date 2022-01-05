<script>
  import TodoList from './lib/TodoList.svelte';
  import TodoListFilters from './lib/TodoListFilters.svelte';

  // reactivity in Svelte works by re-assigning something to the variables
  // and that way Svelte knows how to update the dom or other variables which
  // are rectively watching its updates.
  // hence we declare variables using `let`.
  let todoText = '';
  let todos = [
    {
      id: 3,
      name: 'Learn React',
      completed: true,
    },
    {
      id: 2,
      name: 'Learn Svelte',
      completed: false,
    },
  ];
  let activeFilter = 1;

  /**
   * @param {KeyboardEvent} event keyboard event
   **/
  const handleKeyDown = (event) => {
    if (event.key === 'Enter') {
      handleAddTodo();
      return;
    }
  };

  const handleAddTodo = () => {
    const newTodo = {
      id: todos.length + 1,
      name: todoText,
      completed: false,
    };
    // need to re-assign the array as push method will not
    // trigger any update on UI
    todos = todos.concat([newTodo]);
    todoText = '';
  };

  const handleToggleTodo = (event) => {
    const todoId = event.detail.id;

    todos = todos.map((todo) => {
      if (todo.id === todoId) {
        return {
          ...todo,
          completed: !todo.completed,
        };
      }
      return todo;
    });
  };

  const handleDeleteTodo = (event) => {
    const todoId = event.detail.id;
    todos = todos.filter((todo) => todo.id !== todoId);
  };

  const handleFilterChange = (event) => {
    const filter = parseInt(event.detail.filter, 10);
    activeFilter = filter;
  };

  // reactive block to calculate the filtered todos
  // based on todos, active filter
  $: filteredTodos = todos.filter((todo) => {
    // all todos
    if (activeFilter === 1) {
      return true;
    }
    // active todos
    if (activeFilter === 2) {
      return !todo.completed;
    }
    // completed todos
    if (activeFilter === 3) {
      return todo.completed;
    }
  });
</script>

<main class="w-screen h-screen flex flex-col bg-slate-100 p-10">
  <h1
    class="text-6xl font-bold text-center text-slate-800 mb-10 underline decoration-wavy underline-offset-8"
  >
    Todo List
  </h1>

  <input
    class="w-5/6 p-4 text-lg lg:text-3xl rounded-md my-6 mx-auto bg-white
    border-none shadow-lg shadow-slate-100 outline-none transition duration-200
    ease-in-out focus:ring-2 focus:ring-zinc-500 focus:ring-offset-2"
    type="text"
    placeholder="Write down your todo"
    bind:value={todoText}
    on:keyup={handleKeyDown}
  />

  <div class="w-1/2 mx-auto flex flex-row items-end justify-between">
    <TodoListFilters filter={activeFilter} on:filterChange={handleFilterChange} />

    <p>{filteredTodos.length} items left</p>
  </div>

  <TodoList todos={filteredTodos} on:complete={handleToggleTodo} on:delete={handleDeleteTodo} />

  <footer class="text-center mt-auto">
    Using Svelte, made with <span role="img" aria-label="love">❤️</span> from
    <span role="img" aria-label="India">🇮🇳</span>
  </footer>
</main>

<style>
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>
