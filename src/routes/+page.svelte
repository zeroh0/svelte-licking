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

<h2>Todo List</h2>

<input type="text" bind:value={inputValue} on:keypress={handleAddTodo} />
<button type="button" on:click={addTodo}>Add</button>

<ul>
  {#each todos as todo}
    <li style="list-style: none;">
      <input type="checkbox" id={todo.id} checked={todo.completed} on:change={() => changeCompleted(todo)} />
      <label for={todo.id} style="text-decoration: {todo.completed ? 'line-through' : 'none'}">{todo.title}</label>
      <button on:click={() => deleteTodo(todo)}>❌</button>
    </li>
  {/each}
</ul>
