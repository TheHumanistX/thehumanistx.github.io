Ok, I have a more difficult project I am starting. The project will be a webapp todo-list coded in React.

I am basing the measurements below on a 1900px width by 1200px height area. The entire app will be about 23px away from the top and bottom edges of the workspace and 34px away from the left and right edges of the workspace.

Here I will list out what piece or components the todo-list will be comprised of:

-On the left side of the workspace, there will be a 'Lists' component which runs about 1155px height and 410px width. It is tall enough that nothing can fit above or below it. 
    - This will hold all of the various todo task lists such as 'errands', 'yardwork', 'home chores', etc.  
    - Easy of these will be represented by a small card that has a rough height of 115px and rough width of 380px.  
    - Each of these cards will contain the following information:
        - Task list name in the top left
        - Number of tasks in list in the top right
        - {number of tasks complete} of {total number of tasks} (i.e. '8 of 10 Tasks Complete') below the task list name with some vertical space between them.
        - Task list completion progress bare below that
        - On the far right, below the Number of Tasks in list in the top right, but also centered vertically, will be three vertical dots which user clicks/taps to display a small menu that gives options to Edit tasks list, Delete Task List, maybe other options but definitely those two.
    - On the bottom right on the Lists component will be a small round button with a little + in it which you click or tap to add a new task list to the component.
        - When that button is clicked, a small modal will pop up asking you to input the name of the task list (that's all we need to create a new task list, just a title)

Everything else will be to the right of that tall task lists component.


Across the very top we will have:

-  To the right of the 'task lists component', there will be a header bar that is about 1080px wide and 55px tall. It will be about 30px to the right of the 'task lists' component and aligned vertically with the top of that component.
    - This header bar will display three pieces of information. 
        - On the very left, it will display 'List: {name of current task list that is open/selected}'.
        - In the middle of the bar it will display 'Tasks Completed: {# tasks completed} of {# tasks in current task list}'. 
        - On the far right of the bar it will display 'Date: {current date in Mo. Day, Year form}'

- About 30px to the right of that header bar will be a Wallet connect button
    - It will be in the top right corner of the web-app and will say 'Connect Wallet' and then when connected it will display the first 5 digits of the wallet address, three dots, then the last 2 digits of the wallet address.
    - This piece will be about 285px wide and 55px tall, to start. I want to make this all responsive after I layout the whole app eventually. It will sit about 35px from the right of the edge of the workspace.

Below those two thin top components and to the right of the task lists component will be two larger 'cards'.

The first, which is directly to the right of the task lists component and sits about 30px away from it, will be the card that is the 'tasks' component. 

- This will be about 680px wide, 1050px height.

- When a task list is selected in the task lists component, this card will display all the tasks in that task list. (i.e. If I clicked on the 'errands' task list, this would display things like 'Pick up groceries', 'Go by the bank', 'Pay electric bill', etc.)
- Each of these tasks will be a narrow little card that simply displays the task title and another 3 vertical dots button that you can tap/click to display a small menu to let you edit task, delete task, etc.
    - These little cards are roughly 600px width by 60px height.
- At the bottom of this card will be another small round button with a + inside that, when clicked, lets you add a new task to this list.

The card to the right of this will also measure roughly 680px wide by 1050px height. It will sit about 30px to the right of the Tasks component and 35px from the right edge of the workspace.

- It will display one of two components. 

        - Display all details of the currently selected task from the tasks component to its leftt, or when you click the add task button in the tasks component to the left, this card will be where you have input fields to enter all the information you want to about that task list such as task

        OR
       
       - When you click the add task button at the bottom right of the tasks component, this card will present the user with all the input fields to add the new task. We will have task name, preferred due date for task, description of task (This last piece is a large text area where you could enter a small shopping list or just details about whichever task you are adding). When that add task button is clicked, opening this component to enter details about the task.


I have imported the following libraries (at your prior suggestion):

- Material UI
    - npm install @mui/material @mui/system @emotion/react @emotion/styled 
- React Router (Using HashRouter, because we will store on IPFS/IPNS)
    - npm install react-router-dom
- fleek-storage-js because we will be using Fleek.co to host our web-app and also we will use it to add, remove, change todo list items such as tasks and task lists.
    - npm install @fleekhq/fleek-storage-js
- date-fns
    - npm install date-fns
- useForm
    - npm install react-hook-form
- Third Web JS for the wallet connection
    - npm install @thirdweb-dev/react @thirdweb-dev/sdk ethers@^5
- RReact-dnd
    - npm install react-dnd react-dnd-html5-backend

---

We decided to layout the project with the following components (at least):

1. `App` component: The root component that serves as the entry point of your application. It contains the main layout along with state management for the entire application. It can include context providers or higher-order components for state and handle any global application logic or styles.

2. `Lists` component: This component represents the left sidebar and contains all individual task lists. It manages the creation of new task lists, selecting the current task list, and other related actions.

3. `TaskList` component: Represents an individual task list item within the left sidebar. It displays the task count, completion progress, and tasks-related actions (e.g., edit or delete a list).

4. `TaskHeader` component: Represents the header bar on top of the tasks area. It displays the current active task list name, tasks completed, and current date.

5. `WalletConnect` component: Represents the wallet connect button situated in the top right corner of the app. It manages connectivity to the user's wallet.

6. `Tasks` component: A card that displays all the tasks for the currently selected task list. It manages task interactions like selecting a task, adding a new task, and other task-related actions.

7. `Task` component: Represents an individual task within the Tasks component. It displays the task title and task-related actions (e.g., edit or delete a task).

8. `TaskDetails` component: This card displays the details of the currently selected task or presents a form to create a new task. It contains all the inputs required for adding or editing a task (e.g., task name, due date, description).

9. `AddButton`: Since you find yourself using the round plus button in multiple places (Lists and Tasks components), you can create a reusable AddButton component. This component can handle a click event to open relevant dialogs (add a new task list or add a new task).

10. `ProgressBar`: Creating this component makes sense in this case, as you want to display it in two different places - within each `TaskList` card and at the bottom of the `Tasks` component. By creating a separate `ProgressBar` component, you can maintain consistent styling and behavior across both instances, which can improve code maintainability and help adhere to the DRY (Don't Repeat Yourself) principle.

—

We have created the react app already as well as the App.js. We have a components folder which holds AddButton.js, ProgressBar.js, TestComponent.js (for testing components as we make them).

The code for AddButton.js is:

```
import React from 'react'
import IconButton from '@mui/material/IconButton';
import AddCircleIcon from '@mui/icons-material/AddCircle';
import { useTheme } from '@mui/material/styles';

const AddButton = ({ onClick, size = 'large', color, style }) => {
  const theme = useTheme();
  const buttonColor = color || theme.palette.buttonColor.main;

  return (
    <IconButton
      onClick={onClick}
      style={{ color: buttonColor, ...style }}
    >
      <AddCircleIcon 
      onClick={onClick}
      style={{ color: buttonColor, ...style }}
      fontSize={size}
      />
    </IconButton>
  );
};

export default AddButton;
```

The code for ProgressBar is:

```
import React from 'react';
import { LinearProgress } from '@mui/material';

const ProgressBar = ({ completedTasks=5, totalTasks=9 }) => {
  // Calculate the progress percentage
  const progress = (completedTasks / totalTasks) * 100;

  return (
    <LinearProgress
      variant="determinate"
      value={progress}
      sx={{
        height: '10px', // Adjust height
        width: '50%', // Adjust width
        borderRadius: '5px', // Round the ends 
        border: '1px solid', // Add a border
        borderColor: 'cardBackgroundColor.alternate', // Adjust the border color   
        bgcolor: 'cardBackgroundColor.main', // Adjust the background color
        '& .MuiLinearProgress-bar': {
          bgcolor: 'backgroundColor.default', // Adjust the filled bar color
        },
      }}
    />
  );
};

export default ProgressBar;
```

We have also created theme.js in the ‘theme’ folder. The code, so far, in theme.js is:

```
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    backgroundColor: {
      default: '#52A7CC',
    },
    textColor: {
      primary: '#000000',
    },
    buttonColor: {
      main: '#A5D4DC',
    },
    cardBackgroundColor: {
      main: '#F2F4F8',
      alternate: '#D9D9D9',
    },
  },
  typography: {
    fontFamily: '"Nunito", sans-serif',
  },
});

export default theme;
```

Please review everything I have typed here a few times.  Ask me any questions about anything that is not clear. Don't just assume you can figure out what I meant if I wasnt clear, please ask me.  After that, let me know if you are ready to move forward from where we stopped (at the progress bar).


