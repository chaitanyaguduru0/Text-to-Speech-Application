# Text-to-Speech-Application
#A Python application with a graphical user interface (GUI) that allows users to input text and convert it into speech. The application also provides options for adjusting speech parameters and support multiple languages for enhanced usability.
import tkinter as tk
from tkinter import ttk
import pyttsx3
from gtts import gTTS
import pygame
import os

# Function to convert text to speech using pyttsx3
def text_to_speech_pyttsx3(text, rate, volume):
    engine = pyttsx3.init()
    engine.setProperty('rate', rate)
    engine.setProperty('volume', volume)
    engine.say(text)
    engine.runAndWait()

# Function to convert text to speech using gTTS and save as MP3
def text_to_speech_gtts(text, language, filename="output.mp3"):
    tts = gTTS(text=text, lang=language)
    tts.save(filename)
    pygame.mixer.init()
    pygame.mixer.music.load(filename)
    pygame.mixer.music.play()

# GUI Design
root = tk.Tk()
root.title("Text-to-Speech Application")

# Text Input
text_label = ttk.Label(root, text="Enter Text:")
text_label.pack()
text_entry = ttk.Entry(root, width=50)
text_entry.pack()

# Rate Input
rate_label = ttk.Label(root, text="Rate:")
rate_label.pack()
rate_entry = ttk.Entry(root, width=10)
rate_entry.pack()

# Volume Input
volume_label = ttk.Label(root, text="Volume:")
volume_label.pack()
volume_entry = ttk.Entry(root, width=10)
volume_entry.pack()

# Language Input
language_label = ttk.Label(root, text="Language (e.g., 'en' for English):")
language_label.pack()
language_entry = ttk.Entry(root, width=10)
language_entry.pack()

# Button to trigger pyttsx3 TTS
def on_pyttsx3_button_click():
    text = text_entry.get()
    rate = int(rate_entry.get())
    volume = float(volume_entry.get())
    text_to_speech_pyttsx3(text, rate, volume)

pyttsx3_button = ttk.Button(root, text="Convert to Speech (pyttsx3)", command=on_pyttsx3_button_click)
pyttsx3_button.pack()

# Button to trigger gTTS
def on_gtts_button_click():
    text = text_entry.get()
    language = language_entry.get()
    text_to_speech_gtts(text, language)

gtts_button = ttk.Button(root, text="Convert to Speech (gTTS)", command=on_gtts_button_click)
gtts_button.pack()

root.mainloop()


