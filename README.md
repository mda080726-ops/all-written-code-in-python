# all-written-code-in-python
#python bill generator using tkinter
'''import tkinter as tk
from tkinter import ttk
from tkinter import messagebox

def calculate_bill():
    try:
        # Get item details and quantities
        item1 = item1_entry.get()
        qty1 = int(qty1_entry.get()) if qty1_entry.get() else 0
        price1 = float(price1_entry.get()) if price1_entry.get() else 0

        item2 = item2_entry.get()
        qty2 = int(qty2_entry.get()) if qty2_entry.get() else 0
        price2 = float(price2_entry.get()) if price2_entry.get() else 0

        item3 = item3_entry.get()
        qty3 = int(qty3_entry.get()) if qty3_entry.get() else 0
        price3 = float(price3_entry.get()) if price3_entry.get() else 0

        # Calculate totals
        total1 = qty1 * price1
        total2 = qty2 * price2
        total3 = qty3 * price3
        grand_total = total1 + total2 + total3

        # Display bill
        bill_text.delete("1.0", tk.END)  # Clear previous bill
        bill_text.insert(tk.END, f"{'Item':<20}{'Qty':<5}{'Price':<10}{'Total':<10}\n")
        bill_text.insert(tk.END, f"{'-'*45}\n") # Separator line
        if item1:
            bill_text.insert(tk.END, f"{item1:<20}{qty1:<5}{price1:<10.2f}{total1:<10.2f}\n")
        if item2:
            bill_text.insert(tk.END, f"{item2:<20}{qty2:<5}{price2:<10.2f}{total2:<10.2f}\n")
        if item3:
            bill_text.insert(tk.END, f"{item3:<20}{qty3:<5}{price3:<10.2f}{total3:<10.2f}\n")
        bill_text.insert(tk.END, f"{'-'*45}\n") # Separator line
        bill_text.insert(tk.END, f"{'Grand Total:':>35} {grand_total:<10.2f}\n")


    except ValueError:
        messagebox.showerror("Error", "Invalid input. Please enter numbers for quantity and price.")

# Create main window
window = tk.Tk()
window.title("Bill Generator")

# Item 1
item1_label = ttk.Label(window, text="Item 1:")
item1_label.grid(row=0, column=0, padx=5, pady=5, sticky="w")
item1_entry = ttk.Entry(window)
item1_entry.grid(row=0, column=1, padx=5, pady=5)
qty1_label = ttk.Label(window, text="Qty:")
qty1_label.grid(row=0, column=2, padx=5, pady=5)
qty1_entry = ttk.Entry(window, width=5)
qty1_entry.grid(row=0, column=3, padx=5, pady=5)
price1_label = ttk.Label(window, text="Price:")
price1_label.grid(row=0, column=4, padx=5, pady=5)
price1_entry = ttk.Entry(window, width=5)
price1_entry.grid(row=0, column=5, padx=5, pady=5)


# Item 2
item2_label = ttk.Label(window, text="Item 2:")
item2_label.grid(row=1, column=0, padx=5, pady=5, sticky="w")
item2_entry = ttk.Entry(window)
item2_entry.grid(row=1, column=1, padx=5, pady=5)
qty2_label = ttk.Label(window, text="Qty:")
qty2_label.grid(row=1, column=2, padx=5, pady=5)
qty2_entry = ttk.Entry(window, width=5)
qty2_entry.grid(row=1, column=3, padx=5, pady=5)
price2_label = ttk.Label(window, text="Price:")
price2_label.grid(row=1, column=4, padx=5, pady=5)
price2_entry = ttk.Entry(window, width=5)
price2_entry.grid(row=1, column=5, padx=5, pady=5)


# Item 3
item3_label = ttk.Label(window, text="Item 3:")
item3_label.grid(row=2, column=0, padx=5, pady=5, sticky="w")
item3_entry = ttk.Entry(window)
item3_entry.grid(row=2, column=1, padx=5, pady=5)
qty3_label = ttk.Label(window, text="Qty:")
qty3_label.grid(row=2, column=2, padx=5, pady=5)
qty3_entry = ttk.Entry(window, width=5)
qty3_entry.grid(row=2, column=3, padx=5, pady=5)
price3_label = ttk.Label(window, text="Price:")
price3_label.grid(row=2, column=4, padx=5, pady=5)
price3_entry = ttk.Entry(window, width=5)
price3_entry.grid(row=2, column=5, padx=5, pady=5)


# Calculate Button
calculate_button = ttk.Button(window, text="Calculate", command=calculate_bill)
calculate_button.grid(row=3, column=0, columnspan=6, pady=10)

# Bill Display
bill_text = tk.Text(window, height=10, width=50)
bill_text.grid(row=4, column=0, columnspan=6, padx=5, pady=5)

window.mainloop()'''


#Create a Image viewer app using python
'''
import tkinter as tk
from tkinter import filedialog
from PIL import Image, ImageTk  # Pillow library for image handling

def open_image():
    filepath = filedialog.askopenfilename(
        title="Select Image",
        filetypes=(("Image files", "*.jpg;*.jpeg;*.png;*.gif;*.bmp"), ("All files", "*.*"))
    )

    if filepath:
        try:
            image = Image.open(filepath)
            # Resize image to fit window (maintain aspect ratio)
            width, height = image.size
            window_width = window.winfo_width()
            window_height = window.winfo_height()

            if width > window_width or height > window_height:
                image = image.resize((window_width, window_height), Image.LANCZOS) # Use a good resampling filter

            photo = ImageTk.PhotoImage(image)
            image_label.config(image=photo)
            image_label.image = photo  # Keep a reference to prevent garbage collection
            window.title(f"Image Viewer - {filepath}") # Set window title

        except Exception as e:
            print(f"Error opening image: {e}")
            tk.messagebox.showerror("Error", f"Could not open image: {e}")

# Create main window
window = tk.Tk()
window.title("Image Viewer")
window.geometry("600x400")  # Set initial window size

# Image label to display images
image_label = tk.Label(window)
image_label.pack(fill=tk.BOTH, expand=True) # Make label expand to fill window

# Menu bar
menubar = tk.Menu(window)
filemenu = tk.Menu(menubar, tearoff=0)
filemenu.add_command(label="Open", command=open_image)
filemenu.add_separator()
filemenu.add_command(label="Exit", command=window.quit)
menubar.add_cascade(label="File", menu=filemenu)
window.config(menu=menubar)

# Make window resizable (important for image resizing)
window.resizable(True, True)

window.mainloop()'''


'''
import tkinter as tk
from tkinter import ttk
from tkinter import messagebox

def register_user():
    username = username_entry.get()
    password = password_entry.get()
    confirm_password = confirm_password_entry.get()
    email = email_entry.get()
    phone = phone_entry.get()
    address = address_text.get("1.0", tk.END).strip()  # Get address from Text widget

    if not username or not password or not confirm_password or not email or not phone or not address:
        messagebox.showerror("Error", "All fields are required.")
        return

    if password != confirm_password:
        messagebox.showerror("Error", "Passwords do not match.")
        return

    # Basic email validation (you can improve this)
    if "@" not in email or "." not in email:
        messagebox.showerror("Error", "Invalid email format.")
        return

    # Basic phone number validation (you can improve this)
    if not phone.isdigit() or len(phone) != 10:  # Example: 10-digit number
        messagebox.showerror("Error", "Invalid phone number format.")
        return

    # Here you would typically save the user data to a database or file.
    # For this example, we'll just display a success message.
    messagebox.showinfo("Success", "Registration successful!")

    # Clear the form after successful registration (optional):
    username_entry.delete(0, tk.END)
    password_entry.delete(0, tk.END)
    confirm_password_entry.delete(0, tk.END)
    email_entry.delete(0, tk.END)
    phone_entry.delete(0, tk.END)
    address_text.delete("1.0", tk.END)


# Create main window
window = tk.Tk()
window.title("Registration Form")

# Labels and Entry fields
username_label = ttk.Label(window, text="Username:")
username_label.grid(row=0, column=0, padx=5, pady=5, sticky="w")
username_entry = ttk.Entry(window)
username_entry.grid(row=0, column=1, padx=5, pady=5)

password_label = ttk.Label(window, text="Password:")
password_label.grid(row=1, column=0, padx=5, pady=5, sticky="w")
password_entry = ttk.Entry(window, show="*")  # Hide password
password_entry.grid(row=1, column=1, padx=5, pady=5)

confirm_password_label = ttk.Label(window, text="Confirm Password:")
confirm_password_label.grid(row=2, column=0, padx=5, pady=5, sticky="w")
confirm_password_entry = ttk.Entry(window, show="*")
confirm_password_entry.grid(row=2, column=1, padx=5, pady=5)

email_label = ttk.Label(window, text="Email:")
email_label.grid(row=3, column=0, padx=5, pady=5, sticky="w")
email_entry = ttk.Entry(window)
email_entry.grid(row=3, column=1, padx=5, pady=5)

phone_label = ttk.Label(window, text="Phone:")
phone_label.grid(row=4, column=0, padx=5, pady=5, sticky="w")
phone_entry = ttk.Entry(window)
phone_entry.grid(row=4, column=1, padx=5, pady=5)

address_label = ttk.Label(window, text="Address:")
address_label.grid(row=5, column=0, padx=5, pady=5, sticky="w")
address_text = tk.Text(window, height=5)  # Use a Text widget for address
address_text.grid(row=5, column=1, padx=5, pady=5)

# Register Button
register_button = ttk.Button(window, text="Register", command=register_user)
register_button.grid(row=6, column=0, columnspan=2, pady=10)


window.mainloop()'''

'''# new learn database
import tkinter as tk
from tkinter import ttk
from tkinter import messagebox
import sqlite3

# ... (database functions from the previous response) ...


def create_database():  # Create the database and table if they don't exist
    conn = sqlite3.connect('my_cafe.db')  # Or your database name
    cursor = conn.cursor()
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS bills (
            id INTEGER PRIMARY KEY AUTOINCREMENT,  -- Auto-incrementing primary key
            vendor TEXT NOT NULL,
            date TEXT NOT NULL,
            amount REAL NOT NULL,        -- REAL for floating-point numbers
            due_date TEXT NOT NULL
        )
    """)

    conn.commit()
    conn.close()

def add_bill_to_db(vendor, date, amount, due_date):
    conn = sqlite3.connect('my_cafe.db')
    cursor = conn.cursor()
    try:
      cursor.execute("INSERT INTO bills (vendor, date, amount, due_date) VALUES (?, ?, ?, ?)", (vendor, date, amount, due_date))
      conn.commit()
    except Exception as e:
      print(f"Database error: {e}") # Print for debugging
      conn.rollback() # Important to prevent partial updates
      raise # Re-raise the exception to be caught by add_bill()
    finally:
      conn.close()

def get_all_bills():
    conn = sqlite3.connect('my_cafe.db')
    cursor = conn.cursor()
    cursor.execute("SELECT vendor, date, amount, due_date FROM bills")  # Select the columns you want to display
    bills = cursor.fetchall()
    conn.close()
    return bills
def add_bill():
    vendor = vendor_entry.get()
    date = date_entry.get()
    amount = amount_entry.get()
    due_date = due_date_entry.get()

    if not vendor or not date or not amount or not due_date:
        messagebox.showerror("Error", "All fields are required.")
        return

    try:
        amount = float(amount)  # Convert amount to a float
    except ValueError:
        messagebox.showerror("Error", "Invalid amount. Please enter a number.")
        return

    try:
        add_bill_to_db(vendor, date, amount, due_date) # Assuming this function handles database interaction
        clear_entries()
        update_bill_list()
        messagebox.showinfo("Success", "Bill added successfully!")
    except Exception as e:
        messagebox.showerror("Error", f"Error adding bill: {e}")


def clear_entries():
    vendor_entry.delete(0, tk.END)
    date_entry.delete(0, tk.END)
    amount_entry.delete(0, tk.END)
    due_date_entry.delete(0, tk.END)


def update_bill_list():
    bill_listbox.delete(0, tk.END)  # Clear current items
    bills = get_all_bills()  # Assuming this function retrieves bills from the database
    for bill in bills:
        bill_listbox.insert(tk.END, bill)  # Insert each bill into the listbox
# Create main window (THIS MUST BE DONE FIRST)
window = tk.Tk()  # Define the window here
window.title("Bill Management System")

# Entry fields for adding bills
vendor_label = ttk.Label(window, text="Vendor:")
vendor_label.grid(row=0, column=0, padx=5, pady=5, sticky="w")
vendor_entry = ttk.Entry(window)
vendor_entry.grid(row=0, column=1, padx=5, pady=5)

date_label = ttk.Label(window, text="Date (YYYY-MM-DD):")
date_label.grid(row=1, column=0, padx=5, pady=5, sticky="w")
date_entry = ttk.Entry(window)
date_entry.grid(row=1, column=1, padx=5, pady=5)

amount_label = ttk.Label(window, text="Amount:")
amount_label.grid(row=2, column=0, padx=5, pady=5, sticky="w")
amount_entry = ttk.Entry(window)
amount_entry.grid(row=2, column=1, padx=5, pady=5)

due_date_label = ttk.Label(window, text="Due Date (YYYY-MM-DD):")
due_date_label.grid(row=3, column=0, padx=5, pady=5, sticky="w")
due_date_entry = ttk.Entry(window)
due_date_entry.grid(row=3, column=1, padx=5, pady=5)

add_button = ttk.Button(window, text="Add Bill", command=add_bill)
add_button.grid(row=4, column=0, columnspan=2, pady=10)

bill_listbox = tk.Listbox(window, width=50)
bill_listbox.grid(row=5, column=0, columnspan=2, padx=5, pady=5)

# ... (rest of the functions: add_bill, clear_entries, update_bill_list, etc.) ...

update_bill_list()  # Populate the listbox initially

window.mainloop()  # Start the Tkinter event loop'''


#Create a quizz game in python using mcq
'''import random

def quiz_game():
    """A simple quiz game."""

    questions = [
        {
            "question": "What is the capital of France?",
            "options": ["A) London", "B) Paris", "C) Rome", "D) Berlin"],
            "correct_answer": "B"
        },
        {
            "question": "Which planet is known as the 'Red Planet'?",
            "options": ["A) Earth", "B) Mars", "C) Venus", "D) Jupiter"],
            "correct_answer": "B"
        },
        {
            "question": "What is 2 + 2?",
            "options": ["A) 3", "B) 4", "C) 5", "D) 6"],
            "correct_answer": "B"
        },
        {
            "question": "What is the largest mammal?",
            "options": ["A) Elephant", "B) Blue Whale", "C) Giraffe", "D) Lion"],
            "correct_answer": "B"
        },
        {
            "question": "Which gas do plants absorb from the atmosphere?",
            "options": ["A) Oxygen", "B) Carbon Dioxide", "C) Nitrogen", "D) Helium"],
            "correct_answer": "B"
        }
    ]

    score = 0
    random.shuffle(questions)  # Shuffle the questions

    for question_data in questions:
        print("\n" + question_data["question"])
        for option in question_data["options"]:
            print(option)

        user_answer = input("Your answer (A, B, C, or D): ").upper()

        if user_answer == question_data["correct_answer"]:
            print("Correct!")
            score += 1
        else:
            print(f"Incorrect. The correct answer is {question_data['correct_answer']}.")

    print(f"\nYour final score is: {score}/{len(questions)}")

if __name__ == "__main__":
    quiz_game()'''


#Creating a macro using sqlite
'''import sqlite3

def my_custom_upper_debug(text):
    """Macro with debug print statement."""
    print(f"Macro 'custom_upper_debug' called with text: {text}") # Debugging line
    if text is None:
        return None
    return str(text).upper()

def my_custom_concat_debug(text1, text2):
    """Macro with debug print statements."""
    print(f"Macro 'custom_concat_debug' called with text1: {text1}, text2: {text2}") # Debugging line
    if text1 is None or text2 is None:
        return None
    return str(text1) + str(text2)

def use_macro(db_path, query):
    try:
        conn = sqlite3.connect(db_path)
        conn.create_function("custom_upper_debug", 1, my_custom_upper_debug) # Use debug version of macro
        conn.create_function("custom_concat_debug", 2, my_custom_concat_debug) # Use debug version of macro
        cursor = conn.cursor()
        cursor.execute(query)
        rows = cursor.fetchall()
        for row in rows:
            print(row)

    except sqlite3.Error as e:
        print(f"Error executing query: {e}")
    finally:
        if conn:
            conn.close()

if __name__ == "__main__":
    db_path = "my_database.db"
    use_macro(db_path, "SELECT custom_upper_debug(name), custom_concat_debug(name, city) FROM test_table;")'''



