In this mini project our team created a To-Do app server application. we have created 5 Rest APIs for add, delete, modify, get and mark todos done. I worked on the API which is used to modify the events in the application. 

~~~

var express = require('express');
var router = express.Router();

module.exports = (todos) => {
// PUT route to modify a to-do item
router.put('/', (req, res) => {
  const id = parseInt(req.body.id);
  console.log(id)

  const { task, completed } = req.body;

  // Find the to-do item in the array
  const index = todos.findIndex(todo => todo.id === id);

  // If the item doesn't exist, return an error
  if (index === -1) {
    return res.status(404).json({ error: 'To-do item not found' });
  }

  // Update the item with the new values
  todos[index].task = task || todos[index].task;
  todos[index].completed = completed !== undefined ? completed : todos[index].completed;

  // Return the updated to-do item
  res.json(todos[index]);
});
return router;
}

~~~

The router handles the PUT request to the root endpoint ('/') and expects a JSON payload in the request body with an 'id' field corresponding to the ID of the to-do item to be modified and 'task' and 'completed' fields corresponding to the new values for the to-do item.

The router then attempts to find the to-do item in the array by using the 'findIndex' method to search for the index of the to-do item with the given ID. If the item is not found, the router returns an error response with a 404 status code.

If the item is found, the router updates the 'task' and 'completed' fields of the to-do item with the new values provided in the request body, and then returns the updated to-do item in a JSON response.

A key learning from this code is the use of the findIndex method to locate an item in an array based on a predicate function. This method returns the index of the first element in the array that satisfies the predicate, or -1 if no element satisfies the predicate.

Challenge:

Consistent property naming and Error handling were the main challenges i faced and tried to resolve them but took lot of time.
