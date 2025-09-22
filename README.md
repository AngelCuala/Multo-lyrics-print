# Multo-lyrics-print

from os import name
import sys
import time
from threading import Thread, Lock   

lock = Lock()

def animate_text(text, delay=0.1):
    with lock:
        for char in text:
            sys.stdout.write(char)
            sys.stdout.flush()
            time.sleep(delay)
        print()  

def sing_lyric(lyric, delay, speed):
    time.sleep(delay)              
    animate_text(lyric, speed)     

def sing_song():
    lyrics = [

        ("Hindi na makalaya", 0.3, 0.2),
        ("dinadalaw mo 'ko bawat gabi", 5.0, 0.1),
        ("Wala mang nakikita", 9.8, 0.2),
        ("haplos mo'y ramdam pa rin sa dilim", 15.0, 0.1),
        ("Hindi na na-nanaginip", 19.3, 0.2),
        ("hindi na ma-makagising", 24.6, 0.2),
        ("Pasindi na ng ilaw", 28.0, 0.2),
        ("Minumulto na 'ko ng damdamin ko, ng damdamin ko", 30.0, 0.1),
    ]

    threads = []
    sing_lyric.t0 = time.monotonic()

    for lyric, start_time, speed in lyrics:
        t = Thread(target=sing_lyric, args=(lyric, start_time, speed))
        threads.append(t)
        t.start()

    for t in threads:
        t.join()

if __name__ == "__main__":
    sing_song()
