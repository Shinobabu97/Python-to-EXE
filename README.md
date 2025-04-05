Step-by-Step Guide to Build .exe

1. Install PyInstaller
   Run this once (in your Python environment): pip install pyinstaller 
   
2. Navigate to your project folder
   
3. Build the executable
   pyinstaller --noconfirm --clean --onefile --windowed gui_launcher.py
   
4. Output:
    PyInstaller creates:
    dist/
    ├── gui_launcher.exe     ← ✅ Your final executable
    build/
    gui_launcher.spec
   
You only need the file in dist/gui_launcher.exe. You can rename it if you want.
PyInstaller will include the whole folders automatically if your imports are used.

5. Optional: Add an icon
    pyinstaller --onefile --windowed --icon=myicon.ico gui_launcher.py
