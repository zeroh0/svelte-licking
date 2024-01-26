<script>
  import { parse } from 'svelte/compiler';
  import TodoList from './TodoList.svelte';
  import { onMount } from 'svelte';

  let todos = [];
  let inputValue = '';

  onMount(() => {
		const localTodo = localStorage.getItem('todos');
    if (localTodo) {
      todos = JSON.parse(localTodo);
    }
	});

  /**
   * 할 일 추가
   */
  const addTodo = () => {
    if (!inputValue) return;
    todos = [{ id: todos.length + 1, title: inputValue, completed: false }, ...todos];
    localStorage.setItem('todos', JSON.stringify(todos));
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
</script>

<div class="ml-4 mr-4">
  <h2 class="text-2xl text-center mt-6">Todo List</h2>
  <p class="text-gray-400 text-center mt-1">할 일을 추가해보세용~</p>
  <div class="flex flex-row mt-10 h-9">
    <input class=" pl-1.5 basis-3/4 rounded border" type="text" bind:value={inputValue} on:keypress={handleAddTodo} />
    <button class="ml-4 bg-blue-600 text-white basis-1/4 rounded" type="button" on:click={addTodo}>Add</button>
  </div>
  <TodoList {todos} />
</div>
