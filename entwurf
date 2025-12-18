FILENAME = "todo.txt"

DONE_PREFIX = "[done]: "

def load_tasks():
    try:
        with open(FILENAME, "r", encoding="utf-8") as file:
            return [line.strip() for line in file.readlines() if line.strip()]
    except FileNotFoundError:
        return []

def save_tasks(tasks):
    with open(FILENAME, "w", encoding="utf-8") as file:
        for task in tasks:
            file.write(task + "\n")

def input_task():
    task = input("Enter a new task: ").strip()
    return task

def input_date():
    date = input("Enter due date (YYYY-MM-DD) or leave blank: ").strip()
    return date

def add_task(tasks):
    task = input_task()
    if not task:
        print("Empty task not added.")
        return

    date = input_date()
    if date:
        task = f"{task} (Due: {date})"
    tasks.append(task)
    print("Task added.")

def list_view(tasks, mode="all"):
    """Return list of (original_index, task_string) for the selected mode."""
    view = []
    for i, t in enumerate(tasks):
        is_done = t.startswith(DONE_PREFIX)
        if mode == "all":
            view.append((i, t))
        elif mode == "open" and not is_done:
            view.append((i, t))
        elif mode == "done" and is_done:
            view.append((i, t))
    return view

def show_tasks(tasks, mode="all"):
    view = list_view(tasks, mode)
    if not view:
        print("No tasks available." if mode == "all" else "No tasks in this view.")
        return view

    for shown_idx, (_, task) in enumerate(view, start=1):
        print(f"{shown_idx}. {task}")
    return view

def input_number(max_num, text):
    choice = input(text).strip()
    try:
        num = int(choice)
    except ValueError:
        print("Please enter a number.")
        return None

    if num < 1 or num > max_num:
        print("This number does not exist.")
        return None

    return num - 1

def finish_task(tasks):
    print("\n--- Mark Task as Done ---")
    view = show_tasks(tasks, "open")
    if not view:
        return

    picked = input_number(len(view), "Task number: ")
    if picked is None:
        return

    original_idx, _ = view[picked]

    if tasks[original_idx].startswith(DONE_PREFIX):
        print("Task is already done.")
    else:
        tasks[original_idx] = DONE_PREFIX + tasks[original_idx]
        print("Task marked as done.")

def delete_task(tasks):
    print("\n--- Delete Task ---")
    view = show_tasks(tasks, "all")
    if not view:
        return

    picked = input_number(len(view), "Task number: ")
    if picked is None:
        return

    original_idx, task = view[picked]
    print("deleting:", task)
    confirm = input("Are you sure? (y/n): ").strip().lower()
    if confirm == "y":
        tasks.pop(original_idx)
        print("Task deleted.")
    else:
        print("Delete cancelled.")

def show_menu():
    print("\n--- Todo Manager ---")
    print("1) Add Task")
    print("2) Show all tasks")
    print("3) Show open tasks")
    print("4) Show done tasks")
    print("5) Mark task as done")
    print("6) Delete task")
    print("7) Exit")

def main():
    tasks = load_tasks()
    print("Welcome to your To-Do List.")

    while True:
        show_menu()
        choice = input("Your choice: ").strip()

        if choice == "1":
            add_task(tasks)
            save_tasks(tasks)
        elif choice == "2":
            show_tasks(tasks, "all")
        elif choice == "3":
            show_tasks(tasks, "open")
        elif choice == "4":
            show_tasks(tasks, "done")
        elif choice == "5":
            finish_task(tasks)
            save_tasks(tasks)
        elif choice == "6":
            delete_task(tasks)
            save_tasks(tasks)
        elif choice == "7":
            save_tasks(tasks)
            print("Goodbye!")
            break
        else:
            print("Invalid choice.")

main()
