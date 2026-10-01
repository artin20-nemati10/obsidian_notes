#python_code
```
import tkinter as tk
import random
import string
from tkinter import messagebox
import os
import json


File_name = "users.json"


def load_users():
    if not os.path.exists(File_name):
        return {}
    with open(File_name, "r", encoding="utf-8") as f:
        return json.load(f)


def save_users(users):
    with open(File_name, "w", encoding="utf-8") as f:
        json.dump(users, f, ensure_ascii=False, indent=2)


users = load_users()


def sign_up():
    u = e_user.get().strip()
    p = e_pass.get().strip()
    if not u or not p:
        messagebox.showerror("Error", "Enter the name and the password")
        return
    if u in users:
        messagebox.showerror("Error", "This account exists")
        return
    users[u] = p
    save_users(users)
    if captcha_entry.get() == captcha_text and robot.get() == 1:
        messagebox.showinfo("OK", "Signed Up")


def login():
    u = e_user.get().strip()
    p = e_pass.get().strip()
    if (
        u in users
        and users[u] == p
        and captcha_entry.get() == captcha_text
        and robot.get() == 1
    ):
        messagebox.showinfo("OK", "Loged In Succesfully")
    else:
        messagebox.showerror("Error", "Valid Information")


def varificate():
    if captcha_entry.get() == captcha_text:
        messagebox.showinfo("Succesfull", "You varified succesfully")
    else:
        messagebox.showerror("Unsuccesfull", "Try again")


def generate_captcha(length=5):
    global captcha
    captcha_values = string.ascii_letters + string.digits + string.digits
    return "".join(random.choice(captcha_values) for _ in range(length))


def draw_captcha(canvas, text):
    canvas.delete("all")
    width = int(canvas["width"])
    height = int(canvas["height"])

    for _ in range(50):
        x = random.randint(0, width)
        y = random.randint(0, height)
        r = random.randint(1, 2)
        color = random.choice(["#D6D2D2", "#8d8b8b", "#525151"])
        canvas.create_oval(x, y, x + r, y + r, fill=color, outline=color)

    for _ in range(3):
        x1 = random.randint(0, width)
        y1 = random.randint(0, height)
        x2 = random.randint(0, width)
        y2 = random.randint(0, height)
        canvas.create_line(x1, y1, x2, y2)
    start_x = 16
    for ch in text:
        y = random.randint(15, 25)
        color = random.choice(["black", "darkblue", "darkred", "darkgreen"])
        canvas.create_text(
            start_x,
            y,
            text=ch,
            font=("Arial", random.randint(16, 22)),
            fill=color,
            angle=random.randint(-25, 25),
        )
        start_x += random.randint(19, 35)


def refresh():
    global captcha_text
    captcha_values = string.ascii_letters + string.digits + string.digits
    captcha_text = ""
    for _ in range(5):
        captcha_text = captcha_text + (random.choice(captcha_values))
    draw_captcha(canvas, captcha_text)


window = tk.Tk()
window.title("Varification")
window.geometry("210x300")

tk.Label(window, text="User:", font=("Arial", 13)).place(x=5, y=5, width=40, height=40)
e_user = tk.Entry(window, font=("Arial", 13), bd=2, relief="ridge")
e_user.place(x=55, y=5, width=150, height=35)

tk.Label(window, text="Pass:", font=("Arial", 13)).place(x=5, y=50, width=40, height=40)
e_pass = tk.Entry(window, font=("Arial", 13), bd=2, relief="ridge")
e_pass.place(x=55, y=50, width=150, height=35)

captcha_text = generate_captcha(5)
canvas = tk.Canvas(window, width=150, height=40, bg="white", bd=1, relief="groove")
canvas.place(x=52, y=100)
draw_captcha(canvas, captcha_text)
tk.Button(window, text="⟳", font=("Arial", 22), command=refresh).place(
    x=5, y=100, height=40, width=40
)

tk.Label(window, text="Enter:", font=("Arial", 13)).place(
    x=5, y=150, width=40, height=40
)
captcha_entry = tk.Entry(window, font=("Arial", 13), bd=2, relief="ridge")
captcha_entry.place(x=55, y=150, width=150, height=35)
robot = tk.IntVar()
not_robot = tk.Checkbutton(
    window, text="I'm not robot.", font=("Arial", 13), variable=robot
).place(x=5, y=195)

tk.Button(window, text="sign up", font=("Arial", 13), command=sign_up).place(
    x=35, y=230, width=65, height=40
)
tk.Button(window, text="log in", font=("Arial", 13), command=login).place(
    x=100, y=230, width=65, height=40
)


window.mainloop()

```