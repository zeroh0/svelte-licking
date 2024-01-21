<script>
  export let todos = [];

  /**
   * 완료 상태 변경
   * @param selectedTodo
   */
  const changeCompleted = (selectedTodo) => {
    console.log(selectedTodo);
    todos = todos.map((todo) => {
      if (todo.id === selectedTodo.id) {
        todo.completed = !selectedTodo.completed;
      }
      return todo;
    });
  };

  const deleteTodo = (selectedTodo) => {
    todos = todos.filter((todo) => todo.id != selectedTodo.id);
  };
</script>

<ul class="flex flex-col mt-12">
  {#each todos as todo}
    <li class="list-none flex flex-row mb-2 items-center">
      <input
        class="size-5"
        type="checkbox"
        id={todo.id}
        checked={todo.completed}
        on:change={() => changeCompleted(todo)}
      />
      <label for={todo.id} class="{todo.completed ? 'line-through' : 'no-underline'} text-xl grow pl-2"
        >{todo.title}</label
      >
      <button on:click={() => deleteTodo(todo)}>❌</button>
    </li>
  {/each}
</ul>