'''import sqlite3

def create_macro(db_path, macro_name, macro_definition):
    """
    Creates a macro (user-defined function) in a SQLite database.

    Args:
        db_path (str): Path to the SQLite database file.
        macro_name (str): Name of the macro.
        macro_definition (callable): Python function that defines the macro's behavior.
    """
    try:
        conn = sqlite3.connect(db_path)
        conn.create_function(macro_name, -1, macro_definition)  # -1 for variable number of args
        print(f"Macro '{macro_name}' created successfully.")
    except sqlite3.Error as e:
        print(f"Error creating macro: {e}")
    finally:
        if conn:
            conn.close()

def use_macro(db_path, query):
    """
    Executes a query that uses a macro.

    Args:
        db_path (str): Path to the SQLite database file.
        query (str): SQL query containing the macro.
    """
    try:
        conn = sqlite3.connect(db_path)
        cursor = conn.cursor()
        cursor.execute(query)
        rows = cursor.fetchall()
        for row in rows:
            print(row)

    except sqlite3.Error as e:
        print(f"Error executing query: {e}")
    finally:
        if conn:
            conn.close()


# Example usage:
def my_custom_upper(text):
    """Example macro: Converts text to uppercase."""
    if text is None:
        return None
    return str(text).upper()

def my_custom_concat(text1, text2):
    """Example macro: Concatenates two strings."""
    if text1 is None or text2 is None:
        return None
    return str(text1) + str(text2)

if __name__ == "__main__":
    db_path = "my_database.db"  # Replace with your database path

    # Create a simple table for demonstration
    conn = sqlite3.connect(db_path)
    cursor = conn.cursor()
    cursor.execute("CREATE TABLE IF NOT EXISTS test_table (id INTEGER PRIMARY KEY, name TEXT, city TEXT);")
    cursor.execute("INSERT OR IGNORE INTO test_table (name, city) VALUES ('Alice', 'New York'), ('Bob', 'London'), ('Charlie', 'Paris');")
    conn.commit()
    conn.close()


    create_macro(db_path, "custom_upper", my_custom_upper)
    create_macro(db_path, "custom_concat", my_custom_concat)

    # Use the macros in a query
    use_macro(db_path, "SELECT id, custom_upper(name), custom_concat(city, '!') FROM test_table;")

    #Example of a macro with no arguments.
    def my_custom_version():
        return "My custom version 1.0"

    create_macro(db_path, "custom_version", my_custom_version)
    use_macro(db_path, "SELECT custom_version();")'''

'''#my favourite code
# Define a Contact class to store information
class Contact:
  def __init__(self, name, phone):
    self.name = name
    self.phone = phone

# Initialize an empty list to store contacts
contacts = []

def add_contact():
  """Prompts user for contact details and adds them to the list"""
  name = input("Enter contact name: ")
  phone = input("Enter phone number: ")
  contacts.append(Contact(name, phone))
  print("Contact added successfully!")

def view_contacts():
  """Prints all contacts in the list"""
  if not contacts:
    print("There are no contacts in the list.")
    return
  print("Contacts:")
  for i, contact in enumerate(contacts):
    print(f"{i+1}. {contact.name} - {contact.phone}")

def search_contact():
  """Prompts user for name and searches for contact"""
  name = input("Enter contact name to search: ")
  found = False
  for contact in contacts:
    if contact.name.lower() == name.lower():
      print(f"Contact found: {contact.name} - {contact.phone}")
      found = True
      break
  if not found:
    print(f"Contact not found: {name}")

def main():
  while True:
    print("\nContact Book Menu:")
    print("1. Add Contact")
    print("2. View Contacts")
    print("3. Search Contact")
    print("4. Exit")
    choice = input("Enter your choice: ")

    if choice == '1':
      add_contact()
    elif choice == '2':
      view_contacts()
    elif choice == '3':
      search_contact()
    elif choice == '4':
      print("Exiting Contact Book...")
      break
    else:
      print("Invalid choice. Please try again.")

if __name__ == "__main__":
  main()
'''

#macro system using python and tkinter and sqlite
'''
import tkinter as tk
from tkinter import messagebox
import sqlite3
from datetime import datetime

def create_table():
    conn = sqlite3.connect('macro_data.db')
    cursor = conn.cursor()
    cursor.execute(#remenber to use triple quotes from the hasn
        CREATE TABLE IF NOT EXISTS macro_entries (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name TEXT,
            phone TEXT,
            address TEXT,
            date TEXT
        )
    remember to end hash)
    conn.commit()
    conn.close()

def save_data():
    name = name_entry.get()
    phone = phone_entry.get()
    address = address_text.get("1.0", tk.END).strip()
    date = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    if not name or not phone or not address:
        messagebox.showerror("Error", "Please fill in all fields.")
        return

    conn = sqlite3.connect('macro_data.db')
    cursor = conn.cursor()
    try:
        cursor.execute("INSERT INTO macro_entries (name, phone, address, date) VALUES (?, ?, ?, ?)", (name, phone, address, date))
        conn.commit()
        messagebox.showinfo("Success", "Data saved successfully!")
        clear_entries()

    except sqlite3.Error as e:
        messagebox.showerror("Database Error", f"An error occurred: {e}")
    finally:
        conn.close()

def clear_entries():
    name_entry.delete(0, tk.END)
    phone_entry.delete(0, tk.END)
    address_text.delete("1.0", tk.END)

# Create main window
root = tk.Tk()
root.title("Macro Data Entry")

# Create labels and entry fields
name_label = tk.Label(root, text="Name:")
name_label.grid(row=0, column=0, padx=10, pady=5, sticky="w")
name_entry = tk.Entry(root, width=30)
name_entry.grid(row=0, column=1, padx=10, pady=5)

phone_label = tk.Label(root, text="Phone:")
phone_label.grid(row=1, column=0, padx=10, pady=5, sticky="w")
phone_entry = tk.Entry(root, width=30)
phone_entry.grid(row=1, column=1, padx=10, pady=5)

address_label = tk.Label(root, text="Address:")
address_label.grid(row=2, column=0, padx=10, pady=5, sticky="w")
address_text = tk.Text(root, width=30, height=5)
address_text.grid(row=2, column=1, padx=10, pady=5)

# Create buttons
save_button = tk.Button(root, text="Save", command=save_data)
save_button.grid(row=3, column=0, columnspan=2, pady=10)

clear_button = tk.Button(root, text="Clear", command=clear_entries)
clear_button.grid(row=4, column=0, columnspan=2, pady=5)

# Create database table if it doesn't exist
create_table()

# Run the Tkinter event loop
root.mainloop()'''




'''import tkinter as tk
from tkinter import messagebox
import sqlite3
import random

class QuizApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Quiz Application")
        self.root.geometry("600x400")

        self.conn = sqlite3.connect("quiz_database.db")
        self.cursor = self.conn.cursor()
        self.create_table()

        self.questions = self.fetch_questions()
        self.score = 0
        self.current_question_index = 0
        self.answered_questions = 0 # Keep track of answered questions
        self.total_questions = len(self.questions)

        self.question_label = tk.Label(root, text="", wraplength=550, font=("Arial", 16), justify="left")
        self.question_label.pack(pady=20)

        self.answer_buttons = []
        for i in range(4):
            button = tk.Button(root, text="", font=("Arial", 12), width=40, command=lambda i=i: self.check_answer(i))
            button.pack(pady=5)
            self.answer_buttons.append(button)

        self.next_button = tk.Button(root, text="Next Question", font=("Arial", 12), command=self.next_question, state=tk.DISABLED)
        self.next_button.pack(pady=10)

        self.results_label = tk.Label(root, text="", font=("Arial", 14, "bold"), justify="center") # To display results
        self.results_label.pack(pady=20)  # Add some padding

        self.load_question()

    def create_table(self):
        self.cursor.execute("""
            CREATE TABLE IF NOT EXISTS questions (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                question TEXT NOT NULL,
                answer1 TEXT NOT NULL,
                answer2 TEXT NOT NULL,
                answer3 TEXT NOT NULL,
                answer4 TEXT NOT NULL,
                correct_answer INTEGER NOT NULL
            )
        """)
        self.conn.commit()

    def fetch_questions(self):
        self.cursor.execute("SELECT * FROM questions")
        return self.cursor.fetchall()

    def load_question(self):
        if self.current_question_index < len(self.questions):
            question_data = self.questions[self.current_question_index]
            self.question_label.config(text=f"Q{self.current_question_index + 1}: {question_data[1]}")
            options = [question_data[2], question_data[3], question_data[4], question_data[5]]
            random.shuffle(options)
            self.correct_answer_index = options.index(question_data[question_data[6] + 1])
            for i in range(4):
                self.answer_buttons[i].config(text=options[i], state=tk.NORMAL)
            self.next_button.config(state=tk.DISABLED)
            self.results_label.config(text="") # Clear result label
        else:
            self.show_results()

    def check_answer(self, selected_index):
        if selected_index == self.correct_answer_index:
            self.score += 1
            messagebox.showinfo("Correct", "You got it right!")
        else:
            correct_option = self.answer_buttons[self.correct_answer_index]["text"]
            messagebox.showerror("Incorrect", f"Oops! The correct answer was: {correct_option}")
        for button in self.answer_buttons:
            button.config(state=tk.DISABLED)
        self.next_button.config(state=tk.NORMAL)
        self.answered_questions += 1 # Increment counter

    def next_question(self):
        self.current_question_index += 1
        self.load_question()

    def show_results(self):
        """Display results in the Tkinter window."""
        self.question_label.config(text="")  # Clear question
        for button in self.answer_buttons:
            button.pack_forget()  # Hide answer buttons
        self.next_button.pack_forget()    # Hide next button

        result_text = f"You answered all {self.total_questions} questions.\nYour final score is: {self.score}/{self.total_questions}"
        self.results_label.config(text=result_text)
        # You could add a "Restart Quiz" button here if you want

# --- Database Initialization ---
def initialize_database():
    conn = sqlite3.connect("quiz_database.db")
    cursor = conn.cursor()

    # Check if the table is empty
    cursor.execute("SELECT COUNT(*) FROM questions")
    if cursor.fetchone()[0] == 0:
        questions_data = [
            ("What is the capital of India?", "Delhi", "Mumbai", "Kolkata", "Chennai", 1),
            ("Which planet is known as the 'Red Planet'?", "Mars", "Jupiter", "Venus", "Saturn", 1),
            ("What is the chemical symbol for water?", "H₂O", "CO₂", "O₂", "N₂", 1),
            ("Who painted the Mona Lisa?", "Leonardo da Vinci", "Pablo Picasso", "Vincent van Gogh", "Michelangelo", 1),
            ("What is the largest mammal in the world?", "Blue Whale", "African Elephant", "Giraffe", "Hippopotamus", 1)
        ]
        cursor.executemany("INSERT INTO questions (question, answer1, answer2, answer3, answer4, correct_answer) VALUES (?, ?, ?, ?, ?, ?)", questions_data)
        conn.commit()
        print("Quiz questions added to the database.")
    else:
        print("Quiz database already contains questions.")
    conn.close()

if __name__ == "__main__":
    initialize_database()
    root = tk.Tk()
    app = QuizApp(root)
    root.mainloop()
'''
#All student marks distribution using sql
'''
import sqlite3

def create_marksheet_table():
    """
    Creates a marksheet table in an SQLite database.
    """
    try:
        # 1. Connect to the database (or create it if it doesn't exist)
        conn = sqlite3.connect('marksheet.db')
        cursor = conn.cursor()

        # 2. Define the table schema
        table_name = 'marksheet'
        columns = [
            'roll_number INTEGER PRIMARY KEY',  # Changed to roll_number
            'name TEXT NOT NULL',
            'math INTEGER NOT NULL',
            'science INTEGER NOT NULL',
            'english INTEGER NOT NULL',
            'total INTEGER',
            'average REAL',
            'grade TEXT'
        ]

        # Construct the CREATE TABLE statement
        create_table_query = f"CREATE TABLE IF NOT EXISTS {table_name} ("
        create_table_query += ", ".join(columns)
        create_table_query += ")"

        # 3. Execute the CREATE TABLE statement
        cursor.execute(create_table_query)
        print(f"Table '{table_name}' created successfully.")

        # 4. Commit the changes and close the connection
        conn.commit()
        conn.close()

    except sqlite3.Error as e:
        print(f"Error creating table: {e}")
    finally:
        if conn: #check if connection was established
            conn.close()

def insert_marks(roll_number, name, math, science, english):
    """
    Inserts a student's marks into the marksheet table.

    Args:
        roll_number (int): The student's roll number (primary key).
        name (str): The student's name.
        math (int): Marks in Math.
        science (int): Marks in Science.
        english (int): Marks in English.
    """
    try:
        conn = sqlite3.connect('marksheet.db')
        cursor = conn.cursor()

        # Input validation: Check for valid marks (0-100)
        if not all(0 <= mark <= 100 for mark in [math, science, english]):
            print("Error: Marks must be between 0 and 100.")
            conn.close()
            return

        # Calculate total and average
        total = math + science + english
        average = total / 3

        # Determine the grade
        if average >= 90:
            grade = 'A+'
        elif average >= 80:
            grade = 'A'
        elif average >= 70:
            grade = 'B'
        elif average >= 60:
            grade = 'C'
        elif average >= 50:
            grade = 'D'
        else:
            grade = 'F'

        # Construct the INSERT statement
        insert_query = f"""
            INSERT INTO marksheet (roll_number, name, math, science, english, total, average, grade)
            VALUES (?, ?, ?, ?, ?, ?, ?, ?)
        """
        values = (roll_number, name, math, science, english, total, average, grade)

        # Execute the INSERT statement
        cursor.execute(insert_query, values)
        conn.commit()
        print(f"Marks for {name} (Roll Number: {roll_number}) inserted successfully.")
        conn.close()

    except sqlite3.Error as e:
        print(f"Error inserting data: {e}")
        if conn:
            conn.rollback()  # Rollback on error
        conn.close()

def display_marksheet():
    """
    Displays the entire marksheet table.
    """
    try:
        conn = sqlite3.connect('marksheet.db')
        cursor = conn.cursor()

        # Select all data from the marksheet table
        select_query = "SELECT * FROM marksheet"
        cursor.execute(select_query)

        # Fetch all rows
        rows = cursor.fetchall()

        # Print the header
        print("-" * 70)
        print(f"{'Roll Number':<12}{'Name':<20}{'Math':<6}{'Science':<10}{'English':<10}{'Total':<8}{'Average':<10}{'Grade':<5}")
        print("-" * 70)

        # Print the data rows
        if not rows:
            print("No records found in the marksheet table.")
        else:
            for row in rows:
                print(f"{row[0]:<12}{row[1]:<20}{row[2]:<6}{row[3]:<10}{row[4]:<10}{row[5]:<8}{row[6]:<10.2f}{row[7]:<5}") #formatted output

        print("-" * 70)
        conn.close()

    except sqlite3.Error as e:
        print(f"Error displaying data: {e}")
        conn.close()

def get_student_marks(roll_number):
    """
    Retrieves and displays a student's marksheet by roll number.

    Args:
        roll_number (int): The roll number of the student.
    """
    try:
        conn = sqlite3.connect('marksheet.db')
        cursor = conn.cursor()

        # Select data for a specific roll number
        select_query = "SELECT * FROM marksheet WHERE roll_number = ?"
        cursor.execute(select_query, (roll_number,))
        row = cursor.fetchone()  # Fetch only one row

        if row:
            print("-" * 70)
            print(f"{'Roll Number':<12}{'Name':<20}{'Math':<6}{'Science':<10}{'English':<10}{'Total':<8}{'Average':<10}{'Grade':<5}")
            print("-" * 70)
            print(f"{row[0]:<12}{row[1]:<20}{row[2]:<6}{row[3]:<10}{row[4]:<10}{row[5]:<8}{row[6]:<10.2f}{row[7]:<5}")
            print("-" * 70)
        else:
            print(f"No record found for Roll Number: {roll_number}")
        conn.close()

    except sqlite3.Error as e:
        print(f"Error retrieving data: {e}")
        conn.close()

def update_marks(roll_number, math=None, science=None, english=None):
    """
    Updates a student's marks in the marksheet table.  You can update one or more subjects.

    Args:
        roll_number (int): The roll number of the student to update.
        math (int, optional): New Math marks. Defaults to None.
        science (int, optional): New Science marks. Defaults to None.
        english (int, optional): New English marks. Defaults to None.
    """
    try:
        conn = sqlite3.connect('marksheet.db')
        cursor = conn.cursor()

        # Check if the record exists
        select_query = "SELECT * FROM marksheet WHERE roll_number = ?"
        cursor.execute(select_query, (roll_number,))
        if not cursor.fetchone():
            print(f"Error: No record found for Roll Number: {roll_number}")
            conn.close()
            return

        # Construct the UPDATE statement dynamically
        update_query = "UPDATE marksheet SET "
        updates = []
        if math is not None:
            if  0 <= math <= 100:
                updates.append("math = ?")
            else:
                print("Math marks should be between 0 and 100.  Skipping update for Math.")
        if science is not None:
            if  0 <= science <= 100:
                updates.append("science = ?")
            else:
                print("Science marks should be between 0 and 100.  Skipping update for Science.")
        if english is not None:
            if  0 <= english <= 100:
                updates.append("english = ?")
            else:
                print("English marks should be between 0 and 100. Skipping update for English.")

        if not updates:
            print("No valid marks provided for update.")
            conn.close()
            return

        update_query += ", ".join(updates)
        update_query += " WHERE roll_number = ?"

        values = []
        if math is not None and 0 <= math <= 100:
            values.append(math)
        if science is not None and 0 <= science <= 100:
            values.append(science)
        if english is not None and 0 <= english <= 100:
            values.append(english)
        values.append(roll_number) #important, add the roll_number

        # Execute the UPDATE statement
        cursor.execute(update_query, values)

        #Recalculate total, average and grade.
        cursor.execute("SELECT math, science, english FROM marksheet WHERE roll_number = ?", (roll_number,))
        math_marks, science_marks, english_marks = cursor.fetchone()
        total = math_marks + science_marks + english_marks
        average = total/3
        if average >= 90:
            grade = 'A+'
        elif average >= 80:
            grade = 'A'
        elif average >= 70:
            grade = 'B'
        elif average >= 60:
            grade = 'C'
        elif average >= 50:
            grade = 'D'
        else:
            grade = 'F'
        cursor.execute("UPDATE marksheet SET total = ?, average = ?, grade = ? WHERE roll_number = ?", (total, average, grade, roll_number))

        conn.commit()
        print(f"Marks for Roll Number {roll_number} updated successfully.")
        conn.close()

    except sqlite3.Error as e:
        print(f"Error updating data: {e}")
        if conn:
            conn.rollback()
        conn.close()

def delete_student(roll_number):
    """
    Deletes a student's record from the marksheet table.

    Args:
        roll_number (int): The roll number of the student to delete.
    """
    try:
        conn = sqlite3.connect('marksheet.db')
        cursor = conn.cursor()

        # Check if the record exists
        select_query = "SELECT * FROM marksheet WHERE roll_number = ?"
        cursor.execute(select_query, (roll_number,))
        if not cursor.fetchone():
            print(f"Error: No record found for Roll Number: {roll_number}")
            conn.close()
            return

        # Construct the DELETE statement
        delete_query = "DELETE FROM marksheet WHERE roll_number = ?"

        # Execute the DELETE statement
        cursor.execute(delete_query, (roll_number,))
        conn.commit()
        print(f"Record for Roll Number {roll_number} deleted successfully.")
        conn.close()

    except sqlite3.Error as e:
        print(f"Error deleting data: {e}")
        if conn:
            conn.rollback()
        conn.close()

if __name__ == "__main__":
    # Create the marksheet table
    create_marksheet_table()

    # Insert some sample data
    insert_marks(101, 'Alice Smith', 92, 88, 75)
    insert_marks(102, 'Bob Johnson', 65, 78, 82)
    insert_marks(103, 'Charlie Brown', 45, 55, 60)
    insert_marks(104, 'David Miller', 95, 98, 91)
    insert_marks(105, 'Eve Wilson', 70, 72, 68)

    # Display the entire marksheet
    print("\n--- All Student Marks ---")
    display_marksheet()

    # Get and display a specific student's marks
    print("\n--- Student Marks (Roll Number 102) ---")
    get_student_marks(102)

    # Update a student's marks
    print("\n--- Update Marks for Roll Number 103 ---")
    update_marks(103, math=50, english=65)  # Update Math and English marks
    get_student_marks(103) #show updated marks

    # Display the entire marksheet after update
    print("\n--- All Student Marks After Update ---")
    display_marksheet()

    # Delete a student's record
    print("\n--- Delete Student (Roll Number 104) ---")
    delete_student(104)

    # Display the marksheet after deletion
    print("\n--- All Student Marks After Deletion ---")
    display_marksheet()'''



