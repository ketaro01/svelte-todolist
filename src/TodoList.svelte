<script lang="ts">
  import TodoItem from './TodoItem.svelte';
  import _ from 'lodash';
  import { Button, Icon, Input, Label } from 'sveltestrap';

  type TodoType = {
    id: number;
    title: string;
    check: boolean;
  }
  let hideComplete = false;
  let modalOpen = false;
  let todoTitle = '';
  let todoItems: TodoType[] = [];
  // let todoItems: TodoType[] = Array.from(Array(10)).map((_, index) => ({
  //   id: index,
  //   title: `title_${index}`,
  //   check: false,
  // }));
  const setTodo = (todo) => {
    let nextTodoItems = _.cloneDeep(todoItems);
    const idx = nextTodoItems.findIndex((item) => item.id === todo.id);
    nextTodoItems.splice(idx, 1, todo);
    todoItems = nextTodoItems;
  }
  const removeTodo = (todoId) => {
    let nextTodoItems = _.cloneDeep(todoItems);
    const idx = nextTodoItems.findIndex((item) => item.id === todoId);
    nextTodoItems.splice(idx, 1);
    todoItems = nextTodoItems;
  }
  const submit= () => {
    if (!todoTitle) return;
    const id = Math.max(-1, ...todoItems.map((item) => item.id));
    // 이게 정상적인 push 에 대한 패턴이라함..
    todoItems.push({
      id: id + 1,
      title: todoTitle,
      check: false,
    });
    todoItems = todoItems;
    todoTitle = '';
  }
</script>

<div class="todo-main">
  <h2>Todo List</h2>
  <div class="backyard"></div>
  <div class="add-todo">
    <Input
      type="text"
      placeholder="내용을 입력해 주세요."
      bind:value={todoTitle}
    />
    &nbsp;
    <Button on:click={submit}>
      <Icon name="plus"/>
    </Button>
  </div>
  <div>
    {#each todoItems as todo, i}
      {#if !hideComplete || (hideComplete && !todo.check)}
        <TodoItem todo={todo} setTodo={setTodo} removeTodo={removeTodo} />
      {/if}
    {/each}
  </div>
  <div class="hide-complete form-inline">
    <Label for="hideComplete">완료된 Todo 숨기기&nbsp;</Label>
    <Input
      type="checkbox"
      class="inline-block"
      id="hideComplete"
      name="hideComplete"
      bind:checked={hideComplete}
    />
  </div>
</div>

<style lang="scss">
  .add-todo {
    display: flex;
    margin: 10px 0;
  }
  .todo-main {
    position: relative;
    width: 500px;
    border-radius: 7px;
    .backyard {
      z-index: -1;
      position: absolute;
      background-color: #eee;
      height: 22px;
      width: 130px;
      top: 20px;
      left: calc(50% - 50px);
    }
    .hide-complete {
      display: flex;
      justify-content: right;
      font-size: 12px;
      h5 {
        font-weight: 600;
        margin: 5px 0;
      }
    }
  }
</style>
