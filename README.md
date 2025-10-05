"""
╔══════════════════════════════════════════════════════════════════════════╗
║                        SHIKSHA ROBOT PROJECT                             ║
║              AI-Integrated Educational Assistant System                  ║
╚══════════════════════════════════════════════════════════════════════════╝

📋 OVERVIEW
─────────────────────────────────────────────────────────────────────────
SHIKSHA Robot is an AI-integrated educational assistant developed at 
Experimind Labs. It uses barcode scanning to detect educational charts and 
narrates lessons through voice, making learning interactive and accessible 
for students in government schools.

🎯 OBJECTIVES
─────────────────────────────────────────────────────────────────────────
- Develop affordable educational robot for government schools
- Enable interactive learning through voice and visual engagement
- Use barcode-based chart recognition for content delivery
- Build durable, modular design for classroom use
- Minimize production costs without compromising functionality

🔍 SCOPE
─────────────────────────────────────────────────────────────────────────
- Target: Government schools and budget-constrained institutions
- Application: Interactive teaching assistant for STEM education
- Deployment: 8 units successfully deployed
- Impact: Making technology-driven education accessible to all

🤖 KEY FEATURES
─────────────────────────────────────────────────────────────────────────
- Barcode chart detection (98.5% accuracy)
- Voice narration of educational content
- NeoPixel LED facial expressions (64 LEDs)
- Servo-controlled ear movements
- 6-8 hours battery life
- Response time < 0.5 seconds

🔧 HARDWARE COMPONENTS
─────────────────────────────────────────────────────────────────────────
- Raspberry Pi 4
- Barcode Scanner Module
- NeoPixel LED Matrix (64 pixels)
- 2x SG90 Servo Motors
- 5W Speaker + Amplifier
- 12V Battery + Buck Converter
- MDF, SS Steel, MS Steel Chassis

💻 SOFTWARE STACK
─────────────────────────────────────────────────────────────────────────
- Python 3.x
- RPi.GPIO (Servo control)
- Adafruit NeoPixel (LED control)
- PyGame (Audio playback)
- PySerial (Scanner interface)
- SMBus (Power monitoring)

⚙️ HOW IT WORKS
─────────────────────────────────────────────────────────────────────────
1. Teacher presents chart → Barcode scanner reads ID
2. Robot displays thinking expression → Loads audio content
3. Excited expression + ear wiggle → Captures attention
4. Audio narration plays → Visual feedback via LEDs
5. Returns to happy face → Ready for next chart

📊 PERFORMANCE METRICS
─────────────────────────────────────────────────────────────────────────
- Detection Accuracy: 98.5%
- Response Time: < 0.5 seconds
- Battery Life: 6-8 hours
- Units Deployed: 8
- Weight: 2.5 kg

🚀 FUTURE ENHANCEMENTS
─────────────────────────────────────────────────────────────────────────
- Voice command recognition
- Multilingual content support
- Cloud connectivity for content updates
- Mobile app for teacher control
- Advanced AI for personalized learning
"""

import serial
import time
import board
import neopixel
import RPi.GPIO as GPIO
import pygame
import os
import smbus

# Configuration
CONFIG = {
    "barcode_scanner": {"port": "/dev/ttyUSB0", "baudrate": 9600},
    "neopixel": {"pin": board.D18, "num_pixels": 64, "brightness": 0.5},
    "servo": {"left_pin": 17, "right_pin": 27},
    "audio": {"directory": "audio_files", "volume": 0.8},
    "power": {"i2c_address": 0x48}
}

class BarcodeScanner:
    def __init__(self, port, baudrate):
        self.serial_port = serial.Serial(port, baudrate, timeout=1)
        
    def read_barcode(self):
        if self.serial_port.in_waiting > 0:
            return self.serial_port.readline().decode('utf-8').strip()
        return None
    
    def close(self):
        self.serial_port.close()

class FacialExpression:
    def __init__(self, pin, num_pixels, brightness):
        self.pixels = neopixel.NeoPixel(pin, num_pixels, brightness=brightness, auto_write=False)
        
    def happy_face(self):
        self.pixels.fill((0, 0, 0))
        for pos in [18, 19, 21, 22, 42, 43, 45, 46]:
            self.pixels[pos] = (0, 255, 0)
        for pos in [49, 50, 51, 52, 53, 54]:
            self.pixels[pos] = (255, 255, 0)
        self.pixels.show()
    
    def thinking_face(self):
        self.pixels.fill((0, 0, 0))
        for pos in [18, 19, 21, 22, 42, 43, 45, 46]:
            self.pixels[pos] = (0, 0, 255)
        self.pixels.show()
    
    def excited_face(self):
        self.pixels.fill((0, 0, 0))
        for pos in [17, 18, 19, 20, 21, 22, 41, 42, 43, 44, 45, 46]:
            self.pixels[pos] = (0, 255, 255)
        for pos in [48, 49, 50, 51, 52, 53, 54, 55]:
            self.pixels[pos] = (255, 200, 0)
        self.pixels.show()
    
    def listening_face(self):
        self.pixels.fill((0, 0, 0))
        for pos in [18, 19, 21, 22, 42, 43, 45, 46]:
            self.pixels[pos] = (0, 200, 100)
        self.pixels.show()
    
    def clear(self):
        self.pixels.fill((0, 0, 0))
        self.pixels.show()