#metro train time table
'''import tkinter as tk
from tkinter import messagebox
import datetime
import random

# Function to calculate and display the actual departure time for metro trains
def display_actual_time():
    """
    Retrieves the metro line/name and scheduled departure time from the input fields.
    Sets the 'actual' departure time to the current system time.
    Displays the metro line/name, scheduled time, and the current actual time in the GUI.
    Handles potential errors in time input format.
    """
    metro_line_name = metro_line_entry.get()
    scheduled_time_str = scheduled_time_entry.get()

    # Basic validation for metro line/name
    if not metro_line_name:
        messagebox.showwarning("Input Error", "Please enter a Metro Line/Name.")
        return

    # Validate and parse the scheduled time
    try:
        # Assuming scheduled time is in HH:MM format
        scheduled_hour, scheduled_minute = map(int, scheduled_time_str.split(':'))
        scheduled_time = datetime.time(scheduled_hour, scheduled_minute)

        # The 'actual_datetime' will now be the current system time
        actual_datetime = datetime.datetime.now()
        actual_time_str = actual_datetime.strftime('%H:%M')

        # Update the display labels
        display_text = f"Metro Line/Name: {metro_line_name}\n" \
                       f"Scheduled Departure: {scheduled_time.strftime('%H:%M')}\n" \
                       f"Actual Departure: {actual_time_str}"
        result_label.config(text=display_text, fg="blue", font=("Arial", 12, "bold"))

    except ValueError:
        messagebox.showerror("Invalid Time", "Please enter Scheduled Departure Time in HH:MM format (e.g., 14:30).")
    except Exception as e:
        messagebox.showerror("An Error Occurred", f"An unexpected error occurred: {e}")

# Set up the main application window
app = tk.Tk()
app.title("Metro Train Info Tracker")
app.geometry("400x300") # Set initial window size
app.resizable(False, False) # Prevent resizing for simplicity

# Configure column and row weights to center widgets (optional, but good practice)
app.columnconfigure(0, weight=1)
app.columnconfigure(1, weight=1)
app.rowconfigure(0, weight=1)
app.rowconfigure(1, weight=1)
app.rowconfigure(2, weight=1)
app.rowconfigure(3, weight=1)
app.rowconfigure(4, weight=1)


# --- Input Widgets ---

# Metro Line/Name
metro_line_label = tk.Label(app, text="Metro Line/Name:", font=("Arial", 10))
metro_line_label.grid(row=0, column=0, padx=10, pady=5, sticky="e")
metro_line_entry = tk.Entry(app, width=20, font=("Arial", 10))
metro_line_entry.grid(row=0, column=1, padx=10, pady=5, sticky="w")

# Scheduled Departure Time
scheduled_time_label = tk.Label(app, text="Scheduled Departure Time (HH:MM):", font=("Arial", 10))
scheduled_time_label.grid(row=1, column=0, padx=10, pady=5, sticky="e")
scheduled_time_entry = tk.Entry(app, width=20, font=("Arial", 10))
scheduled_time_entry.grid(row=1, column=1, padx=10, pady=5, sticky="w")
scheduled_time_entry.insert(0, "08:15") # Pre-fill for convenience with a typical metro time

# --- Button ---
display_button = tk.Button(app, text="Get Actual Time", command=display_actual_time,
                           bg="#4CAF50", fg="white", font=("Arial", 10, "bold"),
                           relief="raised", bd=3, padx=10, pady=5)
display_button.grid(row=2, column=0, columnspan=2, pady=20)

# --- Result Display ---
result_label = tk.Label(app, text="Enter details and click 'Get Actual Time'",
                        font=("Arial", 10), wraplength=350, justify="center")
result_label.grid(row=3, column=0, columnspan=2, padx=10, pady=10)

# Start the Tkinter event loop
app.mainloop()'''

'''import tkinter as tk
from tkinter import messagebox
import datetime

# Pre-defined list of metro trains with their scheduled departure times
metro_data = [
    {"name": "Blue Line", "scheduled": "07:30"},
    {"name": "Green Line", "scheduled": "07:45"},
    {"name": "Yellow Line", "scheduled": "08:00"},
    {"name": "Red Line", "scheduled": "08:15"},
    {"name": "Purple Line", "scheduled": "08:30"},
    {"name": "Orange Line", "scheduled": "08:45"},
    {"name": "Aqua Line", "scheduled": "09:00"},
]

# Function to calculate and display the actual departure time for metro trains
def display_actual_time():
    """
    Iterates through the pre-defined metro train data.
    For each metro, it calculates the 'actual' departure time (which is the current system time).
    Formats and displays all metro train information in the result text area.
    Handles potential errors in time input format.
    """
    # Enable the text widget for editing
    result_text_widget.config(state=tk.NORMAL)
    result_text_widget.delete(1.0, tk.END) # Clear previous results

    current_actual_time = datetime.datetime.now().strftime('%H:%M:%S')
    result_text_widget.insert(tk.END, f"Current System Time: {current_actual_time}\n\n")

    for metro_info in metro_data:
        metro_line_name = metro_info["name"]
        scheduled_time_str = metro_info["scheduled"]

        try:
            # Assuming scheduled time is in HH:MM format
            scheduled_hour, scheduled_minute = map(int, scheduled_time_str.split(':'))
            scheduled_time = datetime.time(scheduled_hour, scheduled_minute)

            # The 'actual_datetime' will now be the current system time
            # For displaying, we'll just show the time at which the button was clicked
            display_actual_time_str = datetime.datetime.now().strftime('%H:%M')

            # Format the display text for each metro
            display_text = f"Metro Line/Name: {metro_line_name}\n" \
                           f"Scheduled Departure: {scheduled_time.strftime('%H:%M')}\n" \
                           f"Actual Departure: {display_actual_time_str}\n" \
                           f"{'-'*30}\n" # Separator for readability
            result_text_widget.insert(tk.END, display_text)

        except ValueError:
            result_text_widget.insert(tk.END, f"Error: Invalid Scheduled Time for {metro_line_name} ({scheduled_time_str}).\n")
        except Exception as e:
            result_text_widget.insert(tk.END, f"An unexpected error occurred for {metro_line_name}: {e}\n")

    # Disable the text widget after updating content
    result_text_widget.config(state=tk.DISABLED)

# Set up the main application window
app = tk.Tk()
app.title("Metro Train Info Tracker")
app.geometry("500x550") # Adjust window size for more content
app.resizable(True, True) # Allow resizing

# Configure column and row weights
app.columnconfigure(0, weight=1)
app.rowconfigure(0, weight=1)
app.rowconfigure(1, weight=1)
app.rowconfigure(2, weight=4) # Give more weight to the result display area

# --- Instruction Label ---
instruction_label = tk.Label(app, text="Click 'Get Actual Time' to see metro departure info.",
                             font=("Arial", 10), wraplength=450, justify="center")
instruction_label.grid(row=0, column=0, padx=10, pady=10, sticky="nsew")

# --- Button ---
display_button = tk.Button(app, text="Get Actual Time", command=display_actual_time,
                           bg="#4CAF50", fg="white", font=("Arial", 10, "bold"),
                           relief="raised", bd=3, padx=10, pady=5)
display_button.grid(row=1, column=0, pady=10)

# --- Result Display Area (Text Widget) ---
result_text_widget = tk.Text(app, wrap="word", font=("Arial", 11), bg="#f0f0f0", bd=2, relief="groove")
result_text_widget.grid(row=2, column=0, padx=10, pady=10, sticky="nsew")
result_text_widget.insert(tk.END, "Metro train information will appear here.")
result_text_widget.config(state=tk.DISABLED) # Make the text widget read-only initially

# Start the Tkinter event loop
app.mainloop()'''
 #Quizz game with timer also


'''
import random
import time # Import the time module for the timer

def run_quiz(questions):
    """
    Runs the quiz game.

    Args:
        questions (list of dict): A list of dictionaries, where each dictionary
                                  represents a question with 'question',
                                  'options', and 'answer' keys.
    """
    score = 0
    # Define the total time limit for the entire quiz in seconds
    TOTAL_TIME_LIMIT = 60 # For example, 60 seconds for the entire quiz

    # Shuffle the questions to make the quiz different each time
    random.shuffle(questions)

    print("Welcome to the Python Quiz Game!\n")
    print(f"You will have a total of {TOTAL_TIME_LIMIT} seconds to complete all questions.\n")

    quiz_start_time = time.time() # Record the start time for the entire quiz

    for i, q in enumerate(questions):
        print(f"Question {i + 1}: {q['question']}")
        for j, option in enumerate(q['options']):
            print(f"  {chr(65 + j)}. {option}") # A, B, C, D options

        # Check if time has run out before asking the next question
        current_time = time.time()
        elapsed_time = current_time - quiz_start_time
        if elapsed_time > TOTAL_TIME_LIMIT:
            print("\nTime's up! You ran out of time before completing all questions.")
            break # Exit the quiz loop if total time is exceeded

        user_answer = input("Your answer (A, B, C, or D): ").strip().upper()

        # Convert user's letter choice to the actual option text
        chosen_option_index = ord(user_answer) - 65
        chosen_option_text = ""
        if 0 <= chosen_option_index < len(q['options']):
            chosen_option_text = q['options'][chosen_option_index]
        else:
            print("Invalid input. Your answer is marked incorrect.") # Handle invalid input gracefully

        if chosen_option_text == q['answer']:
            print("Correct!\n")
            score += 1
        else:
            print(f"Wrong! The correct answer was: {q['answer']}\n")

    quiz_end_time = time.time() # Record the end time for the entire quiz
    total_time_taken = quiz_end_time - quiz_start_time

    print("Quiz Finished!")
    print(f"You got {score} out of {len(questions)} questions correct.")

    if total_time_taken > TOTAL_TIME_LIMIT:
        print(f"Unfortunately, you exceeded the time limit of {TOTAL_TIME_LIMIT} seconds. You took {total_time_taken:.2f} seconds.")
    else:
        print(f"You completed the quiz in {total_time_taken:.2f} seconds.")

    if score == len(questions) and total_time_taken <= TOTAL_TIME_LIMIT:
        print("Congratulations! You got all questions correct within the time limit!")
    elif score >= len(questions) / 2 and total_time_taken <= TOTAL_TIME_LIMIT:
        print("Good job! Keep practicing!")
    elif total_time_taken > TOTAL_TIME_LIMIT:
        print("You can do better! Try to be faster next time.")
    else:
        print("You can do better! Keep learning!")


if __name__ == "__main__":
    # Define your quiz questions here
    # Each question is a dictionary with 'question', 'options', and 'answer'
    quiz_questions = [
        {
            "question": "What is the capital of France?",
            "options": ["Berlin", "Madrid", "Paris", "Rome"],
            "answer": "Paris"
        },
        {
            "question": "Which planet is known as the Red Planet?",
            "options": ["Earth", "Mars", "Jupiter", "Venus"],
            "answer": "Mars"
        },
        {
            "question": "What is the largest ocean on Earth?",
            "options": ["Atlantic Ocean", "Indian Ocean", "Arctic Ocean", "Pacific Ocean"],
            "answer": "Pacific Ocean"
        },
        {
            "question": "Who painted the Mona Lisa?",
            "options": ["Vincent van Gogh", "Pablo Picasso", "Leonardo da Vinci", "Claude Monet"],
            "answer": "Leonardo da Vinci"
        },
        {
            "question": "What is the chemical symbol for water?",
            "options": ["O2", "H2O", "CO2", "NaCl"],
            "answer": "H2O"
        },
        {
            "question": "What is the largest land animal?",
            "options": ["Elephant", "Giraffe", "Blue Whale", "Polar Bear"],
            "answer": "Elephant"
        },
        {
            "question": "What is the highest mountain in the world?",
            "options": ["K2", "Mount Everest", "Kangchenjunga", "Lhotse"],
            "answer": "Mount Everest"
        }
    ]

    run_quiz(quiz_questions)
'''


# Import the App class from kivy.app module
'''from kivy.app import App
# Import the Label widget from kivy.uix.label module
from kivy.uix.label import Label

class BasicKivyApp(App):
    """
    This is the main application class for our Kivy app.
    It inherits from kivy.app.App.
    """

    def build(self):
        """
        The build method is the entry point for your Kivy application.
        It must return a Widget instance, which will be the root widget
        of your application's widget tree.
        """
        # Create a Label widget with the text "Hello, Kivy!"
        # This label will be the root widget of our application.
        return Label(text="Hello, Kivy!")

# This block ensures that the app runs only when the script is executed directly.
if __name__ == "__main__":
    # Create an instance of our BasicKivyApp class
    # and call its run() method to start the Kivy application.
    BasicKivyApp().run()'''


