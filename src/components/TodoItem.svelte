<script>
  export let todo;
  export let toggleDone;
  export let deleteTodo;
</script>

<li>
  <input
    type="checkbox"
    checked={todo.checked}
    on:click={() => toggleDone(todo.id)} />
  <span class={todo.checked ? 'done' : ''}>{todo.text}</span>
  <button on:click={() => deleteTodo(todo.id)}>delete</button>
</li>

<style>
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 3px;
  }

  input {
    margin: 0;
  }

  button {
    margin: 0;
  }

  .done {
    text-decoration: line-through;
  }
</style>
