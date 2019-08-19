<script>
  import TodosList from "./TodosList.svelte";

  let todoItems = [];
  let newTodo = "";

  const addTodo = () => {
    newTodo = newTodo.trim();
    if (!newTodo || todoItems.find(item => item.text === newTodo)) {
      return;
    }

    const todo = {
      text: newTodo,
      checked: false,
      id: Date.now()
    };

    todoItems = [...todoItems, todo];
    newTodo = "";
  };

  const toggleDone = id => {
    const index = todoItems.findIndex(item => item.id === Number(id));
    todoItems[index].checked = !todoItems[index].checked;
  };

  const deleteTodo = id => {
    todoItems = todoItems.filter(item => item.id !== Number(id));
  };
</script>

<div>
  <TodosList
    {todoItems}
    {addTodo}
    {toggleDone}
    {deleteTodo}
    bind:newTodo />
</div>