# Import necessary classes from Kivy
'''from kivy.app import App
from kivy.uix.label import Label
from kivy.uix.button import Button
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.textinput import TextInput # Added for another example

class BasicKivyApp(App):
    """
    This is the main application class for our Kivy app.
    It inherits from kivy.app.App.
    """

    def build(self):
        """
        The build method is the entry point for your Kivy application.
        It must return a Widget instance, which will be the root widget
        of your application's widget tree.
        """
        # --- Example 1: Simple Label (as in the original code) ---
        # return Label(text="Hello, Kivy!")

        # --- Example 2: BoxLayout with a Label and a Button ---
        # BoxLayout is a layout widget that arranges children in a box,
        # either horizontally or vertically.
        main_layout = BoxLayout(orientation='vertical', padding=10, spacing=10)

        # Create a Label widget
        self.hello_label = Label(text="Hello from Kivy!",
                                 font_size='24sp',
                                 halign='center',
                                 valign='middle')
        # Bind the label's size to its text size to prevent text cutoff
        self.hello_label.bind(size=self.hello_label.setter('text_size'))


        # Create a Button widget
        action_button = Button(text="Click Me!",
                               font_size='20sp',
                               size_hint=(1, 0.2)) # Take full width, 20% of parent height
        # Bind the button's 'on_press' event to a method
        action_button.bind(on_press=self.on_button_press)

        # Add the label and button to the main layout
        main_layout.add_widget(self.hello_label)
        main_layout.add_widget(action_button)

        # --- Example 3: Adding a TextInput and a dynamic message ---
        self.user_input = TextInput(hint_text="Type something here...",
                                   multiline=False,
                                   font_size='18sp',
                                   size_hint=(1, 0.15))
        self.user_input.bind(text=self.on_text_input)
        main_layout.add_widget(self.user_input)

        self.dynamic_message = Label(text="Input will appear here.",
                                     font_size='16sp',
                                     color=(0.2, 0.8, 0.2, 1)) # Green text
        self.dynamic_message.bind(size=self.dynamic_message.setter('text_size'))
        main_layout.add_widget(self.dynamic_message)


        return main_layout

    def on_button_press(self, instance):
        """
        This method is called when the 'Click Me!' button is pressed.
        It changes the text of the hello_label.
        """
        self.hello_label.text = "Button was clicked!"
        print("Button was clicked!") # Also print to console for debugging

    def on_text_input(self, instance, value):
        """
        This method is called whenever the text in the TextInput changes.
        It updates the dynamic_message label with the current input.
        """
        self.dynamic_message.text = f"You typed: {value}"
        print(f"User input: {value}")


# This block ensures that the app runs only when the script is executed directly.
if __name__ == "__main__":
    # Create an instance of our BasicKivyApp class
    # and call its run() method to start the Kivy application.
    BasicKivyApp().run()'''


#Student management system 
'''import tkinter as tk
from tkinter import ttk, messagebox
import sqlite3

class StudentManagementSystem:
    def _init_(self, root):
        self.root = root
        self.root.title("Student Management System")
        self.root.geometry("1000x500")

        self.roll_no_var = tk.StringVar()
        self.name_var = tk.StringVar()
        self.email_var = tk.StringVar()
        self.gender_var = tk.StringVar()
        self.contact_var = tk.StringVar()
        self.dob_var = tk.StringVar()
        self.search_by = tk.StringVar()
        self.search_txt = tk.StringVar()

        self.create_table()
        self.manage_ui()
        self.fetch_data()

    def create_table(self):
        con = sqlite3.connect("students.db")
        cur = con.cursor()
        cur.execute("""
            CREATE TABLE IF NOT EXISTS students (
                roll_no TEXT PRIMARY KEY,
                name TEXT,
                email TEXT,
                gender TEXT,
                contact TEXT,
                dob TEXT,
                address TEXT
            )
        """)
        con.commit()
        con.close()

    def manage_ui(self):
        # Manage Frame
        manage_frame = tk.Frame(self.root, bd=4, relief=tk.RIDGE)
        manage_frame.place(x=10, y=60, width=330, height=420)

        tk.Label(manage_frame, text="Manage Students", font=("Arial", 14, "bold")).grid(row=0, columnspan=2, pady=10)

        fields = [("Roll No.", self.roll_no_var), ("Name", self.name_var), ("Email", self.email_var),
                  ("Gender", self.gender_var), ("Contact", self.contact_var), ("D.O.B", self.dob_var)]
        
        for idx, (label, var) in enumerate(fields, start=1):
            tk.Label(manage_frame, text=label, font=("Arial", 12)).grid(row=idx, column=0, pady=5, padx=5, sticky="w")
            if label == "Gender":
                gender_combo = ttk.Combobox(manage_frame, textvariable=var, state='readonly', values=["Male", "Female", "Other"])
                gender_combo.grid(row=idx, column=1, pady=5, padx=5)
            else:
                tk.Entry(manage_frame, textvariable=var).grid(row=idx, column=1, pady=5, padx=5)

        tk.Label(manage_frame, text="Address", font=("Arial", 12)).grid(row=7, column=0, pady=5, padx=5, sticky="w")
        self.txt_address = tk.Text(manage_frame, height=3, width=23)
        self.txt_address.grid(row=7, column=1, pady=5, padx=5)

        # Buttons
        btn_frame = tk.Frame(manage_frame)
        btn_frame.place(x=10, y=300, width=300)

        tk.Button(btn_frame, text="Add", command=self.add_student).grid(row=0, column=0, padx=5)
        tk.Button(btn_frame, text="Update", command=self.update_student).grid(row=0, column=1, padx=5)
        tk.Button(btn_frame, text="Delete", command=self.delete_student).grid(row=0, column=2, padx=5)
        tk.Button(btn_frame, text="Clear", command=self.clear_data).grid(row=0, column=3, padx=5)

        # Detail Frame
        detail_frame = tk.Frame(self.root, bd=4, relief=tk.RIDGE)
        detail_frame.place(x=350, y=60, width=630, height=420)

        tk.Label(detail_frame, text="Search By", font=("Arial", 12)).grid(row=0, column=0, padx=5, pady=10, sticky="w")
        search_combo = ttk.Combobox(detail_frame, textvariable=self.search_by, state='readonly', values=["roll_no", "name", "contact"])
        search_combo.grid(row=0, column=1, padx=5)
        tk.Entry(detail_frame, textvariable=self.search_txt).grid(row=0, column=2, padx=5)
        tk.Button(detail_frame, text="Search", command=self.search_data).grid(row=0, column=3, padx=5)
        tk.Button(detail_frame, text="Show All", command=self.fetch_data).grid(row=0, column=4, padx=5)

        # Table Frame
        table_frame = tk.Frame(detail_frame)
        table_frame.place(x=10, y=50, width=600, height=340)

        scroll_x = tk.Scrollbar(table_frame, orient=tk.HORIZONTAL)
        scroll_y = tk.Scrollbar(table_frame, orient=tk.VERTICAL)
        self.student_table = ttk.Treeview(table_frame, columns=("roll_no", "name", "email", "gender", "contact", "dob", "address"),
                                          xscrollcommand=scroll_x.set, yscrollcommand=scroll_y.set)

        scroll_x.pack(side=tk.BOTTOM, fill=tk.X)
        scroll_y.pack(side=tk.RIGHT, fill=tk.Y)
        scroll_x.config(command=self.student_table.xview)
        scroll_y.config(command=self.student_table.yview)

        self.student_table.heading("roll_no", text="Roll No.")
        self.student_table.heading("name", text="Name")
        self.student_table.heading("email", text="E-mail")
        self.student_table.heading("gender", text="Gender")
        self.student_table.heading("contact", text="Contact")
        self.student_table.heading("dob", text="D.O.B")
        self.student_table.heading("address", text="Address")
        self.student_table['show'] = 'headings'

        for col in self.student_table["columns"]:
            self.student_table.column(col, width=100)

        self.student_table.pack(fill=tk.BOTH, expand=1)
        self.student_table.bind("<ButtonRelease-1>", self.get_cursor)

    def add_student(self):
        if self.roll_no_var.get() == "" or self.name_var.get() == "":
            messagebox.showerror("Error", "All fields are required")
            return
        con = sqlite3.connect("students.db")
        cur = con.cursor()
        try:
            cur.execute("INSERT INTO students VALUES (?, ?, ?, ?, ?, ?, ?)", (
                self.roll_no_var.get(),
                self.name_var.get(),
                self.email_var.get(),
                self.gender_var.get(),
                self.contact_var.get(),
                self.dob_var.get(),
                self.txt_address.get("1.0", tk.END).strip()
            ))
            con.commit()
            self.fetch_data()
            self.clear_data()
        except sqlite3.IntegrityError:
            messagebox.showerror("Error", "Roll number already exists")
        con.close()

    def fetch_data(self):
        con = sqlite3.connect("students.db")
        cur = con.cursor()
        cur.execute("SELECT * FROM students")
        rows = cur.fetchall()
        self.student_table.delete(*self.student_table.get_children())
        for row in rows:
            self.student_table.insert('', tk.END, values=row)
        con.close()

    def clear_data(self):
        self.roll_no_var.set("")
        self.name_var.set("")
        self.email_var.set("")
        self.gender_var.set("")
        self.contact_var.set("")
        self.dob_var.set("")
        self.txt_address.delete("1.0", tk.END)

    def get_cursor(self, event):
        selected_row = self.student_table.focus()
        data = self.student_table.item(selected_row)['values']
        if data:
            self.roll_no_var.set(data[0])
            self.name_var.set(data[1])
            self.email_var.set(data[2])
            self.gender_var.set(data[3])
            self.contact_var.set(data[4])
            self.dob_var.set(data[5])
            self.txt_address.delete("1.0", tk.END)
            self.txt_address.insert(tk.END, data[6])

    def update_student(self):
        con = sqlite3.connect("students.db")
        cur = con.cursor()
        cur.execute("""UPDATE students SET name=?, email=?, gender=?, contact=?, dob=?, address=? WHERE roll_no=?""",
                    (
                        self.name_var.get(),
                        self.email_var.get(),
                        self.gender_var.get(),
                        self.contact_var.get(),
                        self.dob_var.get(),
                        self.txt_address.get("1.0", tk.END).strip(),
                        self.roll_no_var.get()
                    ))
        con.commit()
        self.fetch_data()
        self.clear_data()
        con.close()

    def delete_student(self):
        con = sqlite3.connect("students.db")
        cur = con.cursor()
        cur.execute("DELETE FROM students WHERE roll_no=?", (self.roll_no_var.get(),))
        con.commit()
        self.fetch_data()
        self.clear_data()
        con.close()

    def search_data(self):
        con = sqlite3.connect("students.db")
        cur = con.cursor()
        query = f"SELECT * FROM students WHERE {self.search_by.get()} LIKE ?"
        cur.execute(query, ('%' + self.search_txt.get() + '%',))
        rows = cur.fetchall()
        self.student_table.delete(*self.student_table.get_children())
        for row in rows:
            self.student_table.insert('', tk.END, values=row)
        con.close()

if __name__ == "_main_":
    root = tk.Tk()
    app = StudentManagementSystem(root)
    root.mainloop()'''

'''import tkinter as tk
from tkinter import ttk

# --- Data Structure for Questions and Answers ---
questions_data = [
    {
        "question_number": 41,
        "question_text": "Which process is done first in split AC for shifting from one place to another? | কোন জায়গা থেকে অন্য জায়গায় স্থানান্তরিত করার জন্য স্প্লিট এসিতে প্রথমে কোন প্রক্রিয়া করা হয়?",
        "options": [
            {"text": "A) Flushing | ফ্লাসিং", "value": "flushing"},
            {"text": "B) Evacuation | অপসারণ", "value": "evacuation"},
            {"text": "C) Pump down | পাম্প ডাউন", "value": "pump_down"},
            {"text": "D) Charging | চার্জিং", "value": "charging"}
        ],
        "correct_answer": "pump_down"
    },
    {
        "question_number": 42,
        "question_text": "What is the primary function of a capacitor in an AC motor? | একটি এসি মোটরের ক্যাপাসিটরের প্রধান কাজ কি?",
        "options": [
            {"text": "A) To store voltage", "value": "store_voltage"},
            {"text": "B) To improve power factor", "value": "improve_power_factor"},
            {"text": "C) To start the motor", "value": "start_motor"},
            {"text": "D) To regulate current", "value": "regulate_current"}
        ],
        "correct_answer": "start_motor"
    },
    {
        "question_number": 43,
        "question_text": "Which refrigerant is commonly used in modern refrigerators? | আধুনিক রেফ্রিজারেটরে সাধারণত কোন রেফ্রিজারেন্ট ব্যবহার করা হয়?",
        "options": [
            {"text": "A) R-22", "value": "r22"},
            {"text": "B) R-134a", "value": "r134a"},
            {"text": "C) R-410A", "value": "r410a"},
            {"text": "D) Ammonia", "value": "ammonia"}
        ],
        "correct_answer": "r134a"
    },
    {
        "question_number": 44,
        "question_text": "What is the purpose of a thermostatic expansion valve (TXV) in a refrigeration system? | রেফ্রিজারেশন সিস্টেমে থার্মোস্ট্যাটিক এক্সপেনশন ভালভের (TXV) উদ্দেশ্য কী?",
        "options": [
            {"text": "A) To increase refrigerant pressure", "value": "increase_pressure"},
            {"text": "B) To control refrigerant flow to the evaporator", "value": "control_flow"},
            {"text": "C) To filter out impurities", "value": "filter_impurities"},
            {"text": "D) To cool the compressor", "value": "cool_compressor"}
        ],
        "correct_answer": "control_flow"
    },
    {
        "question_number": 45,
        "question_text": "Which component typically condenses refrigerant vapor into liquid? | কোন উপাদানটি সাধারণত রেফ্রিজারেন্ট বাষ্পকে তরলে ঘনীভূত করে?",
        "options": [
            {"text": "A) Evaporator", "value": "evaporator"},
            {"text": "B) Compressor", "value": "compressor"},
            {"text": "C) Condenser", "value": "condenser"},
            {"text": "D) Drier", "value": "drier"}
        ],
        "correct_answer": "condenser"
    },
    {
        "question_number": 46,
        "question_text": "What is the purpose of a drier/filter in an HVAC system? | HVAC সিস্টেমে একটি ড্রায়ার/ফিল্টারের উদ্দেশ্য কী?",
        "options": [
            {"text": "A) To remove moisture and contaminants", "value": "remove_moisture"},
            {"text": "B) To increase refrigerant pressure", "value": "increase_pressure"},
            {"text": "C) To store excess refrigerant", "value": "store_refrigerant"},
            {"text": "D) To reduce noise levels", "value": "reduce_noise"}
        ],
        "correct_answer": "remove_moisture"
    },
    {
        "question_number": 47,
        "question_text": "Which tool is used to measure the vacuum in a refrigeration system? | রেফ্রিজারেশন সিস্টেমে শূন্যতা পরিমাপ করতে কোন সরঞ্জাম ব্যবহার করা হয়?",
        "options": [
            {"text": "A) Manifold gauge", "value": "manifold_gauge"},
            {"text": "B) Micron gauge", "value": "micron_gauge"},
            {"text": "C) Thermometer", "value": "thermometer"},
            {"text": "D) Ammeter", "value": "ammeter"}
        ],
        "correct_answer": "micron_gauge"
    },
    {
        "question_number": 48,
        "question_text": "What is the typical working pressure of the low-side in an R-22 system during operation? | অপারেশন চলাকালীন একটি R-22 সিস্টেমে লো-সাইডের সাধারণ কার্যকারী চাপ কত?",
        "options": [
            {"text": "A) 0-10 PSI", "value": "0-10_psi"},
            {"text": "B) 20-30 PSI", "value": "20-30_psi"},
            {"text": "C) 60-70 PSI", "value": "60-70_psi"},
            {"text": "D) 100-120 PSI", "value": "100-120_psi"}
        ],
        "correct_answer": "60-70_psi"
    },
    {
        "question_number": 49,
        "question_text": "Which type of motor is commonly found in window AC units? | উইন্ডো এসি ইউনিটে সাধারণত কোন ধরনের মোটর পাওয়া যায়?",
        "options": [
            {"text": "A) DC motor", "value": "dc_motor"},
            {"text": "B) Stepper motor", "value": "stepper_motor"},
            {"text": "C) PSC motor (Permanent Split Capacitor)", "value": "psc_motor"},
            {"text": "D) Universal motor", "value": "universal_motor"}
        ],
        "correct_answer": "psc_motor"
    },
    {
        "question_number": 50,
        "question_text": "What is the primary danger of working with refrigerant without proper ventilation? | সঠিক বায়ুচলাচল ছাড়া রেফ্রিজারেন্ট নিয়ে কাজ করার প্রধান বিপদ কী?",
        "options": [
            {"text": "A) Electric shock", "value": "electric_shock"},
            {"text": "B) Explosion", "value": "explosion"},
            {"text": "C) Asphyxiation (lack of oxygen)", "value": "asphyxiation"},
            {"text": "D) Frostbite", "value": "frostbite"}
        ],
        "correct_answer": "asphyxiation"
    }
]

total_questions = len(questions_data)
current_question_index = 0  # Start with the first question (index 0)

# Dictionary to store user's answers (maps question_number to selected_value)
user_answers = {q["question_number"]: "" for q in questions_data}
question_buttons = {}  # Store references to the question grid buttons


def submit_answer():
    print("Submit button clicked! User Answers:", user_answers)
    # Add logic here to process the selected answer, calculate score, etc.
    # For example, to check answers:
    correct_count = 0
    for q_data in questions_data:
        q_num = q_data["question_number"]
        if user_answers.get(q_num) == q_data["correct_answer"]:
            correct_count += 1
    print(f"You answered {correct_count} out of {total_questions} questions correctly!")
    tk.messagebox.showinfo("Exam Result", f"You answered {correct_count} out of {total_questions} questions correctly!")


def previous_question():
    global current_question_index
    if current_question_index > 0:
        load_question(current_question_index - 1)


def next_question():
    global current_question_index
    if current_question_index < total_questions - 1:
        load_question(current_question_index + 1)


def select_option(value):
    global current_question_index
    current_q_num = questions_data[current_question_index]["question_number"]
    user_answers[current_q_num] = value
    print(f"Question {current_q_num}: Option '{value}' selected. User Answers: {user_answers}")
    update_navigation_grid()  # Update grid color immediately
    update_answered_status()


def load_question(index):
    global current_question_index
    if 0 <= index < total_questions:
        current_question_index = index
        question = questions_data[current_question_index]

        question_number_label.config(text=f"{question['question_number']})")
        question_label.config(text=question['question_text'])

        # Clear existing radio buttons
        for widget in options_frame.winfo_children():
            widget.destroy()

        # Add new radio buttons for the current question
        selected_option.set(
            user_answers.get(question['question_number'], ""))  # Set previously selected answer, or empty string

        for opt in question['options']:
            option_radio = tk.Radiobutton(options_frame, text=opt['text'], variable=selected_option, value=opt['value'],
                                          command=lambda v=opt['value']: select_option(v),
                                          fg="white", bg="#34495e", selectcolor="#2c3e50",
                                          font=("Arial", 12), indicatoron=0, width=30, pady=5, bd=2, relief=tk.FLAT,
                                          activebackground="#1abc9c", activeforeground="white",
                                          highlightbackground="#34495e", highlightthickness=0)
            option_radio.pack(anchor=tk.W, pady=5, padx=10)
            option_radio.bind("<Enter>", lambda e, widget=option_radio: widget.config(bg="#1abc9c"))
            option_radio.bind("<Leave>", lambda e, widget=option_radio: widget.config(bg="#34495e"))

        update_navigation_grid()  # Update grid colors based on answers
        update_answered_status()  # Update answered count

    # Disable/enable Previous/Next buttons
    if current_question_index == 0:
        previous_button.config(state=tk.DISABLED)
    else:
        previous_button.config(state=tk.NORMAL)

    if current_question_index == total_questions - 1:
        next_button.config(state=tk.DISABLED)
    else:
        next_button.config(state=tk.NORMAL)


def update_navigation_grid():
    # Clear existing grid buttons before recreating to reflect states
    for widget in nav_grid_frame.winfo_children():
        widget.destroy()
    question_buttons.clear()  # Clear references

    for i, q_data in enumerate(questions_data):
        q_num = q_data["question_number"]
        row = i // 5  # 5 columns per row
        col = i % 5

        bg_color = ""
        fg_color = "white"

        # Determine color based on answer status
        if user_answers.get(q_num):  # If an answer is stored for this question
            bg_color = "#27ae60"  # Green for answered
        else:
            bg_color = "#ecf0f1"  # Light grey for not answered
            fg_color = "black"

        btn = tk.Button(nav_grid_frame, text=str(q_num), width=5, height=2,
                        bg=bg_color, fg=fg_color, font=("Arial", 10, "bold"), bd=0, relief=tk.FLAT,
                        command=lambda idx=i: load_question(idx))  # Click to jump to question
        btn.grid(row=row, column=col, padx=3, pady=3)
        question_buttons[q_num] = btn  # Store button reference


def update_answered_status():
    answered_count = sum(1 for ans in user_answers.values() if ans)
    not_answered_count = total_questions - answered_count
    answered_label.config(text=f"Answered: {answered_count}")
    not_answered_label.config(text=f"Not Answered: {not_answered_count}")


root = tk.Tk()
root.title("Exam Interface")
root.geometry("900x700")  # Adjust size as needed
root.configure(bg="#2c3e50")

# --- Top Bar ---
top_frame = tk.Frame(root, bg="#34495e", padx=10, pady=5)
top_frame.pack(fill=tk.X, ipady=5)

exam_id_label = tk.Label(top_frame, text="Exam ID: YREF250730161427", fg="white", bg="#34495e", font=("Arial", 10))
exam_id_label.pack(side=tk.LEFT)

total_questions_label = tk.Label(top_frame, text=f"Total Questions: {total_questions}", fg="white", bg="#34495e",
                                 font=("Arial", 10))
total_questions_label.pack(side=tk.LEFT, padx=20)

answered_label = tk.Label(top_frame, text="Answered: 0", fg="white", bg="#34495e", font=("Arial", 10))
answered_label.pack(side=tk.LEFT)

not_answered_label = tk.Label(top_frame, text="Not Answered: 0", fg="white", bg="#34495e", font=("Arial", 10))
not_answered_label.pack(side=tk.RIGHT)

# --- Question and Options Area ---
main_frame = tk.Frame(root, bg="#34495e", padx=20, pady=20)
main_frame.pack(fill=tk.BOTH, expand=True, padx=10, pady=10)

# Question Frame
question_frame = tk.Frame(main_frame, bg="#2c3e50", bd=2, relief=tk.GROOVE)
question_frame.pack(fill=tk.X, pady=10)

question_number_label = tk.Label(question_frame, text="41)", fg="white", bg="#2c3e50", font=("Arial", 14, "bold"))
question_number_label.pack(side=tk.LEFT, anchor=tk.NW, padx=5, pady=5)

question_text_placeholder = "Loading question..."  # Placeholder
question_label = tk.Label(question_frame, text=question_text_placeholder, fg="white", bg="#2c3e50", font=("Arial", 12),
                          wraplength=550, justify=tk.LEFT)
question_label.pack(side=tk.LEFT, fill=tk.X, expand=True, padx=5, pady=5)

# Options Frame
options_frame = tk.Frame(main_frame, bg="#34495e", pady=10)
options_frame.pack(fill=tk.X)

selected_option = tk.StringVar(value="")  # Variable to hold the selected radio button value

# --- Question Navigation Grid ---
nav_grid_frame = tk.Frame(main_frame, bg="#34495e", pady=10, padx=10)
nav_grid_frame.pack(fill=tk.BOTH, expand=True)

# --- Bottom Bar ---
bottom_frame = tk.Frame(root, bg="#34495e", padx=10, pady=10)
bottom_frame.pack(fill=tk.X, side=tk.BOTTOM)

timer_label = tk.Label(bottom_frame, text="00:00:00", fg="white", bg="#34495e", font=("Arial", 14, "bold"))
timer_label.pack(side=tk.LEFT, padx=10)

submit_button = tk.Button(bottom_frame, text="Submit", command=submit_answer,
                          bg="#e74c3c", fg="white", font=("Arial", 12, "bold"),
                          width=10, height=2, bd=0, relief=tk.FLAT,
                          activebackground="#c0392b", activeforeground="white")
submit_button.pack(side=tk.LEFT, padx=10)

previous_button = tk.Button(bottom_frame, text="Previous", command=previous_question,
                            bg="#1abc9c", fg="white", font=("Arial", 12, "bold"),
                            width=10, height=2, bd=0, relief=tk.FLAT,
                            activebackground="#16a085", activeforeground="white")
previous_button.pack(side=tk.RIGHT, padx=10)

next_button = tk.Button(bottom_frame, text="Next", command=next_question,
                        bg="#1abc9c", fg="white", font=("Arial", 12, "bold"),
                        width=10, height=2, bd=0, relief=tk.FLAT,
                        activebackground="#16a085", activeforeground="white")
next_button.pack(side=tk.RIGHT)

# Initial load of the first question and grid
load_question(current_question_index)
update_answered_status()  # Initialize answered/not answered counts


# Placeholder for a simple timer function (optional)
def update_timer(seconds=0):
    minutes, secs = divmod(seconds, 60)
    hours, minutes = divmod(minutes, 60)
    timer_label.config(text=f"{hours:02}:{minutes:02}:{secs:02}")
    root.after(1000, lambda: update_timer(seconds + 1))  # Call itself after 1 second


# Uncomment the line below to start the timer
# update_timer()

root.mainloop()'''

