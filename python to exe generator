#pip install pyinstaller

import tkinter as tk
from tkinter import filedialog, messagebox
import subprocess
import os
import shutil  # <-- Import shutil to move files

def select_python_file():
    """ Open a file dialog to select the Python script """
    file_path = filedialog.askopenfilename(filetypes=[("Python Files", "*.py")])
    if file_path:
        py_file_entry.delete(0, tk.END)
        py_file_entry.insert(0, file_path)

def select_output_folder():
    """ Open a file dialog to select the output folder for the .exe file """
    folder_path = filedialog.askdirectory()
    if folder_path:
        output_folder_entry.delete(0, tk.END)
        output_folder_entry.insert(0, folder_path)

def convert_to_exe():
    """ Convert the selected Python file to an executable using PyInstaller """
    py_file = py_file_entry.get()
    output_folder = output_folder_entry.get()
    exe_name = exe_name_entry.get()

    if not py_file or not output_folder or not exe_name:
        messagebox.showerror("Error", "Please select a Python file, output folder, and specify an .exe name.")
        return

    try:
        # Get the directory where the Python script is located
        script_dir = os.path.dirname(py_file)

        # Run PyInstaller in the script directory
        os.chdir(script_dir)
        command = f'pyinstaller --onefile --windowed --name "{exe_name}" "{py_file}"'
        subprocess.run(command, shell=True, check=True)

        # Define the paths
        dist_folder = os.path.join(script_dir, "dist")
        exe_path = os.path.join(dist_folder, f"{exe_name}.exe")
        final_exe_path = os.path.join(output_folder, f"{exe_name}.exe")

        # Move the .exe to the user-specified output folder
        if os.path.exists(exe_path):
            shutil.move(exe_path, final_exe_path)
            messagebox.showinfo("Success", f"Executable created successfully!\nSaved at: {final_exe_path}")
        else:
            messagebox.showerror("Error", "Executable was not created. Check PyInstaller logs.")

    except subprocess.CalledProcessError as e:
        messagebox.showerror("Error", f"Conversion failed!\n{str(e)}")

# GUI Setup
root = tk.Tk()
root.title("Python to EXE Converter")
root.geometry("500x250")

tk.Label(root, text="Select Python File:").pack(pady=5)
py_file_entry = tk.Entry(root, width=50)
py_file_entry.pack(pady=5)
tk.Button(root, text="Browse", command=select_python_file).pack(pady=5)

tk.Label(root, text="Output Folder:").pack(pady=5)
output_folder_entry = tk.Entry(root, width=50)
output_folder_entry.pack(pady=5)
tk.Button(root, text="Browse", command=select_output_folder).pack(pady=5)

tk.Label(root, text="Executable Name (without .exe):").pack(pady=5)
exe_name_entry = tk.Entry(root, width=50)
exe_name_entry.pack(pady=5)

tk.Button(root, text="Convert to EXE", command=convert_to_exe).pack(pady=10)

root.mainloop()
