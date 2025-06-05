# VoiceAssistant
import pyautogui
import time
import pyttsx3
import speech_recognition as sr

recognizer = sr.Recognizer()
engine = pyttsx3.init()


def Jarvis_main():
    while True:
        try:
            with sr.Microphone() as source:
                recognizer.adjust_for_ambient_noise(source, duration=0.2)
                audio = recognizer.listen(source)
                text = recognizer.recognize_google(audio)
                text = text.lower()
                return text

        except sr.UnknownValueError():
            engine.say("Please say that again")
            engine.runAndWait()
            continue


def play_music(song):
    pyautogui.moveTo(800,744)
    pyautogui.click()
    time.sleep(1)
    pyautogui.hotkey('ctrl', 'k')
    time.sleep(1)
    pyautogui.typewrite(song)
    time.sleep(1)
    pyautogui.press('enter')

def search_up(thing):
    pyautogui.moveTo(755,744)
    pyautogui.click()
    time.sleep(1)
    pyautogui.hotkey('ctrl', 't')
    time.sleep(1)
    pyautogui.typewrite(thing + " ")
    time.sleep(1)
    pyautogui.press('enter')

def contact_whatsapp(person):
    pyautogui.moveTo(529,744)
    pyautogui.click()
    time.sleep(1)
    pyautogui.moveTo(440, 90)
    pyautogui.click()
    time.sleep(1)
    pyautogui.typewrite("whatsapp")
    pyautogui.press('enter')
    time.sleep(5)
    pyautogui.hotkey("ctrl", "f")
    time.sleep(1)
    pyautogui.typewrite(person)
    time.sleep(1)
    pyautogui.press('enter')
    pyautogui.moveTo(214, 172)
    pyautogui.click()
    time.sleep(1)

def call(persontocall, way):
    contact_whatsapp(persontocall)
    if way == "vid":
        pyautogui.moveTo(1233, 65)
        pyautogui.click()
    else:
        pyautogui.moveTo(1290, 65)
        pyautogui.click()

def analyze(command):
    while True:
        if "search" in command:
            engine.say("What do u want to search up")
            engine.runAndWait()
            thing = Jarvis_main()
            search_up(thing)
            return
        if "song" in command:
            engine.say("What song do you want to play?")
            engine.runAndWait()
            song = Jarvis_main()
            play_music(song)
            return
        if "call" in command:
            engine.say("Who do you want to call?")
            engine.runAndWait()
            person = Jarvis_main()
            way = "voice"
            call(person, way)
            return
        if "nothing" in command:
            engine.say("Ok")
            engine.runAndWait()
            return
        else:
            engine.say("Could u repeat that?")
            engine.runAndWait()
            command = Jarvis_main()
            continue

while True:
    try:
        with sr.Microphone() as source:
            recognizer.adjust_for_ambient_noise(source, duration=0.2)
            audio = recognizer.listen(source)
            text = recognizer.recognize_google(audio)
            text = text.lower()
            if "friday" in text:
                engine.say("What's up")
                engine.runAndWait()
                time.sleep(1)
                command = Jarvis_main()
                analyze(command)
                continue
            else:
                print("Not a command")

    except sr.UnknownValueError:
        print("Could not understand audio")
        continue
