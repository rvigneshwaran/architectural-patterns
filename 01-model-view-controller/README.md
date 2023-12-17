
# Model-View-Controller (MVC) Pattern

The Model-View-Controller (MVC) is an architectural pattern widely used in software development. This pattern divides an application into three interconnected components: the Model, the View, and the Controller. The primary goal is to enhance modularity and maintainability by promoting a clear separation of concerns.

## Components:

### 1. Model

- **Responsibility:** Manages application data and business logic.
- **Example:** In a to-do list application, the Model would handle tasks and their properties. It might include methods like `addTask`, `removeTask`, and `updateTaskStatus`.

### 2. View

- **Responsibility:** Presents data to the user and captures user input.
- **Example:** In the to-do list app, the View would be the user interface displaying the list of tasks. It could include buttons for marking tasks as complete or deleting them.

### 3. Controller

- **Responsibility:** Acts as an intermediary between the Model and the View.
- **Example:** The Controller in the to-do list app would receive user input from the View, process it, and update the Model accordingly. For instance, a `completeTask` method in the Controller might interact with the Model to mark a task as complete.

## Example: To-Do List Application

Consider a simple to-do list application as an example.

- **Model:** Manages tasks and their status (completed or pending). Provides methods to add, remove, or update tasks.

  - **Example:**
    ```python
    class TodoListModel:
        def __init__(self):
            self.tasks = []

        def addTask(self, task):
            self.tasks.append(task)

        def removeTask(self, task):
            self.tasks.remove(task)

        def updateTaskStatus(self, task, status):
            task['status'] = status
    ```
- **View:** Displays the list of tasks to the user and allows them to interact (mark tasks as completed or delete them).

  - **Example:**
    ```python
    class TodoListView:
        def showTasks(self, tasks):
            for task in tasks:
                print(f"{task['title']} - {task['status']}")

        def getUserInput(self):
            # Code to capture user input and return it
            pass
    ```
- **Controller:** Receives user input from the View, updates the Model accordingly, and ensures the View reflects any changes made.

  - **Example:**
    ```python
    class TodoListController:
        def __init__(self, model, view):
            self.model = model
            self.view = view

        def handleUserInput(self):
            user_input = self.view.getUserInput()
            if user_input == 'complete':
                task = self.model.tasks[0]  # For simplicity, assume the first task
                self.model.updateTaskStatus(task, 'completed')
            # Other handling logic...
    ```

## Real-world Scenario

Imagine a physical to-do list notebook:

- **Model:** The actual list of tasks written in the notebook.

  - **Example:** Your physical to-do list could have entries like "Buy groceries" and "Finish work report."
- **View:** The pages of the notebook that display tasks in a readable format.

  - **Example:** Each page of your notebook displays a list of tasks with checkboxes next to them, providing a visual representation.
- **Controller:** Your hand holding a pen, marking tasks as completed or deleting them. Your actions update the physical list through the notebook interface.

  - **Example:** When you mark "Buy groceries" with a checkmark, you are acting as the controller, updating the state of the task in the physical list.

In this scenario, the separation of concerns is evident, allowing for easier modification of tasks without affecting how they are displayed and vice versa.

## Conclusion

The MVC pattern provides a structured approach to software design, improving maintainability and scalability by separating concerns and promoting a clear organization of code.
