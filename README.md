# Rails React Example

An example application build with Rails and React

### Questions

#### Updating State Doesn't Work When I Reassign an Object to an Existing Object

The `updateTodoItem` method in `app/javascript/packs/components/TodoApp.jsx` manually assigns the `title`, `complete` and `updated_at` values to the `todoItem` as seen below:

```
const { id, title, complete, updated_at } = todoItem
...
todoItems[todoItemIndex].title = title
todoItems[todoItemIndex].complete = complete
todoItems[todoItemIndex].updated_at = updated_at
```

However, I tried the following with no success:

```
todoItems[todoItemIndex] = { ...todoItem }
```

```
todoItems[todoItemIndex] = todoItem
```

```
this.setState(state => {
    todoItems: state.todoItems.map(item => {
        if (item.id === todoItem.id) {
            item = { ...todoItem }
        }
        return item
    })
})
```

This confuses me, because the following works as expected:

```
const people = [
    { name: 'steve', age: 29 },
    { name: 'linds', age: 30 },
]

const updatePerson = {
    name: 'steve',
    age: 30,
}

people[0] = updatePerson

console.log(people)
```

## Local Build

```
bundle install
yarn install
rails db:create
rails db:seed
rails s
```

## Tests

```
rspec
```

## Specs

```
rspec f -d
```

## To Do

-   [ ] Refactor `updateTodoItem`
-   [ ] Add ability to filter `complete` items
-   [ ] Only load the `<Spinner/>` if content is loading, not if `this.state.todoItems.length === 0`, since it's possible a user could have no items.
    -   Add a `loading` key into `state`
-   [ ] Write feature tests
-   [ ] Highlight invalid field elements
-   [ ] Consider using `axios` for better compatibility in `app/javascript/packs/components/TodoApp.jsx`
