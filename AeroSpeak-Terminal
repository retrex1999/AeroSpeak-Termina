import tkinter as tk
import os, threading
from gtts import gTTS

# NATO AVIATION PHONETIC ALPHABET
AVIATION_ALPHABET = {
    'A': 'Alpha', 'B': 'Bravo', 'C': 'Charlie', 'D': 'Delta', 'E': 'Echo',
    'F': 'Foxtrot', 'G': 'Golf', 'H': 'Hotel', 'I': 'India', 'J': 'Juliett',
    'K': 'Kilo', 'L': 'Lima', 'M': 'Mike', 'N': 'November', 'O': 'Oscar',
    'P': 'Papa', 'Q': 'Quebec', 'R': 'Romeo', 'S': 'Sierra', 'T': 'Tango',
    'U': 'Uniform', 'V': 'Victor', 'W': 'Whiskey', 'X': 'X-ray', 'Y': 'Yankee',
    'Z': 'Zulu', '0': 'Zero', '1': 'One', '2': 'Two', '3': 'Three', '4': 'Four',
    '5': 'Five', '6': 'Six', '7': 'Seven', '8': 'Eight', '9': 'Nine'
}

class AeroSpeakTerminal(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title("AeroSpeak Terminal")
        self.geometry("1000x750")
        self.configure(bg="#000")
        self.setup_ui()

    def setup_ui(self):
        tk.Label(self, text="AEROSPEAK TERMINAL", fg="cyan", bg="#000", font=("Consolas", 24, "bold")).pack(pady=20)
        tk.Label(self, text="COMMAND INPUT:", fg="cyan", bg="#000", font=("Consolas", 12)).pack(pady=10)
        self.cmd_entry = tk.Entry(self, width=60, font=("Consolas", 14), bg="#111", fg="white", insertbackground="white")
        self.cmd_entry.pack(pady=5)
        tk.Button(self, text="TRANSMIT (SPEAK)", command=self.process_command, bg="#00CED1", font=("Consolas", 10, "bold")).pack(pady=15)
        
        tk.Label(self, text="AVIATION PHONETIC REFERENCE:", fg="#00FF00", bg="#000", font=("Consolas", 10, "bold")).pack(pady=(30, 5))
        self.ref_frame = tk.Frame(self, bg="#050505", bd=2, relief="groove")
        self.ref_frame.pack(fill="x", padx=20, pady=10)
        ref_text = " | ".join([f"{k}:{v}" for k, v in AVIATION_ALPHABET.items()])
        tk.Label(self.ref_frame, text=ref_text, fg="#CCC", bg="#050505", font=("Consolas", 8), wraplength=950).pack(pady=10)

    def process_command(self):
        text = self.cmd_entry.get()
        if text:
            threading.Thread(target=self.speak_aviation_code, args=(text,), daemon=True).start()

    def speak_aviation_code(self, text):
        encoded = " ".join([AVIATION_ALPHABET.get(c.upper(), c) for c in text if c.isalnum() or c == ' '])
        tts = gTTS(text=encoded, lang='en')
        tts.save("output.mp3")
        os.system("play output.mp3" if os.path.exists("/usr/bin/play") else "mpg123 output.mp3")

if __name__ == "__main__":
    app = AeroSpeakTerminal()
    app.mainloop()
