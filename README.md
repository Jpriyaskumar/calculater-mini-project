import tkinter as tk

def click(event):
    global expression
    text = event.widget.cget("text")

    if text == "=":
        try:
            result = eval(expression)
            entry.set(result)
            expression = str(result)
        except:
            entry.set("Error")
            expression = ""

    elif text == "C":
        expression = ""
        entry.set("")

    else:
        expression += text
        entry.set(expression)

root = tk.Tk()
root.title("Calculator")

expression = ""
entry = tk.StringVar()

screen = tk.Entry(root, textvar=entry, font="Arial 20", bd=10, relief=tk.SUNKEN)
screen.grid(row=0, column=0, columnspan=4)

buttons = [
    "7","8","9","/",
    "4","5","6","*",
    "1","2","3","-",
    "C","0","=","+"
]

row = 1
col = 0

for button in buttons:
    b = tk.Button(root, text=button, font="Arial 18", width=5, height=2)
    b.grid(row=row, column=col)
    b.bind("<Button-1>", click)
    col += 1
    if col == 4:
        col = 0
        row += 1

root.mainloop()
