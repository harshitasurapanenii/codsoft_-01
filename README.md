# codsoft_-01
To-Do List application is a useful project that helps users manage and organize their tasks efficiently. This project aims to create a command-line or GUI-based application using Python, allowing  users to create, update, and track their to-do lists
import pickle

class Task:
    def __init__(self, title):
        self.title = title
        self.completed = False

    def __str__(self):
        status = '✓' if self.completed else '✗'
        return f"{status} {self.title}"

class ToDoList:
    def __init__(self):
        self.tasks = []
        self.load_tasks()

    def add_task(self, title):
        task = Task(title)
        self.tasks.append(task)
        print(f"Task '{title}' added.")

    def view_tasks(self):
        if not self.tasks:
            print("No tasks.")
        else:
            for i, task in enumerate(self.tasks, 1):
                print(f"{i}. {task}")

    def mark_task_completed(self, task_index):
        if 1 <= task_index <= len(self.tasks):
            task = self.tasks[task_index - 1]
            task.completed = True
            print(f"Task '{task.title}' marked as completed.")
        else:
            print("Invalid task number.")

    def delete_task(self, task_index):
        if 1 <= task_index <= len(self.tasks):
            task = self.tasks.pop(task_index - 1)
            print(f"Task '{task.title}' deleted.")
        else:
            print("Invalid task number.")

    def save_tasks(self):
        with open('tasks.pickle', 'wb') as f:
            pickle.dump(self.tasks, f)
        print("Tasks saved.")

    def load_tasks(self):
        try:
            with open('tasks.pickle', 'rb') as f:
                self.tasks = pickle.load(f)
            print("Tasks loaded.")
        except FileNotFoundError:
            print("No saved tasks found.")

def main():
    todo_list = ToDoList()

    while True:
        print("\n===== TO-DO LIST MENU =====")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Mark Task as Completed")
        print("4. Delete Task")
        print("5. Save Tasks")
        print("6. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            title = input("Enter task title: ")
            todo_list.add_task(title)
        elif choice == '2':
            todo_list.view_tasks()
        elif choice == '3':
            task_index = int(input("Enter task number to mark as completed: "))
            todo_list.mark_task_completed(task_index)
        elif choice == '4':
            task_index = int(input("Enter task number to delete: "))
            todo_list.delete_task(task_index)
        elif choice == '5':
            todo_list.save_tasks()
        elif choice == '6':
            todo_list.save_tasks()
            break
        else:
            print("Invalid choice. Please enter a number from 1 to 6.")

if __name__ == "__main__":
    main()