#Best program ever for mcq using tkinter
'''
import tkinter as tk
from tkinter import ttk, messagebox  # Import messagebox for pop-up alerts

# --- Data Structure for Questions and Answers ---
questions_data = [
    {
        "question_number": 41,
        "question_text": "Which process is done first in split AC for shifting from one place to another? | কোন জায়গা থেকে অন্য জায়গায় স্থানান্তরিত করার জন্য স্প্লিট এসিতে প্রথমে কোন প্রক্রিয়া করা হয়?",
        "options": [
            {"text": "A) Flushing | ফ্লাসিং", "value": "flushing"},
            {"text": "B) Evacuation | অপসারণ", "value": "evacuation"},
            {"text": "C) Pump down | পাম্প ডাউন", "value": "pump_down"},
            {"text": "D) Charging | চার্জিং", "value": "charging"}
        ],
        "correct_answer": "pump_down",
        "marks": 1
    },
    {
        "question_number": 42,
        "question_text": "What is the primary function of a capacitor in an AC motor? | একটি এসি মোটরের ক্যাপাসিটরের প্রধান কাজ কি?",
        "options": [
            {"text": "A) To store voltage", "value": "store_voltage"},
            {"text": "B) To improve power factor", "value": "improve_power_factor"},
            {"text": "C) To start the motor", "value": "start_motor"},
            {"text": "D) To regulate current", "value": "regulate_current"}
        ],
        "correct_answer": "start_motor",
        "marks": 1
    },
    {
        "question_number": 43,
        "question_text": "Which refrigerant is commonly used in modern refrigerators? | আধুনিক রেফ্রিজারেটরে সাধারণত কোন রেফ্রিজারেন্ট ব্যবহার করা হয়?",
        "options": [
            {"text": "A) R-22", "value": "r22"},
            {"text": "B) R-134a", "value": "r134a"},
            {"text": "C) R-410A", "value": "r410a"},
            {"text": "D) Ammonia", "value": "ammonia"}
        ],
        "correct_answer": "r134a",
        "marks": 1
    },
    {
        "question_number": 44,
        "question_text": "What is the purpose of a thermostatic expansion valve (TXV) in a refrigeration system? | রেফ্রিজারেশন সিস্টেমে থার্মোস্ট্যাটিক এক্সপেনশন ভালভের (TXV) উদ্দেশ্য কী?",
        "options": [
            {"text": "A) To increase refrigerant pressure", "value": "increase_pressure"},
            {"text": "B) To control refrigerant flow to the evaporator", "value": "control_flow"},
            {"text": "C) To filter out impurities", "value": "filter_impurities"},
            {"text": "D) To cool the compressor", "value": "cool_compressor"}
        ],
        "correct_answer": "control_flow",
        "marks": 1
    },
    {
        "question_number": 45,
        "question_text": "Which component typically condenses refrigerant vapor into liquid? | কোন উপাদানটি সাধারণত রেফ্রিজারেন্ট বাষ্পকে তরলে ঘনীভূত করে?",
        "options": [
            {"text": "A) Evaporator", "value": "evaporator"},
            {"text": "B) Compressor", "value": "compressor"},
            {"text": "C) Condenser", "value": "condenser"},
            {"text": "D) Drier", "value": "drier"}
        ],
        "correct_answer": "condenser",
        "marks": 1
    },
    {
        "question_number": 46,
        "question_text": "What is the purpose of a drier/filter in an HVAC system? | HVAC সিস্টেমে একটি ড্রায়ার/ফিল্টারের উদ্দেশ্য কী?",
        "options": [
            {"text": "A) To remove moisture and contaminants", "value": "remove_moisture"},
            {"text": "B) To increase refrigerant pressure", "value": "increase_pressure"},
            {"text": "C) To store excess refrigerant", "value": "store_refrigerant"},
            {"text": "D) To reduce noise levels", "value": "reduce_noise"}
        ],
        "correct_answer": "remove_moisture",
        "marks": 1
    },
    {
        "question_number": 47,
        "question_text": "Which tool is used to measure the vacuum in a refrigeration system? | রেফ্রিজারেশন সিস্টেমে শূন্যতা পরিমাপ করতে কোন সরঞ্জাম ব্যবহার করা হয়?",
        "options": [
            {"text": "A) Manifold gauge", "value": "manifold_gauge"},
            {"text": "B) Micron gauge", "value": "micron_gauge"},
            {"text": "C) Thermometer", "value": "thermometer"},
            {"text": "D) Ammeter", "value": "ammeter"}
        ],
        "correct_answer": "micron_gauge",
        "marks": 1
    },
    {
        "question_number": 48,
        "question_text": "What is the typical working pressure of the low-side in an R-22 system during operation? | অপারেশন চলাকালীন একটি R-22 সিস্টেমে লো-সাইডের সাধারণ কার্যকারী চাপ কত?",
        "options": [
            {"text": "A) 0-10 PSI", "value": "0-10_psi"},
            {"text": "B) 20-30 PSI", "value": "20-30_psi"},
            {"text": "C) 60-70 PSI", "value": "60-70_psi"},
            {"text": "D) 100-120 PSI", "value": "100-120_psi"}
        ],
        "correct_answer": "60-70_psi",
        "marks": 1
    },
    {
        "question_number": 49,
        "question_text": "Which type of motor is commonly found in window AC units? | উইন্ডো এসি ইউনিটে সাধারণত কোন ধরনের মোটর পাওয়া যায়?",
        "options": [
            {"text": "A) DC motor", "value": "dc_motor"},
            {"text": "B) Stepper motor", "value": "stepper_motor"},
            {"text": "C) PSC motor (Permanent Split Capacitor)", "value": "psc_motor"},
            {"text": "D) Universal motor", "value": "universal_motor"}
        ],
        "correct_answer": "psc_motor",
        "marks": 1
    },
    {
        "question_number": 50,
        "question_text": "What is the primary danger of working with refrigerant without proper ventilation? | সঠিক বায়ুচলাচল ছাড়া রেফ্রিজারেন্ট নিয়ে কাজ করার প্রধান বিপদ কী?",
        "options": [
            {"text": "A) Electric shock", "value": "electric_shock"},
            {"text": "B) Explosion", "value": "explosion"},
            {"text": "C) Asphyxiation (lack of oxygen)", "value": "asphyxiation"},
            {"text": "D) Frostbite", "value": "frostbite"}
        ],
        "correct_answer": "asphyxiation",
        "marks": 1
    }
]

total_questions = len(questions_data)
current_question_index = 0  # Start with the first question (index 0)

# Dictionary to store user's answers (maps question_number to selected_value)
user_answers = {q["question_number"]: "" for q in questions_data}
question_buttons = {}  # Store references to the question grid buttons


# --- Functions ---
def submit_answer():
    print("Submit button clicked!")
    # Stop the timer if it's running
    if timer_job_id:
        root.after_cancel(timer_job_id)

    total_marks_possible = sum(q["marks"] for q in questions_data)
    marks_obtained = 0
    results_text = "Exam Results:\n\n"

    for q_data in questions_data:
        q_num = q_data["question_number"]
        user_choice = user_answers.get(q_num, "Not Answered")
        correct_ans = q_data["correct_answer"]
        question_text = q_data["question_text"].split('|')[0].strip()  # Get only English part

        results_text += f"Question {q_num}: {question_text}\n"
        results_text += f"  Your Answer: "
        # Find the text for the user's selected value
        user_answer_text = "Not Answered"
        for opt in q_data["options"]:
            if opt["value"] == user_choice:
                user_answer_text = opt["text"]
                break
        results_text += f"{user_answer_text}\n"

        correct_answer_text = ""
        for opt in q_data["options"]:
            if opt["value"] == correct_ans:
                correct_answer_text = opt["text"]
                break
        results_text += f"  Correct Answer: {correct_answer_text}\n"

        if user_choice == correct_ans:
            marks_obtained += q_data["marks"]
            results_text += "  Status: Correct! ✅\n"
        else:
            results_text += "  Status: Incorrect ❌\n"
        results_text += "-" * 40 + "\n"

    results_text += f"\nTotal Marks Obtained: {marks_obtained} / {total_marks_possible}\n"

    # Display results in a new window
    display_results_window(results_text)

    # Disable further interaction with the quiz (optional)
    disable_quiz_interaction()


def disable_quiz_interaction():
    # Disable all radio buttons
    for widget in options_frame.winfo_children():
        widget.config(state=tk.DISABLED)
    # Disable navigation buttons
    previous_button.config(state=tk.DISABLED)
    next_button.config(state=tk.DISABLED)
    submit_button.config(state=tk.DISABLED)
    # Disable grid buttons
    for btn in question_buttons.values():
        btn.config(state=tk.DISABLED)


def display_results_window(results_text):
    results_window = tk.Toplevel(root)
    results_window.title("Exam Results")
    results_window.geometry("600x500")
    results_window.configure(bg="#2c3e50")

    text_area = tk.Text(results_window, wrap=tk.WORD, bg="#34495e", fg="white",
                        font=("Arial", 11), padx=10, pady=10, relief=tk.FLAT)
    text_area.pack(expand=True, fill=tk.BOTH, padx=10, pady=10)
    text_area.insert(tk.END, results_text)
    text_area.config(state=tk.DISABLED)  # Make text read-only

    # Add a scrollbar
    scrollbar = tk.Scrollbar(text_area, command=text_area.yview)
    scrollbar.pack(side=tk.RIGHT, fill=tk.Y)
    text_area.config(yscrollcommand=scrollbar.set)

    close_button = tk.Button(results_window, text="Close", command=results_window.destroy,
                             bg="#e74c3c", fg="white", font=("Arial", 12, "bold"),
                             width=10, height=1, bd=0, relief=tk.FLAT,
                             activebackground="#c0392b", activeforeground="white")
    close_button.pack(pady=10)


def previous_question():
    global current_question_index
    if current_question_index > 0:
        load_question(current_question_index - 1)


def next_question():
    global current_question_index
    if current_question_index < total_questions - 1:
        load_question(current_question_index + 1)


def select_option(value):
    global current_question_index
    current_q_num = questions_data[current_question_index]["question_number"]
    user_answers[current_q_num] = value
    print(f"Question {current_q_num}: Option '{value}' selected. User Answers: {user_answers}")
    update_navigation_grid()  # Update grid color immediately
    update_answered_status()


def load_question(index):
    global current_question_index
    if 0 <= index < total_questions:
        current_question_index = index
        question = questions_data[current_question_index]

        question_number_label.config(text=f"{question['question_number']})")
        question_label.config(text=question['question_text'])

        # Clear existing radio buttons
        for widget in options_frame.winfo_children():
            widget.destroy()

        # Add new radio buttons for the current question
        selected_option.set(
            user_answers.get(question['question_number'], ""))  # Set previously selected answer, or empty string

        for opt in question['options']:
            option_radio = tk.Radiobutton(options_frame, text=opt['text'], variable=selected_option, value=opt['value'],
                                          command=lambda v=opt['value']: select_option(v),
                                          fg="white", bg="#34495e", selectcolor="#2c3e50",
                                          font=("Arial", 12), indicatoron=0, width=30, pady=5, bd=2, relief=tk.FLAT,
                                          activebackground="#1abc9c", activeforeground="white",
                                          highlightbackground="#34495e", highlightthickness=0)
            option_radio.pack(anchor=tk.W, pady=5, padx=10)
            option_radio.bind("<Enter>", lambda e, widget=option_radio: widget.config(bg="#1abc9c"))
            option_radio.bind("<Leave>", lambda e, widget=option_radio: widget.config(bg="#34495e"))

        update_navigation_grid()  # Update grid colors based on answers
        update_answered_status()  # Update answered count

    # Disable/enable Previous/Next buttons
    if current_question_index == 0:
        previous_button.config(state=tk.DISABLED)
    else:
        previous_button.config(state=tk.NORMAL)

    if current_question_index == total_questions - 1:
        next_button.config(state=tk.DISABLED)
    else:
        next_button.config(state=tk.NORMAL)


def update_navigation_grid():
    # Clear existing grid buttons before recreating to reflect states
    for widget in nav_grid_frame.winfo_children():
        widget.destroy()
    question_buttons.clear()  # Clear references

    for i, q_data in enumerate(questions_data):
        q_num = q_data["question_number"]
        row = i // 5  # 5 columns per row
        col = i % 5

        bg_color = ""
        fg_color = "white"

        # Determine color based on answer status
        if user_answers.get(q_num):  # If an answer is stored for this question
            bg_color = "#27ae60"  # Green for answered
        else:
            # If current question, make it a distinct color (e.g., blue)
            if q_num == questions_data[current_question_index]["question_number"]:
                bg_color = "#3498db"  # Blue for current question
                fg_color = "white"
            else:
                bg_color = "#ecf0f1"  # Light grey for not answered
                fg_color = "black"

        btn = tk.Button(nav_grid_frame, text=str(q_num), width=5, height=2,
                        bg=bg_color, fg=fg_color, font=("Arial", 10, "bold"), bd=0, relief=tk.FLAT,
                        command=lambda idx=i: load_question(idx))  # Click to jump to question
        btn.grid(row=row, column=col, padx=3, pady=3)
        question_buttons[q_num] = btn  # Store button reference


def update_answered_status():
    answered_count = sum(1 for ans in user_answers.values() if ans)
    not_answered_count = total_questions - answered_count
    answered_label.config(text=f"Answered: {answered_count}")
    not_answered_label.config(text=f"Not Answered: {not_answered_count}")


# --- Timer Functionality ---
timer_seconds = 0
timer_job_id = None  # To store the ID returned by root.after


def update_timer():
    global timer_seconds, timer_job_id
    minutes, secs = divmod(timer_seconds, 60)
    hours, minutes = divmod(minutes, 60)
    timer_label.config(text=f"{hours:02}:{minutes:02}:{secs:02}")
    timer_seconds += 1
    timer_job_id = root.after(1000, update_timer)  # Schedule self to run after 1 second


# --- Main Window Setup ---
root = tk.Tk()
root.title("Exam Interface")
root.geometry("900x700")  # Adjust size as needed
root.configure(bg="#2c3e50")

# --- Top Bar ---
top_frame = tk.Frame(root, bg="#34495e", padx=10, pady=5)
top_frame.pack(fill=tk.X, ipady=5)

exam_id_label = tk.Label(top_frame, text="Exam ID: YREF250730161427", fg="white", bg="#34495e", font=("Arial", 10))
exam_id_label.pack(side=tk.LEFT)

total_questions_label = tk.Label(top_frame, text=f"Total Questions: {total_questions}", fg="white", bg="#34495e",
                                 font=("Arial", 10))
total_questions_label.pack(side=tk.LEFT, padx=20)

answered_label = tk.Label(top_frame, text="Answered: 0", fg="white", bg="#34495e", font=("Arial", 10))
answered_label.pack(side=tk.LEFT)

not_answered_label = tk.Label(top_frame, text="Not Answered: 0", fg="white", bg="#34495e", font=("Arial", 10))
not_answered_label.pack(side=tk.RIGHT)

# --- Question and Options Area ---
main_frame = tk.Frame(root, bg="#34495e", padx=20, pady=20)
main_frame.pack(fill=tk.BOTH, expand=True, padx=10, pady=10)

# Question Frame
question_frame = tk.Frame(main_frame, bg="#2c3e50", bd=2, relief=tk.GROOVE)
question_frame.pack(fill=tk.X, pady=10)

question_number_label = tk.Label(question_frame, text="41)", fg="white", bg="#2c3e50", font=("Arial", 14, "bold"))
question_number_label.pack(side=tk.LEFT, anchor=tk.NW, padx=5, pady=5)

question_text_placeholder = "Loading question..."  # Placeholder
question_label = tk.Label(question_frame, text=question_text_placeholder, fg="white", bg="#2c3e50", font=("Arial", 12),
                          wraplength=550, justify=tk.LEFT)
question_label.pack(side=tk.LEFT, fill=tk.X, expand=True, padx=5, pady=5)

# Options Frame
options_frame = tk.Frame(main_frame, bg="#34495e", pady=10)
options_frame.pack(fill=tk.X)

selected_option = tk.StringVar(value="")  # Variable to hold the selected radio button value

# --- Question Navigation Grid ---
nav_grid_frame = tk.Frame(main_frame, bg="#34495e", pady=10, padx=10)
nav_grid_frame.pack(fill=tk.BOTH, expand=True)

# --- Bottom Bar ---
bottom_frame = tk.Frame(root, bg="#34495e", padx=10, pady=10)
bottom_frame.pack(fill=tk.X, side=tk.BOTTOM)

timer_label = tk.Label(bottom_frame, text="00:00:00", fg="white", bg="#34495e", font=("Arial", 14, "bold"))
timer_label.pack(side=tk.LEFT, padx=10)

submit_button = tk.Button(bottom_frame, text="Submit", command=submit_answer,
                          bg="#e74c3c", fg="white", font=("Arial", 12, "bold"),
                          width=10, height=2, bd=0, relief=tk.FLAT,
                          activebackground="#c0392b", activeforeground="white")
submit_button.pack(side=tk.LEFT, padx=10)

previous_button = tk.Button(bottom_frame, text="Previous", command=previous_question,
                            bg="#1abc9c", fg="white", font=("Arial", 12, "bold"),
                            width=10, height=2, bd=0, relief=tk.FLAT,
                            activebackground="#16a085", activeforeground="white")
previous_button.pack(side=tk.RIGHT, padx=10)

next_button = tk.Button(bottom_frame, text="Next", command=next_question,
                        bg="#1abc9c", fg="white", font=("Arial", 12, "bold"),
                        width=10, height=2, bd=0, relief=tk.FLAT,
                        activebackground="#16a085", activeforeground="white")
next_button.pack(side=tk.RIGHT)

# Initial load of the first question and grid
load_question(current_question_index)
update_answered_status()  # Initialize answered/not answered counts
update_timer()  # Start the timer

root.mainloop()'''

