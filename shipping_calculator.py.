import tkinter as tk
from tkinter import messagebox
import datetime

# Shipping options
STANDARD = 1
EXPEDITED = 2

# Shipping rates (in INR)
shipping_rates = {
    STANDARD: 499,    # Standard shipping cost ₹499
    EXPEDITED: 1099   # Expedited shipping cost ₹1099
}

# Zone multipliers
zone_multipliers = {
    'A': 1.0,
    'B': 1.2,
    'C': 1.5
}

def calculate_shipping_cost(option, weight, dimensions, zone):
    """Calculates the shipping cost based on option, weight, dimensions, and zone."""
    base_cost = shipping_rates[option]
    # Convert dimensions from cm to meters
    volume = (dimensions[0] / 100) * (dimensions[1] / 100) * (dimensions[2] / 100)  # Volume in cubic meters
    zone_multiplier = zone_multipliers[zone]
    return base_cost + weight * volume * 100 * zone_multiplier

def save_shipping_label(option, cost, package_data):
    """Saves the shipping label to a file."""
    current_time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open("shipping_label.txt", "w", encoding="utf-8") as file:
        file.write(f"Shipping Option: {'Standard' if option == STANDARD else 'Expedited'}\n")
        file.write(f"Shipping Cost: ₹{round(cost, 2)}\n")
        file.write("Package Details:\n")
        for key, value in package_data.items():
            file.write(f"  {key}: {value}\n")
        file.write(f"Date & Time: {current_time}\n")

def show_shipping_label(option, cost, package_data):
    """Creates a new window to display the shipping label details."""
    label_window = tk.Toplevel()
    label_window.title("Shipping Label")

    current_time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    tk.Label(label_window, text="Shipping Label", font=("Helvetica", 16)).pack(pady=10)
    tk.Label(label_window, text=f"Shipping Option: {'Standard' if option == STANDARD else 'Expedited'}").pack()
    tk.Label(label_window, text=f"Shipping Cost: ₹{round(cost, 2)}").pack()
    tk.Label(label_window, text="Package Details:").pack()

    for key, value in package_data.items():
        tk.Label(label_window, text=f"  {key}: {value}").pack()

    tk.Label(label_window, text=f"Date & Time: {current_time}").pack()
    tk.Button(label_window, text="Close", command=label_window.destroy).pack(pady=10)

def calculate_and_display():
    """Gets input from the GUI and calculates the shipping cost."""
    try:
        # Get input values from the GUI
        length = float(length_entry.get())
        width = float(width_entry.get())
        height = float(height_entry.get())
        weight = float(weight_entry.get())  # weight in kilograms
        option = option_var.get()
        zone = zone_var.get()

        # Calculate shipping cost
        dimensions = (length, width, height)
        cost = calculate_shipping_cost(option, weight, dimensions, zone)

        # Prepare package data
        package_data = {
            "Length (cm)": length,
            "Width (cm)": width,
            "Height (cm)": height,
            "Weight (kg)": weight,
            "Customer Name": customer_name_entry.get(),
            "Product Name": product_name_entry.get(),
            "Zone": zone
        }

        # Show the shipping label details in a new window
        show_shipping_label(option, cost, package_data)

        # Save shipping label
        save_shipping_label(option, cost, package_data)

        messagebox.showinfo("Success", "Shipping label saved!")
    except ValueError:
        messagebox.showerror("Input Error", "Please enter valid numbers for dimensions and weight.")

# Create the tkinter window
root = tk.Tk()
root.title("Shipping Label Generator")

# Labels and Entry widgets for user input
tk.Label(root, text="Customer Name:").grid(row=0, column=0)
customer_name_entry = tk.Entry(root)
customer_name_entry.grid(row=0, column=1)

tk.Label(root, text="Product Name:").grid(row=1, column=0)
product_name_entry = tk.Entry(root)
product_name_entry.grid(row=1, column=1)

tk.Label(root, text="Length (in cm):").grid(row=2, column=0)
length_entry = tk.Entry(root)
length_entry.grid(row=2, column=1)

tk.Label(root, text="Width (in cm):").grid(row=3, column=0)
width_entry = tk.Entry(root)
width_entry.grid(row=3, column=1)

tk.Label(root, text="Height (in cm):").grid(row=4, column=0)
height_entry = tk.Entry(root)
height_entry.grid(row=4, column=1)

tk.Label(root, text="Weight (in kg):").grid(row=5, column=0)
weight_entry = tk.Entry(root)
weight_entry.grid(row=5, column=1)

# Dropdown for shipping option
tk.Label(root, text="Shipping Option:").grid(row=6, column=0)
option_var = tk.IntVar(value=STANDARD)
tk.Radiobutton(root, text="Standard", variable=option_var, value=STANDARD).grid(row=6, column=1)
tk.Radiobutton(root, text="Expedited", variable=option_var, value=EXPEDITED).grid(row=6, column=2)

# Dropdown for zone selection
tk.Label(root, text="Shipping Zone:").grid(row=7, column=0)
zone_var = tk.StringVar(value='A')
tk.OptionMenu(root, zone_var, 'A', 'B', 'C').grid(row=7, column=1)

# Button to calculate shipping cost
tk.Button(root, text="Calculate Shipping", command=calculate_and_display).grid(row=8, column=0, columnspan=2)

# Start the tkinter main loop
root.mainloop()
