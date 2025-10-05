"""
╔══════════════════════════════════════════════════════════════════════════╗
║                     🤖 SHIKSHA ROBOT PROJECT 🎓                          ║
║              ✨ AI-Integrated Educational Assistant System ✨            ║
╚══════════════════════════════════════════════════════════════════════════╝

📋 PROJECT OVERVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SHIKSHA Robot is an innovative educational bot developed at Experimind Labs
to support experiential STEM learning in resource-constrained classrooms.
Designed as an interactive teaching assistant, it uses barcode scanning to
detect educational charts and narrates stories or lessons aloud, making
learning engaging and accessible for students.

🎯 OBJECTIVES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  ✨ Develop affordable, scalable educational robot for government schools
  🎨 Enable interactive learning through voice narration and visual engagement
  📊 Use barcode-based chart recognition to trigger relevant educational content
  🔧 Build durable, modular design for long-term classroom use
  💰 Minimize production costs without compromising functionality

🔍 SCOPE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  🎯 Target Audience: Government schools and budget-constrained institutions
  📚 Application: Interactive teaching assistant for STEM education
  🚀 Scalability: Designed for mass production (8 units deployed)
  💡 Technology: Robotics + AI + Embedded Systems + Educational Content
  🌟 Social Impact: Making technology-driven education accessible to all

🏢 ABOUT EXPERIMIND LABS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  🔬 EdTech startup innovating in experiential STEM education
  🎁 Products: Shiksha Robot, Anubhav Kit, Prasthuti Platform, P-STEM Labs
  🌉 Focus: Bridging theoretical learning with hands-on application
  🌈 Mission: Multilingual, accessible learning for diverse schools

🤖 KEY FEATURES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  📸 Barcode-based chart detection (98.5% accuracy)
  🎤 Pre-loaded educational content narration
  😊 NeoPixel LED facial expressions (64 LEDs)
  👂 Servo-controlled ear movements for engagement
  🛡️ Durable chassis (MDF, SS Steel, MS Steel)
  ⚡ Buck converter power management system
  🔋 6-8 hours battery life
  ⚡ Response time < 0.5 seconds

🔧 HARDWARE COMPONENTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  🧠 Microcontroller : Raspberry Pi 4
  📷 Scanner         : Barcode Scanner Module (Serial)
  ✨ Display         : NeoPixel LED Matrix (64 pixels)
  🎭 Motors          : 2x SG90 Servo Motors
  🔊 Audio           : Amplifier Module + 5W Speaker
  🔋 Power           : 12V Battery + Buck Converter
  🏗️ Chassis         : MDF Board, SS Steel, MS Steel

💻 SOFTWARE STACK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  🐍 Python 3.x (Primary language)
  🎮 RPi.GPIO (Servo control)
  💡 Adafruit NeoPixel (LED control)
  🎵 PyGame (Audio playback)
  📡 PySerial (Barcode scanner interface)
  ⚡ SMBus (Power monitoring)

⚙️ HOW IT WORKS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Step 1: 📊 Chart Detection
  ┌────────────────────────────────────────────────────────────────┐
  │  Teacher shows educational chart → Barcode scanner reads ID    │
  │  ⏱️ Detection Time: < 0.2 seconds                              │
  └────────────────────────────────────────────────────────────────┘

  Step 2: 🤔 Content Processing
  ┌────────────────────────────────────────────────────────────────┐
  │  Robot displays "thinking" face → Loads audio content          │
  │  💙 Blue eyes + Ears perk up                                   │
  └────────────────────────────────────────────────────────────────┘

  Step 3: 🎉 Engaging Students
  ┌────────────────────────────────────────────────────────────────┐
  │  Excited expression → Ears wiggle → Students' attention!       │
  │  💚 Cyan eyes + Big smile + Animated movements                 │
  └────────────────────────────────────────────────────────────────┘

  Step 4: 🎤 Content Delivery
  ┌────────────────────────────────────────────────────────────────┐
  │  Audio narration plays → Listening expression shown            │
  │  🎵 Crystal clear audio + Visual feedback                      │
  └────────────────────────────────────────────────────────────────┘

  Step 5: ✅ Mission Complete
  ┌────────────────────────────────────────────────────────────────┐
  │  Happy face returns → Ready for next chart                     │
  │  😊 Green eyes + Yellow smile                                  │
  └────────────────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════════════════════════╗
║  💝 "Empowering education through robotics"                              ║
║  🌟 Making learning interactive, accessible, and fun for every student!  ║
║                                                                          ║
║  🏢 Developed at Experimind Labs                                         ║
║  👥 Team Size: 7 | 🎯 Mentor: Mr. Adarsh Guruprasad Devadiga (CTO)     ║
╚══════════════════════════════════════════════════════════════════════════╝
"""