'''{
    "question_number": 41,
    "question_text": "question",
    "options": [
        {"text": "A)  | ", "value": ""},
        {"text": "B)  | ", "value": ""},
        {"text": "C)  | ", "value": ""},
        {"text": "D) Charging | চার্জিং", "value": "charging"}
    ],
    "correct_answer": "",
    "marks": 1
},'''

#analog  clock using turtle
'''import turtle
import datetime
import time

# --- Screen Setup ---
# Create a Turtle screen
screen = turtle.Screen()
screen.setup(width=600, height=600)
screen.bgcolor("black")
screen.tracer(0)  # Turn off screen updates for smoother animation

# --- Drawing Pen Setup ---
# Create a turtle for drawing the clock components
pen = turtle.Turtle()
pen.hideturtle()
pen.speed(0)  # Set the fastest speed
pen.pensize(3)

# --- Clock Hands Setup ---
# Create separate turtles for each hand
hour_hand = turtle.Turtle()
minute_hand = turtle.Turtle()
second_hand = turtle.Turtle()

# Configure hour hand
hour_hand.shape("arrow")
hour_hand.color("white")
hour_hand.shapesize(stretch_wid=0.5, stretch_len=6) # Length of hour hand
hour_hand.penup()
hour_hand.goto(0, 0)
hour_hand.pendown()

# Configure minute hand
minute_hand.shape("arrow")
minute_hand.color("white")
minute_hand.shapesize(stretch_wid=0.5, stretch_len=9) # Length of minute hand
minute_hand.penup()
minute_hand.goto(0, 0)
minute_hand.pendown()

# Configure second hand
second_hand.shape("arrow")
second_hand.color("red")
second_hand.shapesize(stretch_wid=0.2, stretch_len=10) # Length of second hand
second_hand.penup()
second_hand.goto(0, 0)
second_hand.pendown()

# --- Functions ---

def draw_clock(hr_turtle, min_turtle, sec_turtle):
    """Draws the static clock face (circle and marks)."""
    pen.penup()
    pen.goto(0, -210) # Position to draw the circle
    pen.pendown()
    pen.color("white")
    pen.circle(210) # Draw the main clock circle

    # Draw hour marks
    pen.penup()
    pen.goto(0, 0)
    pen.setheading(90) # Point upwards
    for _ in range(12):
        pen.forward(180) # Move to inner end of mark
        pen.pendown()
        pen.pensize(5)
        pen.forward(20) # Draw the mark
        pen.penup()
        pen.goto(0, 0) # Return to center
        pen.right(30) # Rotate for next hour (360/12 = 30)

    # Draw minute marks (lighter/smaller)
    pen.penup()
    pen.goto(0, 0)
    pen.setheading(90)
    for _ in range(60):
        pen.forward(195) # Move to inner end of mark
        pen.pendown()
        pen.pensize(1)
        pen.forward(10) # Draw the mark
        pen.penup()
        pen.goto(0, 0)
        pen.right(6) # Rotate for next minute (360/60 = 6)

    # Center dot
    pen.penup()
    pen.goto(0, -5)
    pen.pendown()
    pen.dot(10, "white") # Draw a small dot in the center

def move_hands():
    """Calculates current time and moves the clock hands."""
    current_time = datetime.datetime.now()
    hour = current_time.hour
    minute = current_time.minute
    second = current_time.second

    # Calculate angles for hands
    # Second hand: 6 degrees per second (360/60)
    sec_angle = second * 6
    # Minute hand: 6 degrees per minute + 0.1 degrees per second (360/60 + (6/60))
    min_angle = (minute * 6) + (second * 0.1)
    # Hour hand: 30 degrees per hour + 0.5 degrees per minute (360/12 + (30/60))
    # Adjust for 12-hour format: (hour % 12)
    hr_angle = ((hour % 12) * 30) + (minute * 0.5)

    # Set the heading of the hands (Turtle's 0 is East, 90 is North)
    # We want 90 degrees to be 12 o'clock, so subtract from 90.
    second_hand.setheading(90 - sec_angle)
    minute_hand.setheading(90 - min_angle)
    hour_hand.setheading(90 - hr_angle)

    # Update the screen
    screen.update()

    # Schedule the next update after 1000 milliseconds (1 second)
    screen.ontimer(move_hands, 1000)

# --- Main Program Flow ---
# Draw the static clock face once
draw_clock(hour_hand, minute_hand, second_hand)

# Start moving the hands
move_hands()

# Keep the window open until manually closed
turtle.done()'''

#!/usr/bin/env python3
"""
Simple USSD-like CLI simulator.
Run: python ussd_cli.py
Type the menu number and press Enter. Type 0 to go back, q to quit.
"""
# creating a ussd dailer code in python
'''
import sys
import time

# Example menu tree. Each node is a dict with: text, options (dict of key->child_key), action optional
MENUS = {
    "root": {
        "text": "Welcome to Demo Service\n1. Balance\n2. Data bundles\n3. Buy airtime\n4. Settings\n0. Exit",
        "options": {"1": "balance", "2": "bundles", "3": "airtime", "4": "settings", "0": "exit"}
    },
    "balance": {
        "text": "Your wallet balance is Rs 123.45\n0. Back",
        "options": {"0": "root"},
        "action": "end"
    },
    "bundles": {
        "text": "Data Bundles\n1. 1GB - Rs 49\n2. 3GB - Rs 129\n3. 10GB - Rs 349\n0. Back",
        "options": {"1": "buy_1gb", "2": "buy_3gb", "3": "buy_10gb", "0": "root"}
    },
    "buy_1gb": {
        "text": "Confirm purchase 1GB for Rs 49?\n1. Confirm\n2. Cancel",
        "options": {"1": "purchase_success", "2": "bundles"}
    },
    "buy_3gb": {
        "text": "Confirm purchase 3GB for Rs 129?\n1. Confirm\n2. Cancel",
        "options": {"1": "purchase_success", "2": "bundles"}
    },
    "buy_10gb": {
        "text": "Confirm purchase 10GB for Rs 349?\n1. Confirm\n2. Cancel",
        "options": {"1": "purchase_success", "2": "bundles"}
    },
    "purchase_success": {
        "text": "Purchase successful. Thank you!\n0. Back to main menu",
        "options": {"0": "root"},
        "action": "end"
    },
    "airtime": {
        "text": "Buy airtime\n1. Self\n2. Another number\n0. Back",
        "options": {"1": "airtime_self", "2": "airtime_other", "0": "root"}
    },
    "airtime_self": {
        "text": "Enter amount to buy for yourself (example: 100):",
        "options": {},
        "action": "input_amount_self"
    },
    "airtime_other": {
        "text": "Enter recipient number (example: 9876543210):",
        "options": {},
        "action": "input_recipient"
    },
    "settings": {
        "text": "Settings\n1. Language\n2. Notifications\n0. Back",
        "options": {"1": "language", "2": "notifications", "0": "root"}
    },
    "language": {
        "text": "Select language\n1. English\n2. Hindi\n0. Back",
        "options": {"1": "lang_set", "2": "lang_set", "0": "settings"},
        "action": "set_language"
    },
    "lang_set": {
        "text": "Language updated.\n0. Back",
        "options": {"0": "settings"},
        "action": "end"
    },
    "notifications": {
        "text": "Notifications toggled.\n0. Back",
        "options": {"0": "settings"},
        "action": "end"
    },
    "exit": {
        "text": "Thank you for using Demo Service.",
        "options": {},
        "action": "quit"
    }
}

def clear_console():
    print("\n" * 1)

def display(menu_key):
    node = MENUS[menu_key]
    print("\n" + node["text"])

def handle_action(node_key, answer_stack):
    node = MENUS[node_key]
    action = node.get("action")
    if action == "end":
        # End session style response: show message then return to root
        display(node_key)
        return "END"
    if action == "quit":
        display(node_key)
        print("Session closed.")
        sys.exit(0)
    if action == "input_amount_self":
        # ask for amount
        amt = input("Amount: ").strip()
        if not amt.isdigit():
            print("Invalid amount. Cancelled.")
            return "END"
        display("purchase_success")
        return "END"
    if action == "input_recipient":
        num = input("Recipient number: ").strip()
        if not (num.isdigit() and len(num) >= 6):
            print("Invalid number. Cancelled.")
            return "END"
        amt = input("Amount: ").strip()
        if not amt.isdigit():
            print("Invalid amount. Cancelled.")
            return "END"
        display("purchase_success")
        return "END"
    if action == "set_language":
        # pretend to set language
        display("lang_set")
        return "END"
    return None

def run_cli():
    current = "root"
    history = []
    while True:
        clear_console()
        display(current)
        node = MENUS[current]
        # If node has no selectable options but has an action, call it
        if not node.get("options") and node.get("action"):
            result = handle_action(current, history)
            if result == "END":
                input("\nPress Enter to continue...")
                current = "root"
            continue

        choice = input("\nEnter choice: ").strip()
        if choice.lower() in ("q", "quit"):
            print("Goodbye.")
            break
        if choice == "0":
            # follow 0 mapping if present
            if "0" in node.get("options", {}):
                current = node["options"]["0"]
                continue
            else:
                print("No back from here.")
                time.sleep(1)
                continue
        if choice in node.get("options", {}):
            next_key = node["options"][choice]
            # if the target has an action that immediately ends, show it
            if MENUS[next_key].get("action"):
                res = handle_action(next_key, history)
                if res == "END":
                    input("\nPress Enter to continue...")
                    current = "root"
                    continue
            history.append(current)
            current = next_key
        else:
            print("Invalid choice, try again.")
            time.sleep(1)

if __name__ == "__main__":
    run_cli()'''
