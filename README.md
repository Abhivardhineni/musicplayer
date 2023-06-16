import tkinter as tk
import pygame
from tkinter import filedialog

class MusicPlayer:
    def __init__(self, root):
        self.root = root
        self.root.title("Music Player")
        
        # Initialize Pygame mixer
        pygame.mixer.init()

        # Create UI elements
        self.label = tk.Label(root, text="Music Player", font=("Helvetica", 16))
        self.label.pack(pady=10)

        self.btn_select = tk.Button(root, text="Select Music", command=self.select_music)
        self.btn_select.pack(pady=5)

        self.btn_play = tk.Button(root, text="Play", state=tk.DISABLED, command=self.play_music)
        self.btn_play.pack(pady=5)

        self.btn_stop = tk.Button(root, text="Stop", state=tk.DISABLED, command=self.stop_music)
        self.btn_stop.pack(pady=5)

    def select_music(self):
        # Open file dialog to select music file
        file_path = filedialog.askopenfilename(filetypes=[("Audio Files", "*.mp3")])
        if file_path:
            self.music_file = file_path
            self.btn_play.config(state=tk.NORMAL)
            self.btn_stop.config(state=tk.NORMAL)

    def play_music(self):
        # Load and play the selected music file
        pygame.mixer.music.load(self.music_file)
        pygame.mixer.music.play()

    def stop_music(self):
        # Stop the currently playing music
        pygame.mixer.music.stop()

if __name__ == "__main__":
    # Create the Tkinter root window
    root = tk.Tk()

    # Create an instance of the MusicPlayer class
    music_player = MusicPlayer(root)

    # Start the Tkinter event loop
    root.mainloop()
