# TO-DO-LIST
import tkinter as tk
from tkinter import messagebox

def add_task():
    task = entry.get()
    if task != "":
        listbox.insert(tk.END, task)
        entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Input Error", "Please enter a task.")

def delete_task():
    try:
        selected_task_index = listbox.curselection()[0]
        listbox.delete(selected_task_index)
    except IndexError:
        messagebox.showwarning("Delete Error", "Please select a task to delete.")

def save_tasks():
    with open("tasks.txt", "w") as f:
        tasks = listbox.get(0, listbox.size())
        for task in tasks:
            f.write(task + "\n")
    messagebox.showinfo("Saved", "Tasks saved successfully!")

def load_tasks():
    try:
        with open("tasks.txt", "r") as f:
            for line in f:
                listbox.insert(tk.END, line.strip())
    except FileNotFoundError:
        pass  # First time no file exists

# Main GUI window
root = tk.Tk()
root.title("To-Do List App")
root.geometry("400x400")
root.config(bg="lightblue")

# Entry field
entry = tk.Entry(root, width=40)
entry.pack(pady=10)

# Buttons
btn_add = tk.Button(root, text="Add Task", command=add_task)
btn_add.pack(pady=5)

btn_delete = tk.Button(root, text="Delete Selected Task", command=delete_task)
btn_delete.pack(pady=5)

btn_save = tk.Button(root, text="Save Tasks", command=save_tasks)
btn_save.pack(pady=5)

btn_load = tk.Button(root, text="Load Tasks", command=load_tasks)
btn_load.pack(pady=5)

# Listbox to show tasks
listbox = tk.Listbox(root, width=45, height=10)
listbox.pack(pady=10)

# Load tasks if file exists
load_tasks()

root.mainloop()
