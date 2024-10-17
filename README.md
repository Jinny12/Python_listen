import os
import speech_recognition as sr
import threading

def print_loop():
    while True:
        print(Fore.LIGHTGREEN_EX + "Listning..", end="",flush=True)
        print(Style.RESET_ALL,end="",flush=True)

def Translate_hindi_tO_english(text):
    english_text =translate(text,"en-us")
    return english_text




def Speech_To_Text_Python():
    recognizer = sr.Recognizer()
    recognizer.energy_threshold = 34000
    recognizer.dynamic_energy_adjustment_damping = 0.010
    recognizer.dynamic_energy_ratio = 1.0
    recognizer.operation_timeout = None
    recognizer.pause_threshold = 0.8
    recognizer.non_speaking_duration = 0.5
    
    with sr.Microphone() as source:
        recognizer.adjust_for_ambient_noise(source)
        while True:
            print("Listening...", end="", flush=True)
            try:
                audio = recognizer.listen(source, timeout=None)
                print("\rRecognizing...", end="", flush=True)
                recognizer_txt = recognizer.recognize_google(audio).lower()
                
                if recognizer_txt:
                    return recognizer_txt
                else:
                    return ""
            except sr.UnknownValueError:
                recognizer_txt = ""
            finally:
                print("\r", end="", flush=True)
            os.system("cls" if os.name == "nt" else "clear")

print(Speech_To_Text_Python())