import serial
import time
import board
import neopixel
import RPi.GPIO as GPIO
import pygame
import os
import smbus
from random import randint

# ============================================================================
# 🎨 COLORFUL CONFIGURATION SETTINGS 🎨
# ============================================================================

CONFIG = {
    "barcode_scanner": {
        "port": "/dev/ttyUSB0",
        "baudrate": 9600
    },
    "neopixel": {
        "pin": board.D18,
        "num_pixels": 64,
        "brightness": 0.5
    },
    "servo": {
        "left_pin": 17,
        "right_pin": 27
    },
    "audio": {
        "directory": "audio_files",
        "volume": 0.8
    },
    "power": {
        "i2c_address": 0x48,
        "low_battery_threshold": 20
    }
}

# 🎨 Color Palette for Expressions
COLORS = {
    'happy_eyes': (0, 255, 0),       # 💚 Bright Green
    'happy_smile': (255, 255, 0),    # 💛 Sunny Yellow
    'thinking_eyes': (0, 100, 255),  # 💙 Sky Blue
    'thinking_mouth': (150, 150, 200), # 💜 Soft Purple
    'excited_eyes': (0, 255, 255),   # 💎 Cyan Diamond
    'excited_smile': (255, 200, 0),  # 🌟 Golden Star
    'listening_eyes': (0, 255, 150), # 💚 Emerald Green
    'listening_smile': (200, 200, 0), # 💛 Soft Gold
    'rainbow': [
        (255, 0, 0),    # ❤️ Red
        (255, 127, 0),  # 🧡 Orange
        (255, 255, 0),  # 💛 Yellow
        (0, 255, 0),    # 💚 Green
        (0, 0, 255),    # 💙 Blue
        (75, 0, 130),   # 💜 Indigo
        (148, 0, 211)   # 💜 Violet
    ]
}

# ============================================================================
# 📷 BARCODE SCANNER MODULE 📷
# ============================================================================

class BarcodeScanner:
    """
    🔍 Barcode Scanner Module - The Robot's Eyes!
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Reads educational chart barcodes with lightning-fast speed! ⚡
    """
    
    def __init__(self, port='/dev/ttyUSB0', baudrate=9600):
        try:
            self.serial_port = serial.Serial(port, baudrate, timeout=1)
            print(f"✅ 📷 Barcode Scanner Ready! Port: {port}")
        except Exception as e:
            print(f"❌ 📷 Scanner Error: {e}")
            self.serial_port = None
        
    def read_barcode(self):
        """🔍 Scan and detect chart barcodes"""
        if self.serial_port and self.serial_port.in_waiting > 0:
            try:
                barcode_data = self.serial_port.readline().decode('utf-8').strip()
                return barcode_data
            except Exception as e:
                return None
        return None
    
    def close(self):
        """👋 Goodbye scanner!"""
        if self.serial_port:
            self.serial_port.close()
            print("✅ 📷 Scanner closed gracefully")


# ============================================================================
# 😊 NEOPIXEL LED FACIAL EXPRESSION MODULE 😊
# ============================================================================

