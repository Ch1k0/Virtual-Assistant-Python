import datetime
import os
import random
import time
import webbrowser
import datetime
from datetime import datetime
from random import choice
from playsound import playsound
import wikipedia
import winsound
import psutil
import pyautogui
import pyttsx3
import requests
import speech_recognition as sr
from pytz import timezone
from datetime import timedelta
from selenium import webdriver
from pyautogui import locateCenterOnScreen, click, typewrite, press
import keyboard
import cv2


engine = pyttsx3.init()
engine = pyttsx3.init('sapi5')
engine.setProperty('rate', 175) # Set Rate
engine.setProperty('volume', 1.0) # Set Volume
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)

def speak(text):
    engine.say(text)
    engine.runAndWait()

def record():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Dinliyorum...")
        audio = r.listen(source)
    try:
        command = r.recognize_google(audio, language = "tr-TR").lower()
        print("Dinlediğiniz komut: " + command)
        return command
    except sr.UnknownValueError:
        print("Anlamadım, lütfen tekrar deneyin.")
        return None
    except sr.RequestError as e:
        print("Hata: {0}".format(e))
        return None

    
def virtual_assistant():
    hour = datetime.now().hour
    if (hour >= 6) and (hour < 12):
        speak(f"Günaydın efendim")
    elif (hour >= 12) and (hour < 16):
        speak(f"iyi günler çiko")
    elif (hour >= 16) and (hour < 22):
        speak(f"iyi akşamlar efendim")
    elif (hour >= 22) and (hour < 24):
        speak(f"İyi Geceler")
    else:
        speak("Bu saatte hayırdır?")
    speak("Nasıl yardımcı olabilirim?")
    while True:
        command = record()
        if command == "uyu":
            speak("Görüşürüz!")
            break
        if command == "wikipedia'da ara":
            speak("Ne arayayım")
            search = record()
            results = wikipedia.summary(search, sentences=2)
            speak(results)

        if command == "şarkı aç":
            speak("ne  dinleyelim?")
            search = record()
            url = "https://www.youtube.com/results?search_query={}".format(search)
            webbrowser.get().open(url)
            pyautogui.moveTo(400,300,3)
            pyautogui.click()
            time.sleep(1)
            speak("keyifli dinlemeler efendim".format(search))
        if command == "google'da ara":
            speak("Ne arayayım")
            search = record()
            url = "https://www.google.com/search?q={}".format(search)
            webbrowser.get().open(url)
            speak("{} için bunları buldum".format(search))

        if command == "pencereyi değiştir":
                pyautogui.keyDown("alt")
                pyautogui.keyDown("tab")
                pyautogui.keyUp("tab")
                pyautogui.keyUp("alt")

        if command == "sekmeyi değiştir":
            pyautogui.keyDown("ctrl")
            pyautogui.keyDown("tab")
            pyautogui.keyUp("tab")
            pyautogui.keyUp("ctrl")
        
        if command == "sekmeyi kapat":
            pyautogui.keyDown("ctrl")
            pyautogui.keyDown("w")
            pyautogui.keyUp("w")
            pyautogui.keyUp("ctrl")

        if command == "yeni sekme aç":
            pyautogui.keyDown("ctrl")
            pyautogui.keyDown("t")
            pyautogui.keyUp("t")
            pyautogui.keyUp("ctrl")

        if command == "sayfayı yenile":
            pyautogui.keyDown("F5")
            pyautogui.keyUp("F5")
            speak("buyurun")
        
        if command == "aşağı kaydır":
            for i in range(10):
                pyautogui.press("down")
        elif command == "yukarı kaydır":
            for i in range(10):
                pyautogui.press("up")

        if command == "tıkla":
            pyautogui.click(button='left')

        # if command == "benim için yazar mısın":
        #     speak("dinliyorum")
        #     text_to_write = record()
        #     pyautogui.hotkey('ctrl', 'a')
        #     pyautogui.typewrite(text_to_write)
        #     pyautogui.keyDown("enter")
        #     pyautogui.keyDown("enter")

        if command == "benim için yazar mısın":
            speak("dinliyorum")
            text_to_write = record()
            keyboard.write(text_to_write, delay=0.1)
            pyautogui.hotkey('ctrl', 'alt', 'up')
            pyautogui.keyDown("enter")
            pyautogui.keyDown("enter")

        #if command == "yorum yap":

        if command == "sesi aç":
            pyautogui.press("volumeup")
        if command == "sesi kıs":
            pyautogui.press("volumedown")
        if command == "sesi kapat":
            pyautogui.press("volumemute")
        
        if command == "şarjımız kaç":
            battery = psutil.sensors_battery()
            percentage = battery.percent
            speak(f"sistemde yüzde {percentage} şarj kaldı.")

        if command == "ss al":
            speak("isim ne olsun")
            name = record()
            speak("çekiyorum")
            time.sleep(3)
            img = pyautogui.screenshot()
            img.save(f"{name}.png")
            speak("Tamamdır")
        if command == "resmi sil":
            speak("hangisini?")
            file = record()
            os.remove(file + ".png")
            speak("tamamdır")

        if command == "benim için not al":
            speak("ismi ne olsun")
            txtFile = record() + ".txt"
            speak("ne yazayım?")
            text = record()
            with open(txtFile, "w", encoding="utf-8") as f:
                f.write(text)
            speak("Tamamdır")
        if command == "notu sil":
            speak("hangi notu sileceğiz?")
            txtFile = record() + ".txt"
            os.remove(txtFile)
            speak("tamamdır")
        if command == "yapay zeka modunu hazırla":
            import ai
            ai.girdi()

        elif command == "saat kaç":
            selection = ["Saat", "şu an"]
            clock = datetime.now().strftime("%H:%M")
            selection = random.choice(selection)
            speak(selection + clock)
        elif command == "bugün tarih ne":
            speak(datetime.now().strftime("%Y-%m-%d"))
        elif command == "günlerden ne":
            today = datetime.now().strftime("%A").lower()
            speak(today)

        elif command == "merhaba":
            speak("Selam")
        elif command == "teşekkür ederim":
            speak("Rica ederim")
        if command == "hava durumuna bak":
            speak("Hangi şehrin hava durumuna bakalım?")
            city_name = record()
            api_key = "api key here"
            base_url = "http://api.openweathermap.org/"
            complete_url = base_url + "appid=" + api_key + "&q=" + city_name

            response = requests.get(complete_url)

            data = response.json()

            main = data['main']

            sıcaklık = main['temp']

            nem = main['humidity']

            basınç = main['pressure']

            fahrenheit = float(sıcaklık)
            celsius = round(fahrenheit - 273)

            # hPa = float(pressure)
            # psi = (hPa * 0.0145038)  

            detay = data['weather']
            weather_translations = {"Clouds": "Bulutlu", "Clear": "Açık", "Rain": "Yağmurlu", "Snow": "Kar yağışlı"}
            main = data['weather'][0]['main']

            speak(f"{city_name:}, Sıcaklık: {celsius}°C, Nem: %{nem} Basınç: {basınç}, Hava: {weather_translations[main]}")
            # print(f"{city_name:})
            # print(f"Sıcaklık: {celsius}°C")
            # print(f"Nem: %{nem}")
            # print(f"Basınç: {basınç}")
            # print(f"Hava: {detay[0]['main']}")
virtual_assistant()
