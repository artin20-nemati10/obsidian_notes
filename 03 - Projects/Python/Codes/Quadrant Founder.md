#python_code
```
import tkinter as tk
import matplotlib.pyplot as plt
main_window=tk.Tk()
main_window.geometry("200x500")
main_window.title("Coordinate Chart")
def one_point():
        main_window.destroy()
        def find_quadrant(event=None):
                        result_text.delete("1.0",tk.END)
                        x = int(entry_x.get())
                        y= int(entry_y.get())
                        point_coordinate = (x,y)
                        match point_coordinate:
                                case (0,0) :
                                        text = "Vetrex"
                                case (x,0) if x>0:
                                        text = "X line"
                                case (x,0) if x<0:
                                        text = "X line"
                                case (0,y) if y>0 :
                                        text = "Y line"
                                case (0,y) if y<0 :
                                        text = "Y line"
                                case (x,y) if x>0 and y>0:
                                        text = "first Quadrant"
                                case (x,y) if x<0 and y>0:
                                        text = "second Quadrant"
                                case (x,y) if x<0 and y<0:
                                        text= "third Quadrant"
                                case (x,y) if x>0 and y<0:
                                        text = "fourth Quadrant"
                        result_text.insert(tk.END,text)    
                
        def clear():
                entry_y.delete(0,"end")
                entry_x.delete(0,"end")
                result_text.delete("1.0","end")
                entry_x.focus_set()
                plt.close()

        def mew(event=None):
                entry_y.focus_set()        


        def coordinate_chart():
                x= int(entry_x.get())
                y=int(entry_y.get())
                plt.plot(x, y, marker = "o", color ="red")
                plt.axhline(0,color = "black",linewidth=1)
                plt.axvline(0,color="black",linewidth=1)

                plt.grid(True)
                plt.xlabel("X")
                plt.ylabel("Y")
                plt.title("Coordinate")
                plt.show()
        window = tk.Tk()
        window.title("Quadrant Finder")
        window.geometry("300x200")

        label_x = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x.place(x=5,y=20,height=45,width=45)

        entry_x = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x.place(x=50,y=20,height=45,width=80)
        entry_x.focus_set()
        entry_x.bind("<Return>",mew)
        label_y = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y.place(x=155,y=20,height=45,width=45)

        entry_y = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y.place(x=200,y=20,height=45,width=80)

        entry_y.bind("<Return>",find_quadrant)

        Find_Button = tk.Button(window, text = "🔍",font = ("Arial",18,"bold"),command= find_quadrant)
        Find_Button.place(x=50,y=80)

        clear_button = tk.Button(window,text = "❌",font = ("Arial",18,),command=clear)
        clear_button.place(x=130,y=80)

        chart = tk.Button(window,text= "chart",font = ("Arial",16),command= coordinate_chart)
        chart.place(x=200,y= 80)
        result_text = tk.Text(window, font= ("Arial",17))
        result_text.place(x=5,y=145,height= 40,width=290)


        window.mainloop()

def two_points():
        main_window.destroy()                    
        def clear():
                entry_y1.delete(0,"end")
                entry_x1.delete(0,"end")
                entry_y2.delete(0,"end")
                entry_x2.delete(0,"end")
                
                entry_x1.focus_set()
                plt.close()
       
        def coordinate_chart(event=None):
                x= [int(entry_x1.get()),int(entry_x2.get())]
                y=[int(entry_y1.get()),int(entry_y2.get())]
                plt.plot(x, y, marker = "o", color ="red")
                plt.axhline(0,color = "black",linewidth=1)
                plt.axvline(0,color="black",linewidth=1)

                plt.grid(True)
                plt.xlabel("X")
                plt.ylabel("Y")
                plt.title("Coordinate")
                plt.show()
        window = tk.Tk()
        window.title("Coordinate chart")
        window.geometry("300x240")

        label_x1 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x1.place(x=5,y=20,height=45,width=45)

        entry_x1 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x1.place(x=50,y=20,height=45,width=80)
        entry_x1.focus_set()

        label_y1 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y1.place(x=155,y=20,height=45,width=45)

        entry_y1 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y1.place(x=200,y=20,height=45,width=80)
###############################################################################################
        label_x2 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x2.place(x=5,y=75,height=45,width=45)

        entry_x2 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x2.place(x=50,y=75,height=45,width=80)
        entry_x2.focus_set()
        

        label_y2 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y2.place(x=155,y=75,height=45,width=45)

        entry_y2 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y2.place(x=200,y=75,height=45,width=80)

        Find_Button = tk.Button(window, text = "🔍",font = ("Arial",18,"bold"),command=coordinate_chart)
        Find_Button.place(x=95,y=140)

        clear_button = tk.Button(window,text = "❌",font = ("Arial",18,),command=clear)
        clear_button.place(x=175,y=140)


        window.mainloop()

def three_points():               
        main_window.destroy()                    
        def clear():
                entry_y1.delete(0,"end")
                entry_x1.delete(0,"end")
                entry_y2.delete(0,"end")
                entry_x2.delete(0,"end")
                entry_y3.delete(0,"end")
                entry_x3.delete(0,"end")
                entry_x1.focus_set()
                plt.close()
       
        def coordinate_chart(event=None):
                x= [int(entry_x1.get()),int(entry_x2.get()),int(entry_x3.get())]
                y=[int(entry_y1.get()),int(entry_y2.get()),int(entry_y3.get())]
                plt.plot(x, y, marker = "o", color ="red")
                plt.axhline(0,color = "black",linewidth=1)
                plt.axvline(0,color="black",linewidth=1)

                plt.grid(True)
                plt.xlabel("X")
                plt.ylabel("Y")
                plt.title("Coordinate")
                plt.show()
        window = tk.Tk()
        window.title("Coordinate chart")
        window.geometry("300x340")

        label_x1 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x1.place(x=5,y=20,height=45,width=45)

        entry_x1 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x1.place(x=50,y=20,height=45,width=80)
        entry_x1.focus_set()

        label_y1 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y1.place(x=155,y=20,height=45,width=45)

        entry_y1 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y1.place(x=200,y=20,height=45,width=80)
###############################################################################################
        label_x2 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x2.place(x=5,y=75,height=45,width=45)

        entry_x2 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x2.place(x=50,y=75,height=45,width=80)
        entry_x2.focus_set()
        

        label_y2 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y2.place(x=155,y=75,height=45,width=45)

        entry_y2 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y2.place(x=200,y=75,height=45,width=80)
##################################################################################################
        label_x3 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x3.place(x=5,y=130,height=45,width=45)

        entry_x3 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x3.place(x=50,y=130,height=45,width=80)
        entry_x3.focus_set()
        

        label_y3 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y3.place(x=155,y=130,height=45,width=45)

        entry_y3 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y3.place(x=200,y=130,height=45,width=80)

        Find_Button = tk.Button(window, text = "🔍",font = ("Arial",18,"bold"),command=coordinate_chart)
        Find_Button.place(x=95,y=185)

        clear_button = tk.Button(window,text = "❌",font = ("Arial",18,),command=clear)
        clear_button.place(x=175,y=185)


        window.mainloop()

def four_points():               
        main_window.destroy()                    
        def clear():
                entry_y1.delete(0,"end")
                entry_x1.delete(0,"end")
                entry_y2.delete(0,"end")
                entry_x2.delete(0,"end")
                entry_y3.delete(0,"end")
                entry_x3.delete(0,"end")
                entry_y4.delete(0,"end")
                entry_x4.delete(0,"end")
                entry_x1.focus_set()
                plt.close()
       
        def coordinate_chart(event=None):
                x= [int(entry_x1.get()),int(entry_x2.get()),int(entry_x3.get()),int(entry_x4.get())]
                y=[int(entry_y1.get()),int(entry_y2.get()),int(entry_y3.get()),int(entry_y4.get())]
                plt.plot(x, y, marker = "o", color ="red")
                plt.axhline(0,color = "black",linewidth=1)
                plt.axvline(0,color="black",linewidth=1)

                plt.grid(True)
                plt.xlabel("X")
                plt.ylabel("Y")
                plt.title("Coordinate")
                plt.show()
        window = tk.Tk()
        window.title("Coordinate chart")
        window.geometry("300x340")

        label_x1 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x1.place(x=5,y=20,height=45,width=45)

        entry_x1 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x1.place(x=50,y=20,height=45,width=80)
        entry_x1.focus_set()

        label_y1 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y1.place(x=155,y=20,height=45,width=45)

        entry_y1 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y1.place(x=200,y=20,height=45,width=80)
###############################################################################################
        label_x2 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x2.place(x=5,y=75,height=45,width=45)

        entry_x2 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x2.place(x=50,y=75,height=45,width=80)
        entry_x2.focus_set()
        

        label_y2 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y2.place(x=155,y=75,height=45,width=45)

        entry_y2 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y2.place(x=200,y=75,height=45,width=80)
##################################################################################################
        label_x3 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x3.place(x=5,y=130,height=45,width=45)

        entry_x3 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x3.place(x=50,y=130,height=45,width=80)
        entry_x3.focus_set()
        

        label_y3 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y3.place(x=155,y=130,height=45,width=45)

        entry_y3 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y3.place(x=200,y=130,height=45,width=80)
        ###################################################################################################
        label_x4 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x4.place(x=5,y=185,height=45,width=45)

        entry_x4 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x4.place(x=50,y=185,height=45,width=80)
        entry_x4.focus_set()
        

        label_y4 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y4.place(x=155,y=185,height=45,width=45)

        entry_y4 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y4.place(x=200,y=185,height=45,width=80)


        Find_Button = tk.Button(window, text = "🔍",font = ("Arial",18,"bold"),command=coordinate_chart)
        Find_Button.place(x=95,y=240)

        clear_button = tk.Button(window,text = "❌",font = ("Arial",18,),command=clear)
        clear_button.place(x=175,y=240)

        window.mainloop()

def five_points():               
        main_window.destroy()                    
        def clear():
                entry_y1.delete(0,"end")
                entry_x1.delete(0,"end")

                entry_y2.delete(0,"end")
                entry_x2.delete(0,"end")

                entry_y3.delete(0,"end")
                entry_x3.delete(0,"end")

                entry_y4.delete(0,"end")
                entry_x4.delete(0,"end")

                entry_y5.delete(0,"end")
                entry_x5.delete(0,"end")
                entry_x1.focus_set()
                plt.close()
       
        def coordinate_chart(event=None):
                x= [int(entry_x1.get()),int(entry_x2.get()),int(entry_x3.get()),int(entry_x4.get()),int(entry_x5.get())]
                y=[int(entry_y1.get()),int(entry_y2.get()),int(entry_y3.get()),int(entry_y4.get()),int(entry_y5.get())]
                plt.plot(x, y, marker = "o", color ="red")
                plt.axhline(0,color = "black",linewidth=1)
                plt.axvline(0,color="black",linewidth=1)

                plt.grid(True)
                plt.xlabel("X")
                plt.ylabel("Y")
                plt.title("Coordinate")
                plt.show()
        window = tk.Tk()
        window.title("Coordinate chart")
        window.geometry("300x340")

        label_x1 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x1.place(x=5,y=20,height=45,width=45)

        entry_x1 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x1.place(x=50,y=20,height=45,width=80)
        entry_x1.focus_set()

        label_y1 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y1.place(x=155,y=20,height=45,width=45)

        entry_y1 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y1.place(x=200,y=20,height=45,width=80)
###############################################################################################
        label_x2 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x2.place(x=5,y=75,height=45,width=45)

        entry_x2 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x2.place(x=50,y=75,height=45,width=80)
        entry_x2.focus_set()
        

        label_y2 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y2.place(x=155,y=75,height=45,width=45)

        entry_y2 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y2.place(x=200,y=75,height=45,width=80)
##################################################################################################
        label_x3 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x3.place(x=5,y=130,height=45,width=45)

        entry_x3 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x3.place(x=50,y=130,height=45,width=80)
        entry_x3.focus_set()
        

        label_y3 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y3.place(x=155,y=130,height=45,width=45)

        entry_y3 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y3.place(x=200,y=130,height=45,width=80)
        ###################################################################################################
        label_x4 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x4.place(x=5,y=185,height=45,width=45)

        entry_x4 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x4.place(x=50,y=185,height=45,width=80)
        entry_x4.focus_set()
        

        label_y4 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y4.place(x=155,y=185,height=45,width=45)

        entry_y4 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y4.place(x=200,y=185,height=45,width=80)

        ###################################################################################################
        label_x5 = tk.Label(window,text = "X :",font=("Arial",16,"bold"))
        label_x5.place(x=5,y=240,height=45,width=45)

        entry_x5 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_x5.place(x=50,y=240,height=45,width=80)
        entry_x5.focus_set()
        

        label_y5 = tk.Label(window,text = "Y :",font=("Arial",16,"bold"))
        label_y5.place(x=155,y=240,height=45,width=45)

        entry_y5 = tk.Entry(window,font=("Arial",16,"bold"))
        entry_y5.place(x=200,y=240,height=45,width=80)
        ###############################################################################################
        Find_Button = tk.Button(window, text = "🔍",font = ("Arial",18,"bold"),command=coordinate_chart)
        Find_Button.place(x=95,y=295)

        clear_button = tk.Button(window,text = "❌",font = ("Arial",18,),command=clear)
        clear_button.place(x=175,y=295)

        window.mainloop()
tk.Label(main_window, text="WELCOME",font = ("Arial",20)).pack(pady=10)
tk.Button(main_window,text="One Point",font=("Arial",16),command = one_point).pack()
tk.Button(main_window,text="Two Points",font = ("Arial",16), command = two_points).pack(pady=10)
tk.Button(main_window,text="Three Points",font = ("Arial",16), command = three_points).pack(pady=10)

tk.Button(main_window,text="Four Points",font = ("Arial",16), command = four_points).pack(pady=10)

tk.Button(main_window,text="Five Points",font = ("Arial",16), command = five_points).pack(pady=10)

main_window.mainloop()
```