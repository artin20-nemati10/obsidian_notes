```
import pandas as pd

import tkinter as tk

import random

import string

import os

import json

from tkinter import ttk, messagebox

  

File_name = "users.json"

  

current_user = None

  
  

def open_inventory():

    global inventory_window, tree

  

    names = [

        "num",

        "Commodity",

        "Number of purchase",

        "Number of sales",

        "Remain number",

        "Purchase price",

        "Sale price",

        "Total price purchase",

        "Total price sale",

        "Profit",

    ]

  

    all_data = {

        "Commodity": [],

        "Number of purchase": [],

        "Number of sales": [],

        "Remain number": [],

        "Purchase price": [],

        "Sale price": [],

        "Total price purchase": [],

        "Total price sale": [],

        "Profit": [],

    }

    if users[current_user]["inventory"]:

        all_data = users[current_user]["inventory"]

    inventory_window = tk.Toplevel(window)

    inventory_window.state("zoomed")

    inventory_window.focus_force()

    inventory_window.title("Inventory Managment")

    inventory_window.configure(bg="#EEF2FF")

  

    style = ttk.Style(inventory_window)

    style.configure("Treeview", font=("Arial", 10))

  

    tree = ttk.Treeview(inventory_window, columns=names, show="headings")

  

    labels_frame = tk.Frame(inventory_window)

    labels_frame.pack(side="top", pady=5)

    total_price_bought_label = tk.Label(

        labels_frame, text="Total price bought :0.00$", font=("Arial", 12)

    )

    total_price_sold_label = tk.Label(

        labels_frame, text="Total price sold :0.00$", font=("Arial", 12)

    )

    total_profit_label = tk.Label(

        labels_frame, text="Total Profit :0.00$", font=("Arial", 12)

    )

  

    total_price_bought_label.pack(side="left", padx=10)

    total_price_sold_label.pack(side="left", padx=10)

    total_profit_label.pack(side="left", padx=40)

    for col in names:

        tree.heading(col, text=col)

        tree.column(col, width=120, anchor="center")

  

    tree.pack(fill="both", expand=True, pady=10)

  

    tree.tag_configure("evenrow", background="#BDBDBD")

    tree.tag_configure("oddrow", background="white")

  

    def refresh_table():

  

        for row in tree.get_children():

            tree.delete(row)

  

        for i in range(len(all_data["Commodity"])):

            tree.insert(

                "",

                "end",

                values=(

                    i + 1,

                    all_data["Commodity"][i],

                    all_data["Number of purchase"][i],

                    all_data["Number of sales"][i],

                    all_data["Remain number"][i],

                    all_data["Purchase price"][i],

                    all_data["Sale price"][i],

                    all_data["Total price purchase"][i],

                    all_data["Total price sale"][i],

                    all_data["Profit"][i],

                ),

            )

  

    def click_on_commodity(event):

        edit_win = tk.Toplevel(inventory_window)

        edit_win.title("Details")

        edit_win.geometry("100x100")

  

        def show_datails():

            edit_win.destroy()

            selected_item = tree.focus()

            if not selected_item:

                return

  

            values = tree.item(selected_item, "values")

            detail_win = tk.Toplevel(inventory_window)

            detail_win.title("Commodity details")

            detail_win.geometry("300x500")

            entries = []

            for i, col in enumerate(names):

                tk.Label(detail_win, text=col + ":").pack()

  

                e = tk.Entry(detail_win)

                e.insert(0, values[i])

                e.pack()

                entries.append(e)

  

            def save_changes():

  

                new_values = [e.get() for e in entries]

                row_index = tree.index(selected_item)

  

                name_val = new_values[1].strip()

                bought_amount_val = float(new_values[2])

                sold_amount_val = float(new_values[3])

                bought_price_val = float(new_values[5])

                sold_price_val = float(new_values[6])

  

                total_price_bought = bought_amount_val * bought_price_val

                total_price_sold = sold_amount_val * sold_price_val

                remainder = bought_amount_val - sold_amount_val

                profit = total_price_sold - (

                    (bought_amount_val - remainder) * bought_price_val

                )

  

                all_data["Commodity"][row_index] = name_val

                all_data["Number of purchase"][row_index] = bought_amount_val

                all_data["Number of sales"][row_index] = sold_amount_val

                all_data["Purchase price"][row_index] = bought_price_val

                all_data["Sale price"][row_index] = sold_price_val

                all_data["Total price purchase"][row_index] = total_price_bought

                all_data["Total price sale"][row_index] = total_price_sold

                all_data["Remain number"][row_index] = remainder

                all_data["Profit"][row_index] = profit

  

                update()

                users[current_user]["inventory"] = all_data

                save_users(users)

                detail_win.destroy()

  

            tk.Button(detail_win, text="Save", command=save_changes).pack(pady=10)

  

        notes = {}

        notes = {}

  

        def open_note():

            edit_win.destroy()

            selected_item = tree.focus()

            if not selected_item:

                return

            row_index = tree.index(selected_item)

            note_win = tk.Toplevel(inventory_window)

            note_win.title(f"Note for {all_data['Commodity'][row_index]}")

            note_win.geometry("400x600")

  

            commodity_name = all_data["Commodity"][row_index]

  

            tk.Label(

                note_win,

                text=f"Commodity: {commodity_name}",

                font=("Arial", 12, "bold"),

            ).pack(pady=5)

  

            text_area = tk.Text(note_win, wrap="word", font=("Arial", 11))

            text_area.pack(expand=True, fill="both", padx=10, pady=10)

  

            prev_note = notes.get(commodity_name, "")

            text_area.insert("1.0", prev_note)

  

            def save_note():

                notes[commodity_name] = text_area.get("1.0", "end-1c")

                note_win.destroy()

  

            tk.Button(note_win, text="Save Note", command=save_note).pack(pady=5)

  

        tk.Button(edit_win, text="Edit", command=show_datails).pack(pady=10)

        tk.Button(edit_win, text="Note", command=open_note).pack(pady=10)

  

    def update():

  

        df = pd.DataFrame(all_data)

        tree.delete(*tree.get_children())

        total_price_sold_value = 0

        total_profit_value = 0

        total_price_bought_value = 0

        for i, (_, row) in enumerate(df.iterrows(), start=1):

            tag = "evenrow" if i % 2 == 0 else "oddrow"

            tree.insert("", "end", values=[i] + list(row), tags=(tag,))

  

            try:

                profit_value = float(str(row["Profit"]))

                total_profit_value += profit_value

            except:

                pass

            try:

                price_bought_value = float(str(row["Total price purchase"]))

                total_price_bought_value += price_bought_value

            except:

                pass

  

            try:

                price_sold_value = float(str(row["Total price sale"]))

                total_price_sold_value += price_sold_value

            except:

                pass

        color = "green" if total_profit_value >= 0 else "red"

        total_price_sold_label.config(

            text=f"Total price sold : {total_price_sold_value:.2f}$"

        )

        total_profit_label.config(

            text=f"Total Profit : {total_profit_value:.2f}$", fg=color

        )

        total_price_bought_label.config(

            text=f"Total price bought : {total_price_bought_value:.2f}$"

        )

  

    def new():

        root = tk.Toplevel(inventory_window)

        root.geometry("300x750")

  

        root.title("commodity info")

        tk.Label(root, text="Commodity name :").pack(pady=5)

        name = tk.Entry(root)

        name.pack(pady=5)

  

        tk.Label(root, text="Number of purchase :").pack(pady=5)

        bought_amount = tk.Entry(root)

        bought_amount.pack(pady=5)

  

        tk.Label(root, text="number of sales:").pack(pady=5)

        sold_amount = tk.Entry(root)

        sold_amount.pack(pady=5)

  

        tk.Label(root, text="Price of purchase :").pack(pady=5)

        bought_price = tk.Entry(root)

        bought_price.pack(pady=5)

  

        tk.Label(root, text="Price of sales:").pack(pady=5)

        Sold_price = tk.Entry(root)

        Sold_price.pack(pady=5)

  

        def add():

            name_val = name.get().strip()

            bought_amount_val = float(bought_amount.get().strip())

            sold_amount_val = float(sold_amount.get().strip())

            bought_price_val = float(bought_price.get().strip())

            sold_price_val = float(Sold_price.get().strip())

            if (

                not name_val

                or not bought_amount_val

                or not sold_amount_val

                or not bought_price_val

                or not sold_price_val

            ):

                messagebox.showerror("Error", "Please fill all fields")

                return

            try:

                bought_amount_val = int(bought_amount_val)

                sold_amount_val = int(sold_amount_val)

                bought_price_val = float(bought_price_val)

                sold_price_val = float(sold_price_val)

            except ValueError:

                messagebox.showerror("Error", "Please becarefull to fill the fields")

                return

            total_price_bought = bought_amount_val * bought_price_val

            total_price_sold = sold_amount_val * sold_price_val

            remainder = bought_amount_val - sold_amount_val

            profit = total_price_sold - (

                (bought_amount_val - remainder) * bought_price_val

            )

  

            all_data["Commodity"].append(name_val)

  

            all_data["Number of purchase"].append(bought_amount_val)

  

            all_data["Number of sales"].append(sold_amount_val)

            all_data["Purchase price"].append(bought_price_val)

  

            all_data["Sale price"].append(sold_price_val)

            all_data["Total price purchase"].append(total_price_bought)

            all_data["Total price sale"].append(total_price_sold)

            all_data["Remain number"].append(remainder)

            all_data["Profit"].append(profit)

            users[current_user]["inventory"] = all_data

            save_users(users)

            update()

            users[current_user]["inventory"] = all_data

            save_users(users)

            root.destroy()

  

        tk.Button(root, text="Add to list", command=add).pack(pady=10)

    def delete():

        selected_item = tree.focus

        if not selected_item:

            pass

  

    tk.Button(

        labels_frame, text="Add", command=new, anchor="center", font=("Arial", 10)

    ).pack()

    tree.bind("<Double-1>", click_on_commodity)

    main_menu = tk.Menu(inventory_window)

    file_menu = tk.Menu(main_menu, tearoff=0)

  

    file_menu.add_command(label="Save", command=None)

    file_menu.add_command(label="Open", command=None)

    file_menu.add_command(label="Exit", command=quit)

    main_menu.add_cascade(label="Menu", menu=file_menu)

  

    inventory_window.config(menu=main_menu)

  

    edit_menu = tk.Menu(main_menu, tearoff=0)

  

    edit_menu.add_command(label="Add", command=new)

    edit_menu.add_command(label="Delete", command=None)

    edit_menu.add_command(label="Edit", command=None)

    main_menu.add_cascade(label="Edit", menu=edit_menu)

  

    inventory_window.config(menu=main_menu)

    update()

  
  

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

        messagebox.showerror("This Username already exists", "Try another one")

        return

    if (

        not any(c.isalpha() for c in p)

        or not any(c.isdigit() for c in p)

        or not any(c.isalnum() for c in p)

        or not any(c.isupper() for c in p)

        or len(p) < 8

    ):

        messagebox.showerror(

            "Weak Password",

            "Password must contain letters, numbers, and special characters",

        )

        return

    users[u] = {

        "password": p,

        "inventory": {

            "Commodity": [],

            "Number of purchase": [],

            "Number of sales": [],

            "Remain number": [],

            "Purchase price": [],

            "Sale price": [],

            "Total price purchase": [],

            "Total price sale": [],

            "Profit": [],

        },

    }

  

    if captcha_entry.get() == captcha_text and robot.get() == 1:

        messagebox.showinfo("OK", "Signed Up")

    save_users(users)

  
  

def login():

    u = e_user.get().strip()

    p = e_pass.get().strip()

    if (

        u in users

        and users[u]["password"] == p

        and captcha_entry.get() == captcha_text

        and robot.get() == 1

    ):

        global current_user

        current_user = u

        all_data = users[current_user]["inventory"]

        window.withdraw()

  

        open_inventory()

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

  
  

def toggle_password():

    if e_pass.cget("show") == "*":

        e_pass.config(show="")

        show_btn.config(text="👁", font=("Arial", 15))

    else:

        e_pass.config(show="*")

        show_btn.config(text="👁", font=("Arial", 15))

  
  

BG = "#EEF2FF"

CARD = "#FFFFFF"

PRIMARY = "#2563EB"

SUCCES = "#10B981"

TEXT = "#1F2937"

  

window = tk.Tk()

window.title("Varification")

window.state("zoomed")

window.configure(bg=BG)

  

#################################################################################################

  

login_frame = tk.Frame(window, bg=CARD, bd=0, padx=30, pady=30)

login_frame.place(relx=0.5, rely=0.5, anchor="center", width=430, height=560)

  

#################################################################################################

tk.Label(

    login_frame,

    text="Inventory Management",

    font=("Segoe UI", 22, "bold"),

    bg=CARD,

    fg="#1E3A8A",

).grid(row=0, column=0, columnspan=2, pady=(10, 30))

#################################################################################################

  

tk.Label(login_frame, text="Username", bg=CARD, font=("Segoe UI", 11)).grid(

    row=1, column=0, sticky="w"

)

e_user = tk.Entry(login_frame, font=("Segoe UI", 12), bd=2, relief="ridge", width=28)

e_user.grid(row=2, column=0, pady=8)

  

#################################################################################################

  

tk.Label(login_frame, text="Password", bg=CARD, font=("Segoe UI", 11)).grid(

    row=3, column=0, sticky="w"

)

e_pass = tk.Entry(

    login_frame, font=("Arial", 13), bd=2, relief="ridge", show="*", width=28

)

e_pass.grid(row=4, column=0, pady=8)

  

#################################################################################################

  

show_btn = tk.Button(

    login_frame, text="👁", font=("Arial", 15), command=toggle_password, relief="flat"

)

show_btn.grid(row=4, column=1, padx=8)

  

#################################################################################################

  

captcha_text = generate_captcha(5)

canvas = tk.Canvas(login_frame, width=150, height=40, bg="white", bd=1, relief="groove")

canvas.grid(row=5, column=0, columnspan=2, pady=15)

draw_captcha(canvas, captcha_text)

  

#################################################################################################

  

tk.Button(login_frame, text="⟳", font=("Arial", 15), command=refresh).grid(

    row=5, column=1, columnspan=2, pady=15

)

  

captcha_entry = tk.Entry(login_frame, font=("Arial", 13), bd=2, relief="ridge")

captcha_entry.grid(row=6, column=0, columnspan=2, pady=10)

robot = tk.IntVar()

not_robot = tk.Checkbutton(

    login_frame, text="I'm not robot.", font=("Segoe UI", 11), variable=robot

).grid(row=7, column=0, columnspan=2, pady=10)

  

tk.Button(

    login_frame,

    text="Login",

    bg="#2563EB",

    fg="white",

    font=("Segoe UI", 12, "bold"),

    relief="flat",

    cursor="hand2",

    width=25,

    command=login,

).grid(row=8, column=0, columnspan=2, pady=10)

  

tk.Button(

    login_frame,

    text="Sign Up",

    bg="#10B981",

    fg="white",

    font=("Segoe UI", 12, "bold"),

    relief="flat",

    cursor="hand2",

    width=25,

    command=sign_up,

).grid(row=9, column=0, columnspan=2, pady=5)

  
  

window.mainloop()
```