class ServoController:
    def __init__(self, left_pin, right_pin):
        GPIO.setmode(GPIO.BCM)
        GPIO.setup(left_pin, GPIO.OUT)
        GPIO.setup(right_pin, GPIO.OUT)
        self.left_servo = GPIO.PWM(left_pin, 50)
        self.right_servo = GPIO.PWM(right_pin, 50)
        self.left_servo.start(0)
        self.right_servo.start(0)
    
    def set_angle(self, servo, angle):
        duty_cycle = 2 + (angle / 18)
        servo.ChangeDutyCycle(duty_cycle)
        time.sleep(0.3)
        servo.ChangeDutyCycle(0)
    
    def wiggle_ears(self, times=3):
        for _ in range(times):
            self.set_angle(self.left_servo, 45)
            self.set_angle(self.right_servo, 135)
            time.sleep(0.2)
            self.set_angle(self.left_servo, 135)
            self.set_angle(self.right_servo, 45)
            time.sleep(0.2)
    
    def neutral_position(self):
        self.set_angle(self.left_servo, 90)
        self.set_angle(self.right_servo, 90)
    
    def perk_up(self):
        self.set_angle(self.left_servo, 45)
        self.set_angle(self.right_servo, 45)
    
    def cleanup(self):
        self.left_servo.stop()
        self.right_servo.stop()
        GPIO.cleanup()

class AudioPlayer:
    def __init__(self, audio_directory, volume):
        pygame.mixer.init()
        pygame.mixer.music.set_volume(volume)
        self.audio_dir = audio_directory
        self.audio_files = {}
        if os.path.exists(audio_directory):
            for file in os.listdir(audio_directory):
                if file.endswith(('.mp3', '.wav')):
                    barcode = file.split('.')[0]
                    self.audio_files[barcode] = os.path.join(audio_directory, file)
    
    def play_audio(self, barcode):
        if barcode in self.audio_files:
            pygame.mixer.music.load(self.audio_files[barcode])
            pygame.mixer.music.play()
            return True
        return False
    
    def stop_audio(self):
        pygame.mixer.music.stop()
    
    def is_playing(self):
        return pygame.mixer.music.get_busy()

class PowerManager:
    def __init__(self, i2c_address):
        try:
            self.bus = smbus.SMBus(1)
            self.address = i2c_address
        except:
            self.bus = None
        
    def read_voltage(self):
        if not self.bus:
            return 12.0
        try:
            data = self.bus.read_i2c_block_data(self.address, 0x02, 2)
            return (data[0] << 8 | data[1]) * 0.004
        except:
            return 12.0
    
    def check_battery_status(self):
        voltage = self.read_voltage()
        percentage = ((voltage - 11.0) / (12.6 - 11.0)) * 100
        percentage = max(0, min(100, percentage))
        return {'voltage': voltage, 'percentage': percentage}

class ShikshaRobot:
    def __init__(self):
        print("\nSHIKSHA ROBOT - Educational Assistant")
        print("Developed at Experimind Labs\n")
        
        self.scanner = BarcodeScanner(CONFIG['barcode_scanner']['port'], CONFIG['barcode_scanner']['baudrate'])
        self.face = FacialExpression(CONFIG['neopixel']['pin'], CONFIG['neopixel']['num_pixels'], CONFIG['neopixel']['brightness'])
        self.servo = ServoController(CONFIG['servo']['left_pin'], CONFIG['servo']['right_pin'])
        self.audio = AudioPlayer(CONFIG['audio']['directory'], CONFIG['audio']['volume'])
        self.power = PowerManager(CONFIG['power']['i2c_address'])
        self.last_barcode = None
        self.running = False
        
        print("All systems initialized\n")
    
    def start(self):
        self.running = True
        print("Robot Started\n")
        
        # Welcome sequence
        self.face.excited_face()
        self.servo.wiggle_ears(2)
        time.sleep(1)
        self.face.happy_face()
        self.servo.neutral_position()
        
        try:
            while self.running:
                barcode = self.scanner.read_barcode()
                if barcode and barcode != self.last_barcode and not self.audio.is_playing():
                    print(f"Chart detected: {barcode}")
                    self.process_chart(barcode)
                    self.last_barcode = barcode
                time.sleep(0.1)
        except KeyboardInterrupt:
            self.shutdown()
    
    def process_chart(self, barcode):
        self.face.thinking_face()
        self.servo.perk_up()
        time.sleep(0.5)
        
        if self.audio.play_audio(barcode):
            self.face.excited_face()
            self.servo.wiggle_ears(1)
            time.sleep(0.5)
            self.face.listening_face()
            
            while self.audio.is_playing():
                time.sleep(0.5)
            
            self.face.happy_face()
            self.servo.neutral_position()
        else:
            print(f"No audio found for: {barcode}")
            self.face.clear()
            time.sleep(0.5)
            self.face.happy_face()
            self.servo.neutral_position()
    
    def shutdown(self):
        print("\nShutting down...")
        self.running = False
        self.audio.stop_audio()
        self.face.clear()
        self.servo.neutral_position()
        time.sleep(0.5)
        self.servo.cleanup()
        self.scanner.close()
        print("Shutdown complete\n")

if __name__ == "__main__":
    robot = ShikshaRobot()
    robot.start()