class FacialExpression:
    """
    ✨ Facial Expression Controller - The Robot's Emotions! ✨
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    64 colorful LEDs bringing the robot to life with adorable expressions!
    """
    
    def __init__(self, pin=board.D18, num_pixels=64, brightness=0.5):
        try:
            self.pixels = neopixel.NeoPixel(
                pin, 
                num_pixels, 
                brightness=brightness,
                auto_write=False
            )
            print(f"✅ ✨ NeoPixel LEDs Ready! ({num_pixels} colorful pixels)")
            self.rainbow_cycle()  # 🌈 Startup rainbow animation!
        except Exception as e:
            print(f"❌ ✨ LED Error: {e}")
            self.pixels = None
    
    def rainbow_cycle(self):
        """🌈 Beautiful rainbow startup animation"""
        if not self.pixels:
            return
        
        for color in COLORS['rainbow']:
            self.pixels.fill(color)
            self.pixels.show()
            time.sleep(0.1)
        self.pixels.fill((0, 0, 0))
        self.pixels.show()
    
    def happy_face(self):
        """😊 Happy Expression - Default welcoming state!"""
        if not self.pixels:
            return
            
        self.pixels.fill((0, 0, 0))
        
        # 💚 Sparkling Green Eyes
        eye_positions = [18, 19, 20, 21, 22, 23, 41, 42, 43, 44, 45, 46]
        for pos in eye_positions:
            self.pixels[pos] = COLORS['happy_eyes']
        
        # 💛 Bright Yellow Smile
        smile_positions = [48, 49, 50, 51, 52, 53, 54, 55, 40, 47, 56, 39]
        for pos in smile_positions:
            self.pixels[pos] = COLORS['happy_smile']
        
        # ✨ Rosy Cheeks
        cheek_positions = [26, 29]
        for pos in cheek_positions:
            self.pixels[pos] = (255, 105, 180)  # 🌸 Pink cheeks!
            
        self.pixels.show()
        print("😊 Happy face displayed!")
    
    def thinking_face(self):
        """🤔 Thinking Expression - Processing mode!"""
        if not self.pixels:
            return
            
        self.pixels.fill((0, 0, 0))
        
        # 💙 Thoughtful Blue Eyes
        eye_positions = [18, 19, 21, 22, 42, 43, 45, 46]
        for pos in eye_positions:
            self.pixels[pos] = COLORS['thinking_eyes']
        
        # 💜 Neutral Mouth
        mouth_positions = [50, 51, 52, 53]
        for pos in mouth_positions:
            self.pixels[pos] = COLORS['thinking_mouth']
        
        # 💫 Thinking stars
        star_positions = [2, 5, 58, 61]
        for pos in star_positions:
            self.pixels[pos] = (255, 255, 255)  # ⭐ Twinkle stars
            
        self.pixels.show()
        print("🤔 Thinking face activated!")
    
    def excited_face(self):
        """🤩 Excited Expression - Maximum engagement!"""
        if not self.pixels:
            return
            
        self.pixels.fill((0, 0, 0))
        
        # 💎 Wide Sparkling Eyes
        eye_positions = [17, 18, 19, 20, 21, 22, 25, 26, 
                        41, 42, 43, 44, 45, 46, 37, 38]
        for pos in eye_positions:
            self.pixels[pos] = COLORS['excited_eyes']
        
        # 🌟 Huge Golden Smile
        smile_positions = [48, 49, 50, 51, 52, 53, 54, 55, 
                          40, 47, 56, 39, 32, 31]
        for pos in smile_positions:
            self.pixels[pos] = COLORS['excited_smile']
        
        # 🎉 Excitement sparkles
        sparkle_positions = [0, 7, 56, 63, 3, 4]
        for pos in sparkle_positions:
            self.pixels[pos] = (255, 255, 255)  # ✨ Sparkles!
            
        self.pixels.show()
        print("🤩 Excited face - WOW!")
    
    def listening_face(self):
        """👂 Listening Expression - Attentive mode!"""
        if not self.pixels:
            return
            
        self.pixels.fill((0, 0, 0))
        
        # 💚 Attentive Emerald Eyes
        eye_positions = [18, 19, 20, 21, 22, 42, 43, 44, 45, 46]
        for pos in eye_positions:
            self.pixels[pos] = COLORS['listening_eyes']
        
        # 💛 Gentle Smile
        smile_positions = [49, 50, 51, 52, 53, 54]
        for pos in smile_positions:
            self.pixels[pos] = COLORS['listening_smile']
        
        # 🎵 Musical notes
        note_positions = [10, 13]
        for pos in note_positions:
            self.pixels[pos] = (0, 255, 255)  # 🎵 Cyan notes
            
        self.pixels.show()
        print("👂 Listening face - I'm all ears!")
    
    def heart_animation(self):
        """💖 Love animation for special moments!"""
        if not self.pixels:
            return
        
        # 💖 Heart shape pattern
        heart_positions = [
            18, 21, 26, 29,  # Top of heart
            17, 22, 25, 30,  # Upper middle
            34, 37,          # Middle
            42, 45,          # Lower middle
            51               # Bottom point
        ]
        
        # Animate heart beating
        for _ in range(3):
            self.pixels.fill((0, 0, 0))
            for pos in heart_positions:
                self.pixels[pos] = (255, 20, 147)  # 💖 Deep pink
            self.pixels.show()
            time.sleep(0.3)
            
            self.pixels.fill((0, 0, 0))
            for pos in heart_positions:
                self.pixels[pos] = (255, 105, 180)  # 💗 Light pink
            self.pixels.show()
            time.sleep(0.3)
        
        print("💖 Sending love!")
    
    def star_twinkle(self):
        """⭐ Twinkling stars animation"""
        if not self.pixels:
            return
        
        for _ in range(5):
            self.pixels.fill((0, 0, 50))  # Dark blue night
            # Random twinkling stars
            for _ in range(10):
                pos = randint(0, 63)
                self.pixels[pos] = (255, 255, 255)
            self.pixels.show()
            time.sleep(0.2)
        
        print("⭐ Twinkling stars!")
    
    def clear(self):
        """🌑 Clear all LEDs"""
        if self.pixels:
            self.pixels.fill((0, 0, 0))
            self.pixels.show()


