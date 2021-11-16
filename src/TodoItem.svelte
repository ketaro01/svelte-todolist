<script lang="ts">
  import { Card, Icon } from 'sveltestrap';

  export let todo;
  export let setTodo;
  export let removeTodo;
</script>

<Card class="mb-2">
  <div class="todo-item">
    <div class="todo-checkbox">
      <div
        class="{ todo.check ? 'active' : '' }"
        on:click={() => setTodo({ ...todo, check: !todo.check })}
      >
        <Icon
          name="check2"
        />
      </div>
    </div>
    <div class="todo-content">
      <div>{todo.title}</div>
    </div>
    <div class="todo-checkbox">
      <div class="trash" on:click={() => removeTodo(todo.id)}>
        <Icon
          name="trash"
        />
      </div>
    </div>
  </div>
</Card>

<style lang="scss">
  .todo-item {
    padding: 10px;
    display: flex;
    justify-content: center;
    .todo-content {
      width: 400px;
      text-align: left;
      padding: 0 10px;
    }
    .todo-checkbox {
      display: flex;
      align-items: center;
      > div {
        margin-right: 5px;
        cursor: pointer;
        color: #ddd;
        transition: all .3s;
        &.trash {
          color: #333;
        }
        &.active, &:hover {
          color: #333;
          font-weight: bold;
        }
      }
    }
  }
</style>
