```
import tkinter as tk

import json

  
class Task:

    def __init__(self, text):

        self.text = text
        
    def __str__(self):

        return self.text
        
class TaskManager:

    def __init__(self):

        self.tasks = []

        self.load_tasks()

    def add_task(self, text):

        self.tasks.append(Task(text))

        self.save_tasks()

    def remove_task(self, index):

        del self.tasks[index]

        self.save_tasks()

    def save_tasks(self):

        tasks_text = []

  

        for task in self.tasks:

            tasks_text.append(task.text)

  

        with open("tasks.json", "w") as file:

            json.dump(tasks_text, file)

  

    def load_tasks(self):

        try:

            with open("tasks.json", "r") as file:

                tasks_text = json.load(file)

                for text in tasks_text:

                    self.tasks.append(Task(text))

        except FileNotFoundError:

            pass


class GUI:

    def __init__(self, root):

        self.task = TaskManager()

  

        self.list = tk.Listbox(root,font = ("Arial",16),bg="#112240",fg="white",selectbackground="#1D4ED8",)

        self.list.place(x=5, y= 5,height = 250,width = 290)

        for task in self.task.tasks:

            self.list.insert(tk.END, task.text)

  

        self.entry_add = tk.Entry(root,font = ("Arial",16),bg = "#233554",fg = "white",insertbackground = "white")

        self.entry_add.place(x=5, y= 265,height = 40,width = 290)

  

        self.add_btn = tk.Button(root, text="Add",font = ("Arial",16),bg="#111154",fg="white", command=self.add_task)

        self.add_btn.place(x=65, y= 315,height = 30,width =  80)

  

        self.del_btn = tk.Button(root, text="Delete",font = ("Arial",16),bg="#111154",fg="white", command=self.delete_task)

        self.del_btn.place(x=145, y= 315,height = 30,width =  80)

  

    def add_task(self):

        text = self.entry_add.get()

        self.task.add_task(text)

        self.list.insert(tk.END, text)

        self.entry_add.delete(0, tk.END)

  

    def delete_task(self):

        selected = self.list.curselection()

        if selected:

            index = selected[0]

            self.task.remove_task(index)

  

            self.list.delete(index)

  
root = tk.Tk()

root.geometry("300x350")

root.title("To Do List")

root.configure(bg="#0A192F")

app = GUI(root)

  

root.mainloop()
```