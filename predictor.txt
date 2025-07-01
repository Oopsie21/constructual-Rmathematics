

import tkinter as tk
from tkinter import messagebox, scrolledtext, filedialog
import random
import hashlib
import math
import datetime

# ------------------ Constructual Prime Checker ------------------
def is_constructual_prime(n):
    if n < 2: return False
    if n in (2, 3): return True
    if n % 2 == 0: return False
    for i in range(3, int(math.sqrt(n)) + 1, 2):
        if n % i == 0:
            return False
    return True

# ------------------ Prime Generator ------------------
def generate_prime(digits):
    while True:
        candidate = random.randint(10**(digits-1), 10**digits - 1)
        if is_constructual_prime(candidate):
            return candidate

# ------------------ SHA EchoMap (basic) ------------------
def sha_echo(input_text):
    hashed = hashlib.sha256(input_text.encode()).hexdigest()
    echo = ''.join(sorted(set(hashed)))
    return hashed, echo

# ------------------ Lagrangian (dummy function) ------------------
def compute_lagrangian(x):
    return x**2 - 0.5 * x

# ------------------ Detonative Mathematics (dummy) ------------------
def detonative_math(x):
    return (x ** 1.618) % 997

# ------------------ GUI Setup ------------------
class PrimeGUI:
    def __init__(self, root):
        self.root = root
        root.title("Core2Pi Prime Intelligence Core")
        root.geometry("800x700")

        self.log_box = scrolledtext.ScrolledText(root, width=100, height=25)
        self.log_box.pack(pady=10)

        self.entry = tk.Entry(root, width=50)
        self.entry.pack(pady=5)

        btn_frame = tk.Frame(root)
        btn_frame.pack()

        tk.Button(btn_frame, text="Check Prime", command=self.check_prime).grid(row=0, column=0, padx=5)
        tk.Button(btn_frame, text="Generate 12-digit Prime", command=lambda: self.generate(12)).grid(row=0, column=1, padx=5)
        tk.Button(btn_frame, text="Generate 18-digit Prime", command=lambda: self.generate(18)).grid(row=0, column=2, padx=5)
        tk.Button(btn_frame, text="Predict Prime", command=self.predict_prime).grid(row=0, column=3, padx=5)
        tk.Button(btn_frame, text="SHA EchoMap", command=self.sha_echo_btn).grid(row=1, column=0, padx=5, pady=5)
        tk.Button(btn_frame, text="Lagrangian", command=self.lagrangian_btn).grid(row=1, column=1, padx=5)
        tk.Button(btn_frame, text="Detonative Math", command=self.detonative_btn).grid(row=1, column=2, padx=5)
        tk.Button(btn_frame, text="Save Log", command=self.save_log).grid(row=1, column=3, padx=5)

    def log(self, text):
        timestamp = datetime.datetime.now().strftime("[%H:%M:%S]")
        self.log_box.insert(tk.END, f"{timestamp} {text}\n")
        self.log_box.see(tk.END)

    def check_prime(self):
        try:
            num = int(self.entry.get())
            result = is_constructual_prime(num)
            self.log(f"Checked {num}: Prime = {result}")
        except ValueError:
            self.log("Invalid input for prime check.")

    def generate(self, digits):
        prime = generate_prime(digits)
        self.log(f"Generated {digits}-digit prime: {prime}")

    def predict_prime(self):
        try:
            seed = int(self.entry.get())
            next_candidate = seed + 2
            while not is_constructual_prime(next_candidate):
                next_candidate += 2
            self.log(f"Predicted next prime after {seed}: {next_candidate}")
        except ValueError:
            self.log("Invalid input for prediction.")

    def sha_echo_btn(self):
        text = self.entry.get()
        if not text:
            self.log("No input text for SHA.")
            return
        hashed, echo = sha_echo(text)
        self.log(f"SHA256: {hashed}\nEcho: {echo}")

    def lagrangian_btn(self):
        try:
            x = float(self.entry.get())
            result = compute_lagrangian(x)
            self.log(f"Lagrangian at x={x}: {result}")
        except ValueError:
            self.log("Invalid input for Lagrangian.")

    def detonative_btn(self):
        try:
            x = float(self.entry.get())
            result = detonative_math(x)
            self.log(f"Detonative Math at x={x}: {result}")
        except ValueError:
            self.log("Invalid input for Detonative Math.")

    def save_log(self):
        content = self.log_box.get("1.0", tk.END)
        path = filedialog.asksaveasfilename(defaultextension=".txt", filetypes=[("Text files", "*.txt")])
        if path:
            with open(path, "w") as f:
                f.write(content)
            self.log(f"Log saved to {path}")

# ------------------ MAIN ------------------
if __name__ == "__main__":
    root = tk.Tk()
    app = PrimeGUI(root)
    root.mainloop()




 
