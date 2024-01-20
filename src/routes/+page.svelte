<script>
  let todos = [];
  let inputValue = '';

  /**
   * 할 일 추가
   */
  const addTodo = () => {
    if (!inputValue) return;
    todos = [{ id: todos.length + 1, title: inputValue, completed: false }, ...todos];
    inputValue = '';
  };

  /**
   * Enter 입력으로 할 일 추가
   * @param e
   */
  const handleAddTodo = (e) => {
    if (e.key === 'Enter') {
      addTodo();
    }
  };

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

<div class="ml-4 mr-4">
  <h2 class="text-2xl text-center mt-6">Todo List</h2>
  <p class="text-gray-400 text-center mt-1">할 일을 추가해보세용~</p>
  <div class="flex flex-row mt-10 h-9">
    <input class=" pl-1.5 basis-3/4 rounded border" type="text" bind:value={inputValue} on:keypress={handleAddTodo} />
    <button class="ml-4 bg-blue-600 text-white basis-1/4 rounded" type="button" on:click={addTodo}>Add</button>
  </div>

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
</div>