'''import tkinter as tk
from tkinter import messagebox
from tkinter import ttk
import json
import os


# Function to save data into a JSON file
def save_data():
    data = {
        "train_number": train_number_var.get(),
        "passenger_name": name_var.get(),
        "age": age_var.get(),
        "gender": gender_var.get(),
        "class": class_var.get(),
        "date_of_journey": doj_var.get()
    }

    file_path = "reservations.json"

    # Load existing data or create new list
    if os.path.exists(file_path):
        with open(file_path, "r") as file:
            reservations = json.load(file)
    else:
        reservations = []

    reservations.append(data)

    with open(file_path, "w") as file:
        json.dump(reservations, file, indent=4)

    messagebox.showinfo("Success", "Reservation saved!")
    clear_form()


# Clear the form after saving
def clear_form():
    train_number_var.set("")
    name_var.set("")
    age_var.set("")
    gender_var.set("")
    class_var.set("")
    doj_var.set("")


# Create the main window
root = tk.Tk()
root.title("Railway Ticket Booking")
root.configure(bg="black")
root.geometry("400x500")

# Variables to store input
train_number_var = tk.StringVar()
name_var = tk.StringVar()
age_var = tk.StringVar()
gender_var = tk.StringVar()
class_var = tk.StringVar()
doj_var = tk.StringVar()

# Labels and entries
fields = [
    ("Train Number", train_number_var),
    ("Passenger Name", name_var),
    ("Age", age_var),
    ("Gender", gender_var),
    ("Class", class_var),
    ("Date of Journey (YYYY-MM-DD)", doj_var)
]

for idx, (label_text, var) in enumerate(fields):
    label = tk.Label(root, text=label_text, fg="white", bg="black", font=("Arial", 20))
    label.pack(pady=(70, 0))
    if label_text in ["Gender", "Class"]:
        if label_text == "Gender":
            combo = ttk.Combobox(root, textvariable=var, values=["Male", "Female", "Other"], state="readonly")
        else:
            combo = ttk.Combobox(root, textvariable=var, values=["General", "Sleeper", "AC"], state="readonly")
        combo.pack(pady=(0, 10))
    else:
        entry = tk.Entry(root, textvariable=var, font=("Arial", 12))
        entry.pack(pady=(10, 10))

# Submit button
submit_btn = tk.Button(root, text="Book Ticket", command=save_data, font=("Arial", 14), bg="#4CAF50", fg="white")
submit_btn.pack(pady=20)

root.mainloop()'''
#Railways resservation using tkinter and sqlite
'''import tkinter as tk
from tkinter import messagebox
from tkinter import ttk
import sqlite3

# Function to create database and table if not exists
def initialize_db():
    conn = sqlite3.connect('reservations.db')
    cursor = conn.cursor()
    cursor.execute(
        CREATE TABLE IF NOT EXISTS reservations (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            train_number TEXT,
            passenger_name TEXT,
            age INTEGER,
            gender TEXT,
            class TEXT,
            date_of_journey TEXT
        )
    #REMEMNER TO PUT TRIPPLE QUOTE)
    conn.commit()
    conn.close()

# Function to save data into the SQLite database
def save_data():
    train_number = train_number_var.get()
    name = name_var.get()
    age = age_var.get()
    gender = gender_var.get()
    ticket_class = class_var.get()
    doj = doj_var.get()

    if not (train_number and name and age and gender and ticket_class and doj):
        messagebox.showwarning("Incomplete Data", "Please fill in all fields.")
        return

    conn = sqlite3.connect('reservations.db')
    cursor = conn.cursor()
    cursor.execute(
        INSERT INTO reservations (train_number, passenger_name, age, gender, class, date_of_journey)
        VALUES (?, ?, ?, ?, ?, ?)
    #triple quote, (train_number, name, age, gender, ticket_class, doj))
    conn.commit()
    conn.close()

    messagebox.showinfo("Success", "Reservation saved in database!")
    clear_form()

# Clear the form after saving
def clear_form():
    train_number_var.set("")
    name_var.set("")
    age_var.set("")
    gender_var.set("")
    class_var.set("")
    doj_var.set("")

# Initialize the database
initialize_db()

# Create the main window
root = tk.Tk()
root.title("Railway Ticket Booking")
root.configure(bg="black")
root.geometry("400x600")

# Variables to store input
train_number_var = tk.StringVar()
name_var = tk.StringVar()
age_var = tk.StringVar()
gender_var = tk.StringVar()
class_var = tk.StringVar()
doj_var = tk.StringVar()

# Labels and entries
fields = [
    ("Train Number", train_number_var),
    ("Passenger Name", name_var),
    ("Age", age_var),
    ("Gender", gender_var),
    ("Class", class_var),
    ("Date of Journey (YYYY-MM-DD)", doj_var)
]

for idx, (label_text, var) in enumerate(fields):
    label = tk.Label(root, text=label_text, fg="white", bg="black", font=("Arial", 14))
    label.pack(pady=(70, 0))
    if label_text in ["Gender", "Class"]:
        if label_text == "Gender":
            combo = ttk.Combobox(root, textvariable=var, values=["Male", "Female", "Other"], state="readonly", font=("Arial", 12))
        else:
            combo = ttk.Combobox(root, textvariable=var, values=["General", "Sleeper", "AC"], state="readonly", font=("Arial", 12))
        combo.pack(pady=(0, 10))
    else:
        entry = tk.Entry(root, textvariable=var, font=("Arial", 12))
        entry.pack(pady=(0, 10))

# Submit button
submit_btn = tk.Button(root, text="Book Ticket", command=save_data, font=("Arial", 14), bg="#4CAF50", fg="white")
submit_btn.pack(pady=20)

root.mainloop()'''
'''

#Atm machine
import tkinter as tk
from tkinter import messagebox
from tkinter import ttk
import sqlite3
from datetime import datetime

# Example user credentials
user_id = 101
user_pin = "1234"
user_id = 102
user_pin = "2915"

# Initialize database and create table if not exists
def initialize_db():
    conn = sqlite3.connect("atm.db")
    cursor = conn.cursor()
    cursor.execute(#triple
        CREATE TABLE IF NOT EXISTS transactions (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            user_id INTEGER,
            transaction_type TEXT,
            amount REAL,
            balance REAL,
            date TEXT
        )
    #triple)
    conn.commit()
    conn.close()


# Get current balance for user
def get_balance():
    conn = sqlite3.connect("atm.db")
    cursor = conn.cursor()
    cursor.execute("SELECT balance FROM transactions WHERE user_id = ? ORDER BY id DESC LIMIT 1", (user_id,))
    result = cursor.fetchone()
    conn.close()
    if result:
        return result[0]
    return 0.0


# Record transaction into database
def record_transaction(transaction_type, amount):
    balance = get_balance()
    if transaction_type == "Deposit":
        balance += amount
    elif transaction_type == "Withdrawal":
        if amount > balance:
            messagebox.showerror("Error", "Insufficient funds!")
            return
        balance -= amount

    date_str = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    conn = sqlite3.connect("atm.db")
    cursor = conn.cursor()
    cursor.execute(#triple
        INSERT INTO transactions (user_id, transaction_type, amount, balance, date)
        VALUES (?, ?, ?, ?, ?)
    #triple, (user_id, transaction_type, amount, balance, date_str))
    conn.commit()
    conn.close()
    messagebox.showinfo("Success", f"{transaction_type} successful!\nNew Balance: ₹{balance:.2f}")
    update_balance_label()


# Deposit money
def deposit():
    try:
        amt = float(amount_var.get())
        if amt <= 0:
            raise ValueError
        record_transaction("Deposit", amt)
    except ValueError:
        messagebox.showerror("Error", "Enter a valid amount")


# Withdraw money
def withdraw():
    try:
        amt = float(amount_var.get())
        if amt <= 0:
            raise ValueError
        record_transaction("Withdrawal", amt)
    except ValueError:
        messagebox.showerror("Error", "Enter a valid amount")


# Update balance display
def update_balance_label():
    balance = get_balance()
    balance_label.config(text=f"Current Balance: ₹{balance:.2f}")


# Verify entered PIN
def verify_pin():
    entered_pin = pin_var.get()
    if entered_pin == user_pin:
        show_transaction_screen()
    else:
        messagebox.showerror("Error", "Incorrect PIN!")


# Show the transaction UI after successful PIN entry
def show_transaction_screen():
    pin_frame.pack_forget()
    transaction_frame.pack(fill="both", expand=True)
    update_balance_label()


# Show transaction history in a new window
def show_transaction_history():
    conn = sqlite3.connect("atm.db")
    cursor = conn.cursor()
    cursor.execute(
        "SELECT transaction_type, amount, balance, date FROM transactions WHERE user_id = ? ORDER BY id DESC",
        (user_id,))
    records = cursor.fetchall()
    conn.close()

    history_window = tk.Toplevel(root)
    history_window.title("Transaction History")
    history_window.geometry("500x400")

    tk.Label(history_window, text="Transaction History", font=("Arial", 16, "bold")).pack(pady=10)

    tree = ttk.Treeview(history_window, columns=("Type", "Amount", "Balance", "Date"), show="headings")
    tree.heading("Type", text="Transaction Type")
    tree.heading("Amount", text="Amount")
    tree.heading("Balance", text="Balance")
    tree.heading("Date", text="Date")

    tree.pack(fill="both", expand=True)

    for record in records:
        tree.insert("", "end", values=record)


# Main window setup
root = tk.Tk()
root.title("ATM Machine")
root.geometry("400x400")
root.configure(bg="black")

# Initialize database
initialize_db()

# Tkinter variables
pin_var = tk.StringVar()
amount_var = tk.StringVar()

# PIN Entry Frame
pin_frame = tk.Frame(root, bg="black")
pin_label = tk.Label(pin_frame, text="Enter PIN", font=("Arial", 16), bg="black", fg="white")
pin_label.pack(pady=20)
pin_entry = tk.Entry(pin_frame, textvariable=pin_var, font=("Arial", 14), show="*")
pin_entry.pack(pady=10)
pin_button = tk.Button(pin_frame, text="Submit", command=verify_pin, font=("Arial", 14), bg="#4CAF50", fg="white")
pin_button.pack(pady=20)
pin_frame.pack(fill="both", expand=True)

# Transaction Frame
transaction_frame = tk.Frame(root, bg="black")

title = tk.Label(transaction_frame, text="ATM Machine", font=("Arial", 20, "bold"), bg="black", fg="white")
title.pack(pady=20)

balance_label = tk.Label(transaction_frame, text="Current Balance: ₹0.00", font=("Arial", 14), bg="black", fg="white")
balance_label.pack(pady=10)

amount_label = tk.Label(transaction_frame, text="Enter Amount", font=("Arial", 12), bg="black", fg="white")
amount_label.pack(pady=(20, 5))

amount_entry = tk.Entry(transaction_frame, textvariable=amount_var, font=("Arial", 14))
amount_entry.pack(pady=(0, 20))

deposit_btn = tk.Button(transaction_frame, text="Deposit", command=deposit, font=("Arial", 14), bg="#4CAF50",
                        fg="white")
deposit_btn.pack(pady=10)

withdraw_btn = tk.Button(transaction_frame, text="Withdraw", command=withdraw, font=("Arial", 14), bg="#f44336",
                         fg="white")
withdraw_btn.pack(pady=10)

check_balance_btn = tk.Button(transaction_frame, text="Check Balance", command=update_balance_label, font=("Arial", 14),
                              bg="#2196F3", fg="white")
check_balance_btn.pack(pady=10)

history_btn = tk.Button(transaction_frame, text="Check History", command=show_transaction_history, font=("Arial", 14),
                        bg="#9C27B0", fg="white")
history_btn.pack(pady=10)

root.mainloop()'''
#student management system
'''import tkinter as tk
from tkinter import messagebox
from tkinter import ttk


class StudentManagementSystem:
    def __init__(self, root):
        self.root = root
        self.root.title("Student Management System")
        self.root.geometry("800x600")
        self.root.configure(bg="#f0f0f0")

        self.is_fullscreen = False

        # --- Configure root window for resizing ---
        self.root.grid_columnconfigure(0, weight=1)
        self.root.grid_rowconfigure(0, weight=0)
        self.root.grid_rowconfigure(1, weight=1)

        # --- Input Frame ---
        self.input_frame = tk.Frame(self.root, bg="#f0f0f0", padx=10, pady=10)
        self.input_frame.grid(row=0, column=0, sticky="ew")

        # --- Table Frame ---
        self.table_frame = tk.Frame(self.root, bg="#e0e0e0", padx=10, pady=10)
        self.table_frame.grid(row=1, column=0, sticky="nsew")

        # --- Configure input frame columns for resizing ---
        self.input_frame.grid_columnconfigure(1, weight=1)
        self.input_frame.grid_columnconfigure(3, weight=1)

        # --- Input Widgets ---
        tk.Label(self.input_frame, text="Name:", bg="#f0f0f0").grid(row=0, column=0, sticky="e")
        self.name_entry = tk.Entry(self.input_frame)
        self.name_entry.grid(row=0, column=1, padx=5, pady=5, sticky="ew")

        tk.Label(self.input_frame, text="Place:", bg="#f0f0f0").grid(row=1, column=0, sticky="e")
        self.place_entry = tk.Entry(self.input_frame)
        self.place_entry.grid(row=1, column=1, padx=5, pady=5, sticky="ew")

        tk.Label(self.input_frame, text="Mobile:", bg="#f0f0f0").grid(row=2, column=0, sticky="e")
        self.mobile_entry = tk.Entry(self.input_frame)
        self.mobile_entry.grid(row=2, column=1, padx=5, pady=5, sticky="ew")

        tk.Label(self.input_frame, text="Age:", bg="#f0f0f0").grid(row=0, column=2, sticky="e")
        self.age_entry = tk.Entry(self.input_frame)
        self.age_entry.grid(row=0, column=3, padx=5, pady=5, sticky="ew")

        tk.Label(self.input_frame, text="Course:", bg="#f0f0f0").grid(row=1, column=2, sticky="e")
        self.course_entry = tk.Entry(self.input_frame)
        self.course_entry.grid(row=1, column=3, padx=5, pady=5, sticky="ew")

        tk.Label(self.input_frame, text="Email:", bg="#f0f0f0").grid(row=2, column=2, sticky="e")
        self.email_entry = tk.Entry(self.input_frame)
        self.email_entry.grid(row=2, column=3, padx=5, pady=5, sticky="ew")

        # --- Buttons ---
        self.add_button = tk.Button(self.input_frame, text="Add Student", command=self.add_student, bg="#4CAF50",
                                    fg="white")
        self.add_button.grid(row=3, column=1, pady=10)

        self.delete_button = tk.Button(self.input_frame, text="Delete Selected", command=self.delete_selected,
                                       bg="#F44336", fg="white")
        self.delete_button.grid(row=3, column=2, pady=10)

        self.fullscreen_button = tk.Button(self.input_frame, text="Toggle Fullscreen", command=self.toggle_fullscreen,
                                           bg="#2196F3", fg="white")
        self.fullscreen_button.grid(row=3, column=3, pady=10)

        # --- Table View (ttk.Treeview) ---
        columns = ("Name", "Place", "Mobile", "Age", "Course", "Email")
        self.student_table = ttk.Treeview(self.table_frame, columns=columns, show="headings")

        for col in columns:
            self.student_table.heading(col, text=col, command=lambda _col=col: self.sort_column(_col, False))
            self.student_table.column(col, anchor="center")

        self.student_table.pack(side=tk.LEFT, fill=tk.BOTH, expand=True)

        self.scrollbar = ttk.Scrollbar(self.table_frame, orient=tk.VERTICAL, command=self.student_table.yview)
        self.student_table.configure(yscrollcommand=self.scrollbar.set)
        self.scrollbar.pack(side=tk.RIGHT, fill=tk.Y)

    def add_student(self):
        name = self.name_entry.get().strip()
        place = self.place_entry.get().strip()
        mobile = self.mobile_entry.get().strip()
        age = self.age_entry.get().strip()
        course = self.course_entry.get().strip()
        email = self.email_entry.get().strip()

        if name and place and mobile and age and course and email:
            self.student_table.insert("", tk.END, values=(name, place, mobile, age, course, email))
            self.clear_entries()
        else:
            messagebox.showwarning("Incomplete Information", "Please fill in all fields.")

    def delete_selected(self):
        selected_items = self.student_table.selection()
        if not selected_items:
            messagebox.showwarning("No Selection", "Please select a row to delete.")
            return

        if messagebox.askyesno("Confirm Deletion",
                               f"Are you sure you want to delete {len(selected_items)} selected row(s)?"):
            for item in selected_items:
                self.student_table.delete(item)
            messagebox.showinfo("Deletion Complete", f"{len(selected_items)} row(s) deleted successfully.")

    def clear_entries(self):
        self.name_entry.delete(0, tk.END)
        self.place_entry.delete(0, tk.END)
        self.mobile_entry.delete(0, tk.END)
        self.age_entry.delete(0, tk.END)
        self.course_entry.delete(0, tk.END)
        self.email_entry.delete(0, tk.END)

    def toggle_fullscreen(self):
        self.is_fullscreen = not self.is_fullscreen
        self.root.attributes("-fullscreen", self.is_fullscreen)

    def sort_column(self, col, reverse):
        l = [(self.student_table.set(k, col), k) for k in self.student_table.get_children('')]
        l.sort(reverse=reverse)

        for index, (val, k) in enumerate(l):
            self.student_table.move(k, '', index)

        self.student_table.heading(col, command=lambda: self.sort_column(col, not reverse))


# --- Main application loop ---
if __name__ == "__main__":
    root = tk.Tk()
    app = StudentManagementSystem(root)
    root.mainloop()'''
