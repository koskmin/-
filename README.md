import json

def load_tasks():
    try:
        with open("tasks.json", "r") as file:
            tasks = json.load(file)
    except FileNotFoundError:
        tasks = []
    return tasks

def save_tasks(tasks):
    with open("tasks.json", "w") as file:
        json.dump(tasks, file)

def add_task(tasks):
    task_name = input("Enter the task name: ")
    task_description = input("Enter the task description: ")
    task = {
        "name": task_name,
        "description": task_description,
        "completed": False
    }
    tasks.append(task)
    save_tasks(tasks)
    print("Task added successfully.")

def view_tasks(tasks):
    if not tasks:
        print("No tasks found.")
    else:
        for index, task in enumerate(tasks, start=1):
            status = "Completed" if task["completed"] else "Not Completed"
            print(f"{index}. {task['name']} - {task['description']} [{status}]")

def mark_completed(tasks):
    view_tasks(tasks)
    try:
        task_index = int(input("Enter the task number to mark as completed: ")) - 1
        if 0 <= task_index < len(tasks):
            tasks[task_index]["completed"] = True
            save_tasks(tasks)
            print("Task marked as completed.")
        else:
            print("Invalid task number.")
    except ValueError:
        print("Invalid input. Please enter a number.")

def main():
    tasks = load_tasks()

    while True:
        print("\nTask Tool Menu:")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Mark Task as Completed")
        print("4. Exit")

        choice = input("Enter your choice (1/2/3/4): ")

        if choice == "1":
            add_task(tasks)
        elif choice == "2":
            view_tasks(tasks)
        elif choice == "3":
            mark_completed(tasks)
        elif choice == "4":
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