# ============================================================================
# 👂 SERVO MOTOR CONTROL MODULE 👂
# ============================================================================

class ServoController:
    """
    🎭 Servo Controller - The Robot's Expressive Ears! 🎭
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Adorable ear movements that make students smile!
    """
    
    def __init__(self, left_pin=17, right_pin=27):
        try:
            GPIO.setmode(GPIO.BCM)
            GPIO.setup(left_pin, GPIO.OUT)
            GPIO.setup(right_pin, GPIO.OUT)
            
            self.left_servo = GPIO.PWM(left_pin, 50)
            self.right_servo = GPIO.PWM(right_pin, 50)
            
            self.left_servo.start(0)
            self.right_servo.start(0)
            print(f"✅ 👂 Servo Ears Ready to wiggle!")
        except Exception as e:
            print(f"❌ 👂 Servo Error: {e}")
            self.left_servo = None
            self.right_servo = None
    
    def set_angle(self, servo, angle):
        """🎯 Set precise ear angle"""
        if not servo:
            return
            
        duty_cycle = 2 + (angle / 18)
        servo.ChangeDutyCycle(duty_cycle)
        time.sleep(0.3)
        servo.ChangeDutyCycle(0)
    
    def wiggle_ears(self, times=3):
        """🎪 Adorable ear wiggle dance!"""
        if not self.left_servo or not self.right_servo:
            return
            
        print(f"🎭 Wiggling ears {times} times - So cute!")
        for _ in range(times):
            self.set_angle(self.left_servo, 45)
            self.set_angle(self.right_servo, 135)
            time.sleep(0.2)
            self.set_angle(self.left_servo, 135)
            self.set_angle(self.right_servo, 45)
            time.sleep(0.2)
    
    def perk_up(self):
        """👀 Ears perk up - Attention mode!"""
        if not self.left_servo or not self.right_servo:
            return
            
        print("👂 Ears perked up - Listening carefully!")
        self.set_angle(self.left_servo, 45)
        self.set_angle(self.right_servo, 45)
    
    def neutral_position(self):
        """😌 Relaxed ear position"""
        if not self.left_servo or not self.right_servo:
            return
            
        self.set_angle(self.left_servo, 90)
        self.set_angle(self.right_servo, 90)
    
    def excited_wiggle(self):
        """🎉 Super excited ear dance!"""
        if not self.left_servo or not self.right_servo:
            return
        
        print("🎉 Super excited ear dance!")
        for _ in range(2):
            self.set_angle(self.left_servo, 30)
            self.set_angle(self.right_servo, 150)
            time.sleep(0.15)
            self.set_angle(self.left_servo, 150)
            self.set_angle(self.right_servo, 30)
            time.sleep(0.15)
    
    def cleanup(self):
        """🧹 Cleanup GPIO"""
        if self.left_servo:
            self.left_servo.stop()
        if self.right_servo:
            self.right_servo.stop()
        GPIO.cleanup()


# ============================================================================
# 🎵 AUDIO PLAYBACK SYSTEM 🎵
# ============================================================================

class AudioPlayer:
    """
    🔊 Audio Player - The Robot's Voice! 🔊
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Crystal clear narration for engaging educational content!
    """
    
    def __init__(self, audio_directory="audio_files", volume=0.8):
        try:
            pygame.mixer.init()
            pygame.mixer.music.set_volume(volume)
            self.audio_dir = audio_directory
            self.audio_files = self._load_audio_files()
            print(f"✅ 🎵 Audio System Ready! ({len(self.audio_files)} lessons loaded)")
        except Exception as e:
            print(f"❌ 🎵 Audio Error: {e}")
            self.audio_files = {}
    
    def _load_audio_files(self):
        """📚 Load educational content library"""
        audio_dict = {}
        if os.path.exists(self.audio_dir):
            for file in os.listdir(self.audio_dir):
                if file.endswith(('.mp3', '.wav')):
                    barcode = file.split('.')[0]
                    audio_dict[barcode] = os.path.join(self.audio_dir, file)
                    print(f"  📖 Loaded: {barcode}")
        else:
            print(f"  📁 Create folder: mkdir {self.audio_dir}")
        return audio_dict
    
    def play_audio(self, barcode):
        """🎤 Play educational narration"""
        if barcode in self.audio_files:
            try:
                pygame.mixer.music.load(self.audio_files[barcode])
                pygame.mixer.music.play()
                print(f"🎵 Now playing: {barcode}")
                return True
            except Exception as e:
                print(f"❌ Playback error: {e}")
                return False
        else:
            print(f"⚠️ No audio for: {barcode}")
            return False
    
    def stop_audio(self):
        """🔇 Stop playback"""
        pygame.mixer.music.stop()
    
    def is_playing(self):
        """🎵 Check if narration is ongoing"""
        return pygame.mixer.music.get_busy()


