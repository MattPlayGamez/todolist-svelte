<script>
  let todos = [];
  let item;
  const getStorage = JSON.parse(localStorage.getItem('todos'))
  console.log(getStorage)
  if(getStorage) {
    todos = getStorage
  } 
  function RemoveATodo(id) {
    const filtered = todos.filter((todo) => todo.id !== id)
    console.log(filtered)
    todos = [...filtered]
  }
  $:  {
    localStorage.setItem('todos', JSON.stringify(todos))
  }
</script>

<main>
  <div name="list">
    <ul>
      {#each todos as todo}
        <li>
          <h2>{todo.text}</h2>
          <button on:click={RemoveATodo(todo.id)}>Remove</button>
        </li>
      {/each}
    </ul>
    <input type="text" placeholder="enter an item" bind:value={item} />
    <button
      on:click={() => todos = [{ text: item, id: Math.round(Math.random() * 1000) }, ...todos]}>Add another one</button>
  </div>
</main>

<style></style>
