# Implementation of a Language Translation Tool

# AIM:
To develop a simple GUI-based language translator using Python and the Google Translate API.

## DESIGN STEPS:

### Step 1:
Define the GUI layout and create an interface using the tkinter library.

### Step 2:
Set up dropdown menus for selecting source and target languages.

### Step 3:
Implement text input and output boxes for user interaction.

### Step 4:
Integrate the Google Translate API to handle the translation functionality.

### Step 5:
Add buttons for translating and clearing text.

### Step 6:
Test the application for various language translations.

## PROGRAM:

```
# Importing required libraries
import tkinter as tk
from tkinter import ttk, messagebox
from googletrans import Translator

# Translator object
translator = Translator()

# Function to translate the text
def translate_text():
    try:
        # Get user inputs
        source_lang = source_language.get()
        target_lang = target_language.get()
        input_text = source_text_box.get("1.0", tk.END).strip()

        # Check if input text is empty
        if not input_text:
            messagebox.showwarning("Warning", "Please enter some text to translate.")
            return

        # Perform translation
        result = translator.translate(input_text, src=language_map[source_lang], dest=language_map[target_lang])
        result_text_box.delete("1.0", tk.END)
        result_text_box.insert(tk.END, result.text)
    except Exception as e:
        messagebox.showerror("Error", f"An error occurred: {e}")

# Function to clear text boxes
def clear_text():
    source_text_box.delete("1.0", tk.END)
    result_text_box.delete("1.0", tk.END)

# Create the main application window
app = tk.Tk()
app.title("Language Translator")
app.geometry("800x500")
app.configure(bg="#e8f4f8")

# Title Label
title_label = tk.Label(
    app,
    text="Language Translator",
    font=("Helvetica", 20, "bold"),
    bg="#007acc",
    fg="white",
    padx=10,
    pady=10
)
title_label.pack(fill=tk.X)

# Language selection dropdowns
language_map = {
    "Auto Detect": "auto",
    "English": "en",
    "French": "fr",
    "German": "de",
    "Spanish": "es",
    "Tamil": "ta",
    "Hindi": "hi"
}

frame = tk.Frame(app, bg="#e8f4f8")
frame.pack(pady=15)

source_language_label = tk.Label(
    frame, text="Source Language:", bg="#e8f4f8", font=("Helvetica", 12)
)
source_language_label.grid(row=0, column=0, padx=10, pady=5, sticky="w")

source_language = ttk.Combobox(
    frame, values=list(language_map.keys()), state="readonly", width=20
)
source_language.set("Auto Detect")
source_language.grid(row=0, column=1, padx=10, pady=5)

target_language_label = tk.Label(
    frame, text="Target Language:", bg="#e8f4f8", font=("Helvetica", 12)
)
target_language_label.grid(row=0, column=2, padx=10, pady=5, sticky="w")

target_language = ttk.Combobox(
    frame, values=list(language_map.keys()), state="readonly", width=20
)
target_language.set("English")
target_language.grid(row=0, column=3, padx=10, pady=5)

# Text boxes for input and output
text_frame = tk.Frame(app, bg="#e8f4f8")
text_frame.pack(pady=10)

source_text_box = tk.Text(
    text_frame, height=10, width=40, font=("Helvetica", 12), wrap=tk.WORD, relief="ridge", bd=2
)
source_text_box.grid(row=0, column=0, padx=10, pady=5)

result_text_box = tk.Text(
    text_frame, height=10, width=40, font=("Helvetica", 12), wrap=tk.WORD, relief="ridge", bd=2, bg="white"
)
result_text_box.grid(row=0, column=1, padx=10, pady=5)

# Buttons
button_frame = tk.Frame(app, bg="#e8f4f8")
button_frame.pack(pady=15)

translate_button = tk.Button(
    button_frame,
    text="🌐 Translate",
    font=("Helvetica", 14, "bold"),
    bg="#4CAF50",
    fg="white",
    padx=20,
    pady=10,
    relief="raised",
    bd=3,
    command=translate_text
)
translate_button.grid(row=0, column=0, padx=10)

clear_button = tk.Button(
    button_frame,
    text="❌ Clear",
    font=("Helvetica", 14, "bold"),
    bg="#FF6347",
    fg="white",
    padx=20,
    pady=10,
    relief="raised",
    bd=3,
    command=clear_text
)
clear_button.grid(row=0, column=1, padx=10)

# Footer Label
footer_label = tk.Label(
    app,
    text="Powered by Google Translate",
    font=("Helvetica", 10, "italic"),
    bg="#e8f4f8",
    fg="#555555"
)
footer_label.pack(side=tk.BOTTOM, pady=10)

# Run the application
app.mainloop()

```
