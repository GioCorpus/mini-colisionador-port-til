# mini-colisionador-portatil
Demo Universidades

mini-colisionador portátil

import RPi.GPIO as GPIO
import time
import matplotlib.pyplot as plt
from gpiozero import LED, Button  # Para detector simulado

# Configuración pines (ajusta según tu wiring)
HV_RELAY_PIN = 17       # Relay para alto voltaje (10kV ON/OFF)
DETECTOR_PIN = 18       # Pin de entrada: simula detector (LED o pulsador)
LED_VISUAL_PIN = 27     # LED que parpadea al detectar colisión

# Inicializa GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setup(HV_RELAY_PIN, GPIO.OUT)
GPIO.setup(LED_VISUAL_PIN, GPIO.OUT)

detector = Button(DETECTOR_PIN)  # gpiozero para leer pulsos

def activar_acelerador():
    GPIO.output(HV_RELAY_PIN, True)
    print("Acelerador ON: 10kV aplicado. Partículas en movimiento...")
    time.sleep(2)  # Tiempo de "aceleración"

def desactivar_acelerador():
    GPIO.output(HV_RELAY_PIN, False)
    print("Acelerador OFF. Seguridad primero.")

def detectar_colision():
    if detector.is_pressed:  # Simula impacto (presiona botón o conecta sensor real)
        GPIO.output(LED_VISUAL_PIN, True)
        print("¡Colisión detectada! Ionización en detector.")
        time.sleep(0.5)
        GPIO.output(LED_VISUAL_PIN, False)
        return True
    return False

def simular_trayectoria():
    """Gráfico simple de trayectoria (electrón en campo magnético)"""
    t = [i * 0.01 for i in range(100) math.cos(2 * math.pi * 0.5 * ti) * ti for ti in t math.sin(2 * math.pi * 0.5 * ti) * ti for ti in t]
    
    plt.figure(figsize=(6, 6))
    plt.plot(x, y, color='blue', label='Electrón acelerado')
    plt.title("Trayectoria en Mini-Colisionador Mexicali")
    plt.xlabel("Distancia (arbitraria)")
    plt.ylabel("Desviación (arbitraria)")
    plt.grid(True)
    plt.legend()
    plt.show(block=False)  # Muestra sin bloquear
    time.sleep(3)  # Da tiempo a ver

def run_experiment():
    print("Mini-Colisionador Mexicali - v1.0")
    print("Presiona el botón del detector para simular colisión.")
    
    activar_acelerador()
    
    start_time = time.time()
    while time.time() - start_time < 15:  # 15 segundos de experimento
        if detectar_colision():
            print(f"Impacto a los {time.time() - start_time:.1f} segundos.")
            simular_trayectoria()
            break
        time.sleep(0.1)
    
    desactivar_acelerador()
    print("Experimento terminado. Limpieza...")

# Ejecuta
try:
    run_experiment()
except KeyboardInterrupt:
    print("Parando manualmente.")
finally:
    desactivar_acelerador()
    GPIO.cleanup()
    print("GPIO limpio. Listo para el siguiente run.")
	
	git add colisionador_portatil.py
git commit -m "feat: mini-colisionador portátil - electrones acelerados, colisiones simuladas, no LHC"
git push
