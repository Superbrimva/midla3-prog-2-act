import tkinter as tk
from tkinter import messagebox

class Application(tk.Tk):
    def __init__(self):
        super().__init__()

        self.title("List Manager")
        self.geometry("400x300")

        self.create_menu()
        self.create_widgets()

    def create_menu(self):
        menubar = tk.Menu(self)

        file_menu = tk.Menu(menubar, tearoff=0)
        file_menu.add_command(label="Open", command=self.open_file)
        file_menu.add_command(label="Save", command=self.save_file)
        menubar.add_cascade(label="File", menu=file_menu)

        edit_menu = tk.Menu(menubar, tearoff=0)
        edit_menu.add_command(label="Add", command=self.add_item)
        edit_menu.add_command(label="Delete", command=self.delete_item)
        edit_menu.add_command(label="Edit", command=self.edit_item)
        menubar.add_cascade(label="Edit", menu=edit_menu)

        help_menu = tk.Menu(menubar, tearoff=0)
        help_menu.add_command(label="About", command=self.show_about)
        menubar.add_cascade(label="Help", menu=help_menu)

        self.config(menu=menubar)

    def create_widgets(self):
        self.frame = tk.Frame(self)
        self.frame.pack(fill=tk.BOTH, expand=True)

        self.listbox = tk.Listbox(self.frame)
        self.listbox.pack(fill=tk.BOTH, expand=True)

    def open_file(self):
        # Implement open file functionality here
        pass

    def save_file(self):
        # Implement save file functionality here
        pass

    def add_item(self):
        item = tk.simpledialog.askstring("Add Item", "Enter item:")
        if item:
            self.listbox.insert(tk.END, item)

    def delete_item(self):
        selected_index = self.listbox.curselection()
        if selected_index:
            self.listbox.delete(selected_index)

    def edit_item(self):
        selected_index = self.listbox.curselection()
        if selected_index:
            item = self.listbox.get(selected_index)
            edited_item = tk.simpledialog.askstring("Edit Item", "Edit item:", initialvalue=item)
            if edited_item:
                self.listbox.delete(selected_index)
                self.listbox.insert(selected_index, edited_item)

    def show_about(self):
        messagebox.showinfo("About", "This is a simple list manager application.")

if __name__ == "__main__":
    app = Application()
    app.mainloop()
