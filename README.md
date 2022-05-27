# Hydroponic-Code

import RPi.GPIO as GPIO
import time
import datetime

#task = input('start? ')

GPIO.setmode(GPIO.BOARD)
GPIO.setup(11, GPIO.OUT)
GPIO.setup(13, GPIO.OUT)

now = datetime.datetime.now()
    
An = now.replace(hour=15, minute=00, second=0, microsecond=0)
Aus = now.replace(hour=14, minute=25, second=0, microsecond=0)

def motor_on(pin):
    global now                                                    
    while(True):
        if now >= An or now <= Aus:
            GPIO.output(11, GPIO.HIGH)
            GPIO.output(13, GPIO.HIGH)
            time.sleep(10)
            GPIO.output(11, GPIO.LOW)
            time.sleep(790)
            GPIO.output(13, GPIO.LOW)
            time.sleep(1200)
            GPIO.output(13, GPIO.HIGH)
            time.sleep(800)
            GPIO.output(13, GPIO.LOW)
            time.sleep(1200)
            now = datetime.datetime.now() 
            print(now)
    
def motor_off(pin):
    GPIO.output(pin, GPIO.LOW)
    
while(True):
    if An <= Aus:
        print(' negatives Zeitintervall, wähle: An < Aus ')       #je nach Zeitverschiebung    
    if now >= An or now <= Aus:
        motor_on(11)
        print('motor on')
        
        
    if now < An and now > Aus:
        #print('motor off ')
        motor_off(11)
        motor_off(13)
        time.sleep(60)
        