'''import tkinter as tk
from tkinter import messagebox


class CountdownTimer:
    def __init__(self, root):
        self.root = root
        self.root.title("Countdown Timer")
        self.root.geometry("400x200")
        self.root.configure(bg="#f0f0f0")

        self.time_left = 0
        self.is_running = False
        self.timer_id = None

        # --- Frames ---
        self.main_frame = tk.Frame(self.root, bg="#f0f0f0", padx=10, pady=10)
        self.main_frame.pack(expand=True)

        # --- Timer Label ---
        self.timer_label = tk.Label(self.main_frame, text="00:00", font=("Arial", 48), bg="#f0f0f0", fg="#333")
        self.timer_label.pack(pady=10)

        # --- Input and Buttons Frame ---
        self.control_frame = tk.Frame(self.main_frame, bg="#f0f0f0")
        self.control_frame.pack()

        self.entry_label = tk.Label(self.control_frame, text="Set Time (seconds):", bg="#f0f0f0")
        self.entry_label.grid(row=0, column=0, padx=5)

        self.time_entry = tk.Entry(self.control_frame, width=10)
        self.time_entry.grid(row=0, column=1, padx=5)

        self.set_button = tk.Button(self.control_frame, text="Set & Start", command=self.set_time, bg="#4CAF50",
                                    fg="white")
        self.set_button.grid(row=1, column=0, pady=10, padx=5)

        self.pause_button = tk.Button(self.control_frame, text="Pause", command=self.pause_timer, bg="#FF9800",
                                      fg="white")
        self.pause_button.grid(row=1, column=1, pady=10, padx=5)

        self.reset_button = tk.Button(self.control_frame, text="Reset", command=self.reset_timer, bg="#F44336",
                                      fg="white")
        self.reset_button.grid(row=1, column=2, pady=10, padx=5)

    def format_time(self, seconds):
        minutes = seconds // 60
        secs = seconds % 60
        return f"{minutes:02}:{secs:02}"

    def set_time(self):
        if self.is_running:
            self.root.after_cancel(self.timer_id)
            self.is_running = False

        try:
            self.time_left = int(self.time_entry.get())
            if self.time_left <= 0:
                messagebox.showerror("Invalid Input", "Please enter a positive number of seconds.")
                return

            self.timer_label.config(text=self.format_time(self.time_left))
            self.is_running = True
            self.countdown()
        except ValueError:
            messagebox.showerror("Invalid Input", "Please enter a valid number.")

    def countdown(self):
        if self.time_left > 0 and self.is_running:
            self.time_left -= 1
            self.timer_label.config(text=self.format_time(self.time_left))
            self.timer_id = self.root.after(1000, self.countdown)
        elif self.time_left == 0 and self.is_running:
            self.is_running = False
            self.timer_label.config(text="Time's up!")
            messagebox.showinfo("Timer Done", "The countdown has finished!")

    def pause_timer(self):
        if self.is_running:
            self.root.after_cancel(self.timer_id)
            self.is_running = False
        else:
            self.is_running = True
            self.countdown()

    def reset_timer(self):
        if self.is_running:
            self.root.after_cancel(self.timer_id)
        self.is_running = False
        self.time_left = 0
        self.timer_label.config(text="00:00")
        self.time_entry.delete(0, tk.END)


# --- Main application loop ---
if __name__ == "__main__":
    root = tk.Tk()
    app = CountdownTimer(root)
    root.mainloop()'''

'''import tkinter as tk
from tkinter import filedialog
import cv2
from PIL import Image, ImageTk


class VideoPlayerApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Simple Video Player")
        self.root.geometry("800x600")

        self.cap = None
        self.paused = False

        # Create a label to display the video frames
        self.video_label = tk.Label(self.root)
        self.video_label.pack(expand=True, fill="both")

        # Create a button to open and play the video file
        self.load_button = tk.Button(self.root, text="Load & Play Video", command=self.load_video)
        self.load_button.pack(pady=10)

        # Create a button to pause/resume the video
        self.pause_button = tk.Button(self.root, text="Pause", command=self.toggle_pause, state=tk.DISABLED)
        self.pause_button.pack(pady=5)

    def load_video(self):
        # Open a file dialog to select a video file
        file_path = filedialog.askopenfilename(
            filetypes=[("Video files", "*.mp4 *.avi *.mov *.mkv")]
        )
        if not file_path:
            return

        # Initialize the video capture object
        if self.cap is not None:
            self.cap.release()
        self.cap = cv2.VideoCapture(file_path)

        # Check if the video file was opened successfully
        if not self.cap.isOpened():
            print("Error: Could not open video file.")
            self.cap = None
            return

        # Enable the pause button
        self.pause_button.config(state=tk.NORMAL)
        self.paused = False
        self.update_frame()

    def update_frame(self):
        if self.cap is None or self.paused:
            return

        # Read a frame from the video capture
        ret, frame = self.cap.read()

        if ret:
            # Convert the frame from BGR to RGB
            frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

            # Convert the frame to a PIL Image
            img = Image.fromarray(frame)

            # Resize the image to fit the label, maintaining aspect ratio
            img_width, img_height = img.size
            label_width = self.video_label.winfo_width()
            label_height = self.video_label.winfo_height()

            if img_width > 0 and img_height > 0:
                aspect_ratio = img_width / img_height
                if label_width / label_height > aspect_ratio:
                    new_width = int(label_height * aspect_ratio)
                    new_height = label_height
                else:
                    new_width = label_width
                    new_height = int(label_width / aspect_ratio)
                img = img.resize((new_width, new_height), Image.LANCZOS)

            # Convert the PIL Image to a Tkinter PhotoImage
            img_tk = ImageTk.PhotoImage(image=img)

            # Update the label with the new frame
            self.video_label.config(image=img_tk)
            self.video_label.image = img_tk  # Keep a reference to prevent garbage collection

            # Schedule the next frame update after a short delay (e.g., 15 ms)
            self.root.after(15, self.update_frame)
        else:
            # End of video file
            self.cap.release()
            self.cap = None
            self.pause_button.config(state=tk.DISABLED)

    def toggle_pause(self):
        self.paused = not self.paused
        if self.paused:
            self.pause_button.config(text="Resume")
        else:
            self.pause_button.config(text="Pause")
            self.update_frame()


if __name__ == "__main__":
    root = tk.Tk()
    app = VideoPlayerApp(root)
    root.mainloop()'''

'''
import random

def slot_machine():
    symbols = ["🍒", "🍋", "🔔", "⭐", "7️⃣"]
    balance = 100

    print("Welcome to the Slot Machine!")
    print("You start with 100 coins.")

    while balance > 0:
        print(f"\nYour balance: {balance} coins")
        bet = int(input("Enter your bet (0 to quit): "))

        if bet == 0:
            print("Thanks for playing! Final balance:", balance)
            break

        if bet > balance:
            print("You don’t have enough coins!")
            continue

        # Spin
        spin = [random.choice(symbols) for _ in range(3)]
        print(" | ".join(spin))

        # Win check
        if spin[0] == spin[1] == spin[2]:
            win = bet * 5
            print(f"Jackpot! You won {win} coins!")
            balance += win
        elif spin[0] == spin[1] or spin[1] == spin[2] or spin[0] == spin[2]:
            win = bet * 2
            print(f"Nice! You matched two symbols and won {win} coins!")
            balance += win
        else:
            print("No match, you lost your bet.")
            balance -= bet

    if balance <= 0:
        print("Game over! You’re out of coins.")

slot_machine()'''

# Atm ui
'''import tkinter as tk
from tkinter import messagebox

# Global balance
balance = 10000

class ATMApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Aamir Bank ATM")
        self.root.geometry("800x600")
        self.root.configure(bg="blue")
        self.pin = "1234"
        self.amount = 0
        self.current_frame = None
        self.show_start_page()

    def clear_frame(self):
        if self.current_frame is not None:
            self.current_frame.destroy()

    def show_start_page(self):  # 1st Page
        self.clear_frame()
        self.current_frame = tk.Frame(self.root, bg="blue")
        self.current_frame.pack(expand=True, fill="both")

        label = tk.Label(self.current_frame, text="Welcome to Aamir Bank", font=("Arial", 28, "bold"), bg="blue", fg="white")
        label.pack(pady=80)

        start_btn = tk.Button(self.current_frame, text="Start", font=("Arial", 20, "bold"), bg="grey", width=15, height=2, command=self.show_pin_page)
        start_btn.pack(pady=40)

    def show_pin_page(self):  # 2nd Page
        self.clear_frame()
        self.current_frame = tk.Frame(self.root, bg="blue")
        self.current_frame.pack(expand=True, fill="both")

        label = tk.Label(self.current_frame, text="Enter PIN", font=("Arial", 24, "bold"), bg="blue", fg="white")
        label.pack(pady=40)

        self.pin_entry = tk.Entry(self.current_frame, show="*", font=("Arial", 20))
        self.pin_entry.pack(pady=20)

        submit_btn = tk.Button(self.current_frame, text="Submit", font=("Arial", 20, "bold"), bg="grey", width=15, height=2, command=self.check_pin)
        submit_btn.pack(pady=40)

    def check_pin(self):
        entered_pin = self.pin_entry.get()
        if entered_pin == self.pin:
            self.show_transaction_page()
        else:
            messagebox.showerror("Error", "Invalid PIN")

    def show_transaction_page(self):  # 3rd Page
        self.clear_frame()
        self.current_frame = tk.Frame(self.root, bg="blue")
        self.current_frame.pack(expand=True, fill="both")

        label = tk.Label(self.current_frame, text="Please Select Transaction", font=("Arial", 24, "bold"), bg="blue", fg="white")
        label.pack(pady=30)

        left_frame = tk.Frame(self.current_frame, bg="blue")
        left_frame.pack(side="left", expand=True, padx=50)

        right_frame = tk.Frame(self.current_frame, bg="blue")
        right_frame.pack(side="right", expand=True, padx=50)

        left_buttons = [
            ("Deposit", self.show_deposit_page),
            ("Pin Change", self.show_pin_change_page),
            ("Others", self.show_others_page)
        ]

        right_buttons = [
            ("Fast Cash", self.show_fast_cash_page),
            ("Withdraw", self.show_account_type_page),
            ("Balance Enquiry", self.show_balance_page),
            ("Mini Statement", self.show_mini_statement_page)
        ]

        for text, cmd in left_buttons:
            btn = tk.Button(left_frame, text=text, font=("Arial", 20, "bold"), bg="grey", width=20, height=2, command=cmd)
            btn.pack(pady=15)

        for text, cmd in right_buttons:
            btn = tk.Button(right_frame, text=text, font=("Arial", 20, "bold"), bg="grey", width=20, height=2, command=cmd)
            btn.pack(pady=15)

    def show_account_type_page(self):  # 4th Page
        self.clear_frame()
        self.current_frame = tk.Frame(self.root, bg="blue")
        self.current_frame.pack(expand=True, fill="both")

        label = tk.Label(self.current_frame, text="Select Account Type", font=("Arial", 24, "bold"), bg="blue", fg="white")
        label.pack(pady=30)

        left_frame = tk.Frame(self.current_frame, bg="blue")
        left_frame.pack(side="left", expand=True, padx=50)

        right_frame = tk.Frame(self.current_frame, bg="blue")
        right_frame.pack(side="right", expand=True, padx=50)

        left_buttons = [
            ("Saving", self.show_amount_page),
            ("Current", self.show_amount_page)
        ]

        right_buttons = [
            ("Credit", self.show_amount_page),
            ("Other", self.show_amount_page)
        ]

        for text, cmd in left_buttons:
            btn = tk.Button(left_frame, text=text, font=("Arial", 20, "bold"), bg="grey", width=20, height=2, command=cmd)
            btn.pack(pady=15)

        for text, cmd in right_buttons:
            btn = tk.Button(right_frame, text=text, font=("Arial", 20, "bold"), bg="grey", width=20, height=2, command=cmd)
            btn.pack(pady=15)

    def show_amount_page(self):  # 5th Page
        self.clear_frame()
        self.current_frame = tk.Frame(self.root, bg="blue")
        self.current_frame.pack(expand=True, fill="both")

        label = tk.Label(self.current_frame, text="Enter Amount (100, 200, 500, 2000)", font=("Arial", 24, "bold"), bg="blue", fg="white")
        label.pack(pady=40)

        self.amount_entry = tk.Entry(self.current_frame, font=("Arial", 20))
        self.amount_entry.pack(pady=20)

        yes_btn = tk.Button(self.current_frame, text="Yes", font=("Arial", 20, "bold"), bg="grey", width=15, height=2, command=self.process_withdrawal)
        yes_btn.pack(pady=20)

        no_btn = tk.Button(self.current_frame, text="No", font=("Arial", 20, "bold"), bg="grey", width=15, height=2, command=self.show_transaction_page)
        no_btn.pack(pady=20)

    def process_withdrawal(self):
        global balance
        try:
            self.amount = int(self.amount_entry.get())
            if self.amount in [100, 200, 500, 2000] and self.amount <= balance:
                balance -= self.amount
                self.show_collect_cash_page()
            else:
                messagebox.showerror("Error", "Invalid Amount or Insufficient Balance")
        except ValueError:
            messagebox.showerror("Error", "Please enter a valid number")

    def show_collect_cash_page(self):  # 6th Page
        self.clear_frame()
        self.current_frame = tk.Frame(self.root, bg="blue")
        self.current_frame.pack(expand=True, fill="both")

        label1 = tk.Label(self.current_frame, text="Please Collect Cash", font=("Arial", 24, "bold"), bg="blue", fg="white")
        label1.pack(pady=40)

        label2 = tk.Label(self.current_frame, text=f"Your Remaining Balance is: {balance}", font=("Arial", 24, "bold"), bg="blue", fg="white")
        label2.pack(pady=40)

    # Extra Pages for remaining buttons
    def show_deposit_page(self):
        messagebox.showinfo("Deposit", "Deposit functionality coming soon!")

    def show_pin_change_page(self):
        messagebox.showinfo("Pin Change", "Pin change functionality coming soon!")

    def show_others_page(self):
        messagebox.showinfo("Others", "Other services coming soon!")

    def show_fast_cash_page(self):
        global balance
        fast_cash_amount = 500
        if fast_cash_amount <= balance:
            balance -= fast_cash_amount
            messagebox.showinfo("Fast Cash", f"Please collect Rs {fast_cash_amount}. Remaining balance: {balance}")
        else:
            messagebox.showerror("Error", "Insufficient Balance")

    def show_balance_page(self):
        messagebox.showinfo("Balance Enquiry", f"Your current balance is: {balance}")

    def show_mini_statement_page(self):
        messagebox.showinfo("Mini Statement", "Mini statement functionality coming soon!")


if __name__ == "__main__":
    root = tk.Tk()
    app = ATMApp(root)
    root.mainloop()'''

# Chat expandable

'''import tkinter as tk
from tkinter import ttk

# Sample chat data
chat_history = {
    "Chat 1": "Hello there!\nHow can I help you today?",
    "Chat 2": "You asked about Python UIs.\nWe discussed Tkinter and PyQt.",
    "Chat 3": "Remember we talked about geometry basics?",
    "Chat 4": "Adil is not working now",
}

class ChatApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Chat History Example")
        self.root.geometry("700x400")

        # Sidebar frame for chat list
        self.sidebar = tk.Frame(root, width=200, bg="#222")
        self.sidebar.pack(side="left", fill="y")

        # Main chat display area
        self.chat_display = tk.Text(root, wrap="word", bg="#fff", font=("Arial", 12))
        self.chat_display.pack(side="right", expand=True, fill="both")

        # Add chat titles to sidebar
        for chat_title in chat_history:
            btn = tk.Button(
                self.sidebar,
                text=chat_title,
                bg="#333",
                fg="white",
                relief="flat",
                anchor="w",
                padx=10,
                pady=5,
                command=lambda title=chat_title: self.show_chat(title)
            )
            btn.pack(fill="x", pady=2)

    def show_chat(self, title):
        """Display selected chat in main window"""
        self.chat_display.delete("1.0", "end")
        self.chat_display.insert("1.0", chat_history[title])

# Run the app
root = tk.Tk()
app = ChatApp(root)
root.mainloop()'''



