
```
import pandas as pd
import tkinter as tk
from tkinter import ttk, messagebox

names = ["num","Commodity","Number of purchase","Number of sales","Remain number","Purchase price","Sale price","Total price purchase","Total price sale","Profit"]

all_data={
          "Commodity":[],
          "Number of purchase":[],
          "Number of sales":[],
          "Remain number" :[],
          "Purchase price":[],
          "Sale price":[],
          "Total price purchase":[],
          "Total price sale":[],          
          "Profit":[]}

window= tk.Tk()
window.geometry("1400x300")
window.title("Commodity")
style = ttk.Style(window)
style.configure("Treeview",font=("Arial",10))

tree=ttk.Treeview(window,columns=names, show="headings")

labels_frame= tk.Frame(window)
labels_frame.pack(side="top",pady=5)
total_price_bought_label=tk.Label(labels_frame,text="Total price bought :0.00$",font=("Arial",12))
total_price_sold_label=tk.Label(labels_frame,text="Total price sold :0.00$",font=("Arial",12))
total_profit_label=tk.Label(labels_frame,text="Total Profit :0.00$",font=("Arial",12))





total_price_bought_label.pack(side="left",padx=10)
total_price_sold_label.pack(side="left",padx=10)
total_profit_label.pack(side="left",padx=40)
for col in names:
    tree.heading(col, text=col)
    tree.column(col,width=120,anchor="center")

tree.pack(fill="both",expand=True,pady=10)

tree.tag_configure("evenrow",background="#BDBDBD")
tree.tag_configure("oddrow",background="white")
def refresh_table():
    
    for row in tree.get_children():
        tree.delete(row)

    for i in range(len(all_data["Commodity"])):
        tree.insert("", "end", values=(
            i+1, 
            all_data["Commodity"][i],
            all_data["Number of purchase"][i],
            all_data["Number of sales"][i],
            all_data["Remain number"][i],
            all_data["Purchase price"][i],
            all_data["Sale price"][i],
            all_data["Total price purchase"][i],
            all_data["Total price sale"][i],
            all_data["Profit"][i]
        ))

def click_on_commodity(event):
    edit_win=tk.Toplevel(window)
    edit_win.title("Details")
    edit_win.geometry("100x100")

    def show_datails():
        edit_win.destroy()
        selected_item=tree.focus()
        if not selected_item:
            return
        
        values = tree.item(selected_item,"values")
        detail_win=tk.Toplevel(window)
        detail_win.title("Commodity details")
        detail_win.geometry("300x500")
        entries=[]
        for i, col in enumerate(names):
            tk.Label(detail_win, text= col + ":").pack()

            e=tk.Entry(detail_win)
            e.insert(0,values[i])
            e.pack()
            entries.append(e)
        
        def save_changes():
            
            new_values = [e.get() for e in entries]
            row_index = tree.index(selected_item)

            
            name_val = new_values[1].strip()
            bought_amount_val = int(new_values[2])
            sold_amount_val = int(new_values[3])
            bought_price_val = float(new_values[5])
            sold_price_val = float(new_values[6])

            
            total_price_bought = bought_amount_val * bought_price_val
            total_price_sold = sold_amount_val * sold_price_val
            remainder = bought_amount_val - sold_amount_val
            profit = total_price_sold - ((bought_amount_val - remainder) * bought_price_val)

            
            all_data["Commodity"][row_index] = name_val
            all_data["Number of purchase"][row_index] = bought_amount_val
            all_data["Number of sales"][row_index] = sold_amount_val
            all_data["Purchase price"][row_index] = bought_price_val
            all_data["Sale price"][row_index] = sold_price_val
            all_data["Total price purchase"][row_index] = total_price_bought
            all_data["Total price sale"][row_index] = total_price_sold
            all_data["Remain number"][row_index] = remainder
            all_data["Profit"][row_index] = profit

            update()  # جدول دوباره رفرش بشه
            detail_win.destroy()
        tk.Button(detail_win, text = "Save",command=save_changes).pack(pady=10)
    notes={}
    notes = {}

    def open_note():
        edit_win.destroy()
        selected_item=tree.focus()
        if not selected_item:
            return
        row_index = tree.index(selected_item)
        note_win = tk.Toplevel(window)
        note_win.title(f"Note for {all_data['Commodity'][row_index]}")
        note_win.geometry("400x600")

        commodity_name = all_data["Commodity"][row_index]

        tk.Label(note_win, text=f"Commodity: {commodity_name}",
                font=("Arial", 12, "bold")).pack(pady=5)

        text_area = tk.Text(note_win, wrap="word", font=("Arial", 11))
        text_area.pack(expand=True, fill="both", padx=10, pady=10)

      
        prev_note = notes.get(commodity_name, "")
        text_area.insert("1.0", prev_note)

        def save_note():
            notes[commodity_name] = text_area.get("1.0", "end-1c")
            note_win.destroy()

        tk.Button(note_win, text="Save Note", command=save_note).pack(pady=5)



    tk.Button(edit_win , text= "Edit", command = show_datails).pack(pady=10)
    tk.Button(edit_win,text="Note",command=open_note).pack(pady=10)


def update():

    df=pd.DataFrame(all_data)
    tree.delete(*tree.get_children())
    total_price_sold_value=0
    total_profit_value=0
    total_price_bought_value=0
    for i, (_, row) in enumerate(df.iterrows(),start=1):
        tag="evenrow" if i % 2 ==0 else "oddrow"
        tree.insert("","end",values=[i] + list(row),tags=(tag,))

        try:
            profit_value= float(str(row["Profit"]))
            total_profit_value+=profit_value
        except:
            pass
        try:
            price_bought_value= float(str(row["Total price purchase"]))
            total_price_bought_value+=price_bought_value
        except:
            pass
            
        try:
            price_sold_value= float(str(row["Total price sale"]))
            total_price_sold_value+=price_sold_value
        except:
            pass
    color="green" if total_profit_value >=0 else "red"
    total_price_sold_label.config(text=f"Total price sold : {total_price_sold_value :.2f}$")
    total_profit_label.config(text=f"Total Profit : {total_profit_value :.2f}$",fg=color)
    total_price_bought_label.config(text=f"Total price bought : {total_price_bought_value :.2f}$")

def new():
    root=tk.Toplevel(window)
    root.geometry("300x750")
    
    root.title("commodity info")
    tk.Label(root,text="Commodity name :").pack(pady=5)
    name=tk.Entry(root);name.pack(pady=5)

    tk.Label(root,text="Number of purchase :").pack(pady=5)
    bought_amount = tk.Entry(root);bought_amount.pack(pady=5)

    tk.Label(root,text="number of sales:").pack(pady=5)
    sold_amount=tk.Entry(root);sold_amount.pack(pady=5)

    tk.Label(root,text="Price of purchase :").pack(pady=5)
    bought_price=tk.Entry(root);bought_price.pack(pady=5)

    tk.Label(root,text="Price of sales:").pack(pady=5)
    Sold_price=tk.Entry(root);Sold_price.pack(pady=5)




    def add():
        name_val=name.get().strip()
        bought_amount_val=bought_amount.get().strip()
        sold_amount_val=sold_amount.get().strip()
        bought_price_val=bought_price.get().strip()
        sold_price_val=Sold_price.get().strip()
        if (not name_val or 
            not bought_amount_val or 
            not sold_amount_val or 
            not bought_price_val or 
            not sold_price_val) :
            messagebox.showerror("Error","Please fill all fields")
            return
        try:
            bought_amount_val=int(bought_amount_val)
            sold_amount_val=int(sold_amount_val)
            bought_price_val=float(bought_price_val)
            sold_price_val=float(sold_price_val)
        except ValueError:
            messagebox.showerror("Error","Please becarefull to fill the fields")
            return
        total_price_bought= bought_amount_val* bought_price_val
        total_price_sold= sold_amount_val * sold_price_val
        remainder=bought_amount_val - sold_amount_val
        profit=total_price_sold - ((bought_amount_val-remainder)*bought_price_val)

        
        

        all_data["Commodity"].append(name_val)

        all_data["Number of purchase"].append(bought_amount_val)

        all_data["Number of sales"].append(sold_amount_val)
        all_data["Purchase price"].append(bought_price_val)

        all_data["Sale price"].append(sold_price_val)
        all_data["Total price purchase"].append(total_price_bought)
        all_data["Total price sale"].append(total_price_sold)
        all_data["Remain number"].append(remainder)
        all_data["Profit"].append(profit)
        update()
        root.destroy()
    tk.Button(root,text="Add to list",command=add).pack(pady=10)
tk.Button(labels_frame,text="Add",command=new,anchor="center",font=("Arial",10)).pack()
tree.bind("<Double-1>",click_on_commodity)
main_menu= tk.Menu(window)
file_menu = tk.Menu(main_menu, tearoff=0)

file_menu.add_command(label="Save",command=None)
file_menu.add_command(label="Open",command=None)
file_menu.add_command(label="Exit",command=quit)
main_menu.add_cascade(label="Menu",menu=file_menu)

window.config(menu=main_menu)


edit_menu = tk.Menu(main_menu, tearoff=0)

edit_menu.add_command(label="Add",command=new)
edit_menu.add_command(label="Delete",command=None)
edit_menu.add_command(label="Edit",command=None)
main_menu.add_cascade(label="Edit",menu=edit_menu)

window.config(menu=main_menu)



window.mainloop()

```