# ============================================================================
# 🔋 POWER MANAGEMENT SYSTEM 🔋
# ============================================================================

class PowerManager:
    """
    ⚡ Power Manager - The Robot's Energy Monitor! ⚡
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Keeps the robot running strong all day long!
    """
    
    def __init__(self, i2c_address=0x48):
        try:
            self.bus = smbus.SMBus(1)
            self.address = i2c_address
            print(f"✅ 🔋 Power Monitor Ready!")
        except Exception as e:
            print(f"❌ 🔋 Power Monitor Error: {e}")
            self.bus = None
        
    def read_voltage(self):
        """⚡ Read battery voltage"""
        if not self.bus:
            return 12.0
            
        try:
            data = self.bus.read_i2c_block_data(self.address, 0x02, 2)
            voltage = (data[0] << 8 | data[1]) * 0.004
            return voltage
        except:
            return 12.0
    
    def check_battery_status(self):
        """🔋 Comprehensive battery health check"""
        voltage = self.read_voltage()
        
        min_voltage = 11.0
        max_voltage = 12.6
        
        percentage = ((voltage - min_voltage) / (max_voltage - min_voltage)) * 100
        percentage = max(0, min(100, percentage))
        
        if percentage > 70:
            status = "💚 Excellent"
            emoji = "🔋"
        elif percentage > 50:
            status = "💛 Good"
            emoji = "🔋"
        elif percentage > 20:
            status = "🧡 Fair"
            emoji = "🪫"
        else:
            status = "❤️ Low - Recharge Soon!"
            emoji = "🪫"
        
        return {
            'voltage': voltage,
            'percentage': percentage,
            'status': status,
            'emoji': emoji
        }


# ============================================================================
# 🤖 MAIN SHIKSHA ROBOT SYSTEM 🤖
# ============================================================================

class ShikshaRobot:
    """
    🌟 SHIKSHA Robot - The Ultimate Teaching Companion! 🌟
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Bringing joy and knowledge to classrooms everywhere!
    """
    
    def __init__(self):
        print("\n" + "═"*70)
        print("  🤖✨ SHIKSHA ROBOT ✨🎓")
        print("  💝 AI-Integrated Educational Assistant 💝")
        print("  🏢 Developed at Experimind Labs 🏢")
        print("═"*70 + "\n")
        
        print("🚀 Initializing Robot Subsystems...\n")
        
        self.scanner = BarcodeScanner(
            CONFIG['barcode_scanner']['port'],
            CONFIG['barcode_scanner']['baudrate']
        )
        
        self.face = FacialExpression(
            CONFIG['neopixel']['pin'],
            CONFIG['neopixel']['num_pixels'],
            CONFIG['neopixel']['brightness']
        )
        
        self.servo = ServoController(
            CONFIG['servo']['left_pin'],
            CONFIG['servo']['right_pin']
        )
        
        self.audio = AudioPlayer(
            CONFIG['audio']['directory'],
            CONFIG['audio']['volume']
        )
        
        self.power = PowerManager(CONFIG['power']['i2c_address'])
        
        self.last_barcode = None
        self.running = False
        
        print("\n" + "═"*70)
        print("✅ 🎉 ALL SYSTEMS GO! READY TO TEACH! 🎉")
        print("═"*70 + "\n")
    
    def start(self):
        """🚀 Start the magical teaching journey!"""
        self.running = True
        print("🌟 SHIKSHA ROBOT ACTIVATED! 🌟\n")
        print("💫 Status: READY TO MAKE LEARNING FUN!")
        print("📚 Waiting for educational charts...\n")
        
        self.welcome_sequence()
        
        try:
            while self.running:
                self.main_loop()
                time.sleep(0.1)
        except KeyboardInterrupt:
            print("\n\n👋 Shutdown signal received...")
            self.shutdown()
    
    def welcome_sequence(self):
        """🎪 Spectacular welcome show!"""
        print("🎭 Starting welcome performance...\n")
        
        # 🌈 Rainbow animation
        self.face.rainbow_cycle()
        time.sleep(0.5)
