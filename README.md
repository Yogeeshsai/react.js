# react.js
It is a internship assignment

Here's a basic implementation of the described To-Do application using ReactJS and Redux:

jsx
Copy code
// App.js
import React from 'react';
import TaskInput from './TaskInput';
import TaskList from './TaskList';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>To-Do Application</h1>
      <TaskInput />
      <TaskList />
    </div>
  );
}

export default App;
jsx
Copy code
// TaskInput.js
import React, { useState } from 'react';
import { useDispatch } from 'react-redux';
import { addTask } from './redux/actions';

const TaskInput = () => {
  const [task, setTask] = useState('');
  const dispatch = useDispatch();

  const handleChange = (e) => {
    setTask(e.target.value);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (task.trim()) {
      dispatch(addTask(task));
      setTask('');
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={task} onChange={handleChange} placeholder="Add a task" />
      <button type="submit">Add</button>
    </form>
  );
};

export default TaskInput;
jsx
Copy code
// TaskList.js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { deleteTask } from './redux/actions';

const TaskList = () => {
  const tasks = useSelector(state => state.tasks);
  const dispatch = useDispatch();

  const handleDelete = (taskId) => {
    dispatch(deleteTask(taskId));
  };

  return (
    <ul>
      {tasks.map(task => (
        <li key={task.id}>
          {task.text}
          <button onClick={() => handleDelete(task.id)}>Delete</button>
        </li>
      ))}
    </ul>
  );
};

export default TaskList;
javascript
Copy code
// redux/actions.js
export const addTask = (text) => ({
  type: 'ADD_TASK',
  payload: {
    id: Math.random().toString(36).substr(2, 9), // Generate unique ID
    text
  }
});

export const deleteTask = (id) => ({
  type: 'DELETE_TASK',
  payload: id
});
javascript
Copy code
// redux/reducers.js
const initialState = {
  tasks: []
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case 'ADD_TASK':
      return {
        ...state,
        tasks: [...state.tasks, action.payload]
      };
    case 'DELETE_TASK':
      return {
        ...state,
        tasks: state.tasks.filter(task => task.id !== action.payload)
      };
    default:
      return state;
  }
};

export default reducer;
javascript
Copy code
// redux/store.js
import { createStore } from 'redux';
import reducer from './reducers';

const store = createStore(reducer);

export default store;
css
Copy code
/* App.css */
.App {
  text-align: center;
  margin-top: 50px;
}

form {
  margin-bottom: 20px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}

button {
  margin-left: 10px;
}
This code creates a simple To-Do application using ReactJS and Redux. Users can add tasks using the input field and delete tasks by clicking on the delete button. The state management is handled using Redux.
