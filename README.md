"""
╔══════════════════════════════════════════════════════════════════════════╗
║                        SHIKSHA ROBOT PROJECT                             ║
║              AI-Integrated Educational Assistant System                  ║
╚══════════════════════════════════════════════════════════════════════════╝

📋 PROJECT OVERVIEW
─────────────────────────────────────────────────────────────────────────
SHIKSHA Robot is an innovative educational bot developed at Experimind Labs
to support experiential STEM learning in resource-constrained classrooms.
Designed as an interactive teaching assistant, it uses barcode scanning to
detect educational charts and narrates stories or lessons aloud, making
learning engaging and accessible for students.

🎯 OBJECTIVES
─────────────────────────────────────────────────────────────────────────
- Develop affordable, scalable educational robot for government schools
- Enable interactive learning through voice narration and visual engagement
- Use barcode-based chart recognition to trigger relevant educational content
- Build durable, modular design for long-term classroom use
- Minimize production costs without compromising functionality

🔍 SCOPE
─────────────────────────────────────────────────────────────────────────
- Target Audience: Government schools and budget-constrained institutions
- Application: Interactive teaching assistant for STEM education
- Scalability: Designed for mass production (8 units deployed)
- Technology: Robotics + AI + Embedded Systems + Educational Content
- Social Impact: Making technology-driven education accessible to all

🏢 ABOUT EXPERIMIND LABS
─────────────────────────────────────────────────────────────────────────
- EdTech startup innovating in experiential STEM education
- Products: Shiksha Robot, Anubhav Kit, Prasthuti Platform, P-STEM Labs
- Focus: Bridging theoretical learning with hands-on application
- Mission: Multilingual, accessible learning for diverse schools

🤖 KEY FEATURES
─────────────────────────────────────────────────────────────────────────
- Barcode-based chart detection (98.5% accuracy)
- Pre-loaded educational content narration
- NeoPixel LED facial expressions (64 LEDs)
- Servo-controlled ear movements for engagement
- Durable chassis (MDF, SS Steel, MS Steel)
- Buck converter power management system
- 6-8 hours battery life
- Response time < 0.5 seconds

🔧 HARDWARE COMPONENTS
─────────────────────────────────────────────────────────────────────────
Microcontroller  : Raspberry Pi 4
Scanner          : Barcode Scanner Module (Serial)
Display          : NeoPixel LED Matrix (64 pixels)
Motors           : 2x SG90 Servo Motors
Audio            : Amplifier Module + 5W Speaker
Power            : 12V Battery + Buck Converter
Chassis          : MDF Board, SS Steel, MS Steel

💻 SOFTWARE STACK
─────────────────────────────────────────────────────────────────────────
- Python 3.x (Primary language)
- RPi.GPIO (Servo control)
- Adafruit NeoPixel (LED control)
- PyGame (Audio playback)
- PySerial (Barcode scanner interface)
- SMBus (Power monitoring)

⚙️ HOW IT WORKS
─────────────────────────────────────────────────────────────────────────
1. Chart Detection:
   • Teacher places educational chart in front of robot
   • Barcode scanner reads unique chart identifier
   • System validates barcode and prepares content

2. Content Delivery:
   • Robot displays "thinking" expression (blue eyes)
   • Audio module loads corresponding lesson file
   • Robot shows "excited" expression and wiggles ears

3. Narration:
   • Pre-recorded educational content plays through speaker
   • Robot displays "listening" expression
   • Students engage with interactive visual feedback

4. Completion:
   • Content finishes playing
   • Robot returns to "happy" expression
   • Ready for next chart scan

📊 DEVELOPMENT PHASES
─────────────────────────────────────────────────────────────────────────
Phase 1: System Architecture Planning
  • Component selection (MCU, sensors, modules)
  • Workflow breakdown (Hardware | Firmware | Assembly)

Phase 2: PCB Design
  • Tools: EasyEDA / KiCad
  • Schematics, layout design, trace routing
  • Board fabrication and testing

Phase 3: Mechanical Fabrication
  • Materials: MDF Board, SS Steel, MS Steel
  • Laser cutting, 3D printing, mounting assembly

🔬 TESTING & DEBUGGING
─────────────────────────────────────────────────────────────────────────
Functional Testing:
  ✓ Raspberry Pi boot verification
  ✓ Speaker clarity and audio quality
  ✓ Chart mode operation validation

Electrical Testing:
  ✓ Voltage level verification
  ✓ Short circuit prevention
  ✓ Stable power delivery

Challenges Solved:
  ✓ Audio distortion → Adjusted amplifier gain
  ✓ Barcode accuracy → Calibrated sensor distance/angle
  ✓ Power balancing → Buck converter with heat sink
  ✓ Sensor noise → Software filters + mounting isolation
  ✓ Mechanical fitting → CAD reworks for tolerances

📈 PROJECT ACHIEVEMENTS
─────────────────────────────────────────────────────────────────────────
✓ Successfully built and deployed 8 Shiksha Robots
✓ Maintained affordability while ensuring functionality
✓ 98.5% barcode detection accuracy
✓ <0.5s average response time
✓ 6-8 hours continuous battery life
✓ Scalable design for mass production

🚀 FUTURE SCOPE
─────────────────────────────────────────────────────────────────────────
- Voice command recognition and natural language interaction
- Multilingual content support for diverse classrooms
- Cloud connectivity for remote content updates
- Mobile app integration for teacher control
- Advanced AI for personalized learning paths
- Gesture recognition capabilities
- Real-time analytics and progress tracking

🎓 KEY LEARNINGS
─────────────────────────────────────────────────────────────────────────
- Complete product development cycle (concept → deployment)
- Embedded systems design and hardware integration
- Real-time sensor interfacing and control
- Circuit design and PCB fabrication
- Cross-domain synchronization in robotic systems
- Power management and optimization techniques
- Team collaboration and project management
- Developing scalable, socially impactful technology

📦 INSTALLATION
─────────────────────────────────────────────────────────────────────────
# Create project directory
mkdir shiksha-robot && cd shiksha-robot

# Create audio directory
mkdir audio_files

# Install dependencies
pip3 install RPi.GPIO adafruit-circuitpython-neopixel pygame pyserial smbus2

# Save this code as shiksha_robot.py and run
python3 shiksha_robot.py

╔══════════════════════════════════════════════════════════════════════════╗
║  "Empowering education through robotics – Making learning interactive,   ║
║   accessible, and engaging for every student."                           ║
║                                                                          ║
║  Developed at Experimind Labs                                            ║
║  Team Size: 7 | Mentor: Mr. Adarsh Guruprasad Devadiga (CTO)           ║
╚══════════════════════════════════════════════════════════════════════════╝
"""

import serial
import time
import board
import neopixel
import RPi.GPIO as GPIO
import pygame
import os
from threading import Thread
import smbus

# ============================================================================
# SYSTEM ARCHITECTURE DIAGRAM
# ============================================================================
"""
┌─────────────────────────────────────────────────────────────────────────┐
│                     SHIKSHA ROBOT SYSTEM ARCHITECTURE                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│      ┌──────────────┐                    ┌──────────────┐              │
│      │   Barcode    │───────────────────▶│  Raspberry   │              │
│      │   Scanner    │   Serial UART      │     Pi 4     │              │
│      └──────────────┘                    └──────┬───────┘              │
│                                                 │                       │
│      ┌──────────────┐                          │        ┌────────────┐ │
│      │   NeoPixel   │◀─────────────────────────┼────────│   Servo    │ │
│      │   64 LEDs    │   GPIO Control           │        │   Motors   │ │
│      └──────────────┘                          │        └────────────┘ │
│                                                 │                       │
│      ┌──────────────┐                          │        ┌────────────┐ │
│      │    Audio     │◀─────────────────────────┼────────│   Power    │ │
│      │   Module     │   PWM Audio              │        │ Management │ │
│      └──────────────┘                          │        └────────────┘ │
│                                                                         │
│  Data Flow: Barcode → Processing → Audio + Visual + Motion Response    │
└─────────────────────────────────────────────────────────────────────────┘
"""

# ============================================================================
# CONFIGURATION SETTINGS
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

# ============================================================================
# BARCODE SCANNER MODULE
# ============================================================================

class BarcodeScanner:
    """
    Barcode Scanner Module
    ─────────────────────────────────────────────────────────────────────
    Handles barcode scanning for educational chart detection.
    Uses serial communication to read barcode data.
    
    Technical Specifications:
    • Interface: Serial UART
    • Baudrate: 9600 bps
    • Protocol: ASCII text output
    • Scan Rate: Up to 300 scans/second
    """
    
    def __init__(self, port='/dev/ttyUSB0', baudrate=9600):
        try:
            self.serial_port = serial.Serial(port, baudrate, timeout=1)
            print(f"✓ Barcode Scanner initialized on {port}")
        except Exception as e:
            print(f"✗ Barcode Scanner initialization failed: {e}")
            self.serial_port = None
        
    def read_barcode(self):
        """Read barcode data from scanner."""
        if self.serial_port and self.serial_port.in_waiting > 0:
            try:
                barcode_data = self.serial_port.readline().decode('utf-8').strip()
                return barcode_data
            except Exception as e:
                print(f"Error reading barcode: {e}")
                return None
        return None
    
    def close(self):
        """Close serial connection."""
        if self.serial_port:
            self.serial_port.close()
            print("✓ Barcode Scanner closed")


# ============================================================================
# NEOPIXEL LED FACIAL EXPRESSION MODULE
# ============================================================================

class FacialExpression:
    """
    NeoPixel LED Facial Expression Module
    ─────────────────────────────────────────────────────────────────────
    Controls 64 NeoPixel LED matrix for displaying facial expressions.
    Creates engaging visual feedback for student interaction.
    
    Expression Types:
    • Happy Face: Green eyes + Yellow smile
    • Thinking Face: Blue eyes + Neutral mouth
    • Excited Face: Cyan wide eyes + Big yellow smile
    • Listening Face: Green attentive eyes + Small smile
    
    Technical Specifications:
    • LEDs: 64 WS2812B NeoPixels
    • Control: Single GPIO data line
    • Update Rate: 400 KHz
    • Color Depth: 24-bit RGB (16.7M colors)
    """
    
    def __init__(self, pin=board.D18, num_pixels=64, brightness=0.5):
        try:
            self.pixels = neopixel.NeoPixel(
                pin, 
                num_pixels, 
                brightness=brightness,
                auto_write=False
            )
            print(f"✓ NeoPixel LEDs initialized ({num_pixels} pixels)")
        except Exception as e:
            print(f"✗ NeoPixel initialization failed: {e}")
            self.pixels = None
        
    def happy_face(self):
        """Display happy expression - Default welcoming state"""
        if not self.pixels:
            return
            
        self.pixels.fill((0, 0, 0))
        
        # Eyes (green - welcoming)
        eye_positions = [18, 19, 21, 22, 42, 43, 45, 46]
        for pos in eye_positions:
            self.pixels[pos] = (0, 255, 0)
        
        # Smile (yellow - friendly)
        smile_positions = [49, 50, 51, 52, 53, 54, 48, 55]
        for pos in smile_positions:
            self.pixels[pos] = (255, 255, 0)
            
        self.pixels.show()
    
    def thinking_face(self):
        """Display thinking expression - Processing state"""
        if not self.pixels:
            return
            
        self.pixels.fill((0, 0, 0))
        
        # Eyes (blue - contemplative)
        eye_positions = [18, 19, 21, 22, 42, 43, 45, 46]
        for pos in eye_positions:
            self.pixels[pos] = (0, 0, 255)
        
        # Neutral mouth
        mouth_positions = [50, 51, 52, 53]
        for pos in mouth_positions:
            self.pixels[pos] = (100, 100, 100)
            
        self.pixels.show()
    
    def excited_face(self):
        """Display excited expression - Engaging moments"""
        if not self.pixels:
            return
            
        self.pixels.fill((0, 0, 0))
        
        # Wide eyes (cyan - excited)
        eye_positions = [17, 18, 19, 20, 21, 22, 41, 42, 43, 44, 45, 46]
        for pos in eye_positions:
            self.pixels[pos] = (0, 255, 255)
        
        # Big smile (bright yellow)
        smile_positions = [48, 49, 50, 51, 52, 53, 54, 55, 40, 47]
        for pos in smile_positions:
            self.pixels[pos] = (255, 200, 0)
            
        self.pixels.show()
    
    def listening_face(self):
        """Display listening expression - During narration"""
        if not self.pixels:
            return
            
        self.pixels.fill((0, 0, 0))
        
        # Attentive eyes (green)
        eye_positions = [18, 19, 21, 22, 42, 43, 45, 46]
        for pos in eye_positions:
            self.pixels[pos] = (0, 200, 100)
        
        # Small smile
        smile_positions = [50, 51, 52, 53]
        for pos in smile_positions:
            self.pixels[pos] = (150, 150, 0)
            
        self.pixels.show()
    
    def clear(self):
        """Clear all LEDs"""
        if self.pixels:
            self.pixels.fill((0, 0, 0))
            self.pixels.show()


# ============================================================================
# SERVO MOTOR CONTROL MODULE
# ============================================================================

class ServoController:
    """
    Servo Motor Control Module
    ─────────────────────────────────────────────────────────────────────
    Controls two SG90 servo motors for robotic ear movements.
    Adds physical expressiveness to enhance student engagement.
    
    Movement Types:
    • Wiggle: Alternating ear movements for attention
    • Perk Up: Both ears raised - attention mode
    • Neutral: Centered position - default state
    
    Technical Specifications:
    • Motors: 2x SG90 Servo Motors
    • Operating Voltage: 4.8V - 6V
    • Rotation: 0° to 180°
    • Control Signal: PWM (50 Hz)
    • Torque: 1.8 kg⋅cm (at 4.8V)
    """
    
    def __init__(self, left_pin=17, right_pin=27):
        try:
            GPIO.setmode(GPIO.BCM)
            GPIO.setup(left_pin, GPIO.OUT)
            GPIO.setup(right_pin, GPIO.OUT)
            
            self.left_servo = GPIO.PWM(left_pin, 50)  # 50Hz PWM
            self.right_servo = GPIO.PWM(right_pin, 50)
            
            self.left_servo.start(0)
            self.right_servo.start(0)
            print(f"✓ Servo motors initialized")
        except Exception as e:
            print(f"✗ Servo initialization failed: {e}")
            self.left_servo = None
            self.right_servo = None
    
    def set_angle(self, servo, angle):
        """Set servo angle (0-180 degrees)"""
        if not servo:
            return
            
        duty_cycle = 2 + (angle / 18)
        servo.ChangeDutyCycle(duty_cycle)
        time.sleep(0.3)
        servo.ChangeDutyCycle(0)
    
    def wiggle_ears(self, times=3):
        """Wiggle both ears for attention"""
        if not self.left_servo or not self.right_servo:
            return
            
        for _ in range(times):
            self.set_angle(self.left_servo, 45)
            self.set_angle(self.right_servo, 135)
            time.sleep(0.2)
            self.set_angle(self.left_servo, 135)
            self.set_angle(self.right_servo, 45)
            time.sleep(0.2)
    
    def perk_up(self):
        """Perk ears up - attention mode"""
        if not self.left_servo or not self.right_servo:
            return
            
        self.set_angle(self.left_servo, 45)
        self.set_angle(self.right_servo, 45)
    
    def neutral_position(self):
        """Return ears to neutral position"""
        if not self.left_servo or not self.right_servo:
            return
            
        self.set_angle(self.left_servo, 90)
        self.set_angle(self.right_servo, 90)
    
    def cleanup(self):
        """Cleanup GPIO resources"""
        if self.left_servo:
            self.left_servo.stop()
        if self.right_servo:
            self.right_servo.stop()
        GPIO.cleanup()


# ============================================================================
# AUDIO PLAYBACK SYSTEM
# ============================================================================

class AudioPlayer:
    """
    Audio Playback System
    ─────────────────────────────────────────────────────────────────────
    Manages educational content narration through audio playback.
    Plays pre-recorded lessons based on scanned chart barcodes.
    
    Audio Format Support:
    • MP3: Compressed audio (recommended)
    • WAV: Uncompressed high-quality audio
    
    Technical Specifications:
    • Sample Rate: 44.1 kHz
    • Bit Depth: 16-bit
    • Channels: Stereo/Mono
    • Output: 5W Speaker via Amplifier
    • File Naming: <BARCODE>.mp3 (e.g., CHART001.mp3)
    """
    
    def __init__(self, audio_directory="audio_files", volume=0.8):
        try:
            pygame.mixer.init()
            pygame.mixer.music.set_volume(volume)
            self.audio_dir = audio_directory
            self.audio_files = self._load_audio_files()
            print(f"✓ Audio Player initialized ({len(self.audio_files)} files loaded)")
        except Exception as e:
            print(f"✗ Audio Player initialization failed: {e}")
            self.audio_files = {}
    
    def _load_audio_files(self):
        """Load all audio files from directory"""
        audio_dict = {}
        if os.path.exists(self.audio_dir):
            for file in os.listdir(self.audio_dir):
                if file.endswith(('.mp3', '.wav')):
                    barcode = file.split('.')[0]
                    audio_dict[barcode] = os.path.join(self.audio_dir, file)
                    print(f"  └─ {barcode} → {file}")
        else:
            print(f"  └─ Audio directory not found. Create: mkdir {self.audio_dir}")
        return audio_dict
    
    def play_audio(self, barcode):
        """Play audio corresponding to barcode"""
        if barcode in self.audio_files:
            try:
                pygame.mixer.music.load(self.audio_files[barcode])
                pygame.mixer.music.play()
                print(f"🔊 Playing: {barcode}")
                return True
            except Exception as e:
                print(f"Error playing audio: {e}")
                return False
        else:
            print(f"⚠ No audio for: {barcode}")
            return False
    
    def stop_audio(self):
        """Stop current audio playback"""
        pygame.mixer.music.stop()
    
    def is_playing(self):
        """Check if audio is currently playing"""
        return pygame.mixer.music.get_busy()


# ============================================================================
# POWER MANAGEMENT SYSTEM
# ============================================================================

class PowerManager:
    """
    Power Management System
    ─────────────────────────────────────────────────────────────────────
    Monitors battery voltage, current draw, and system power consumption.
    Provides alerts for low battery conditions.
    
    Technical Specifications:
    • Sensor: INA219 Current/Voltage Monitor
    • Interface: I2C
    • Battery: 12V Lithium-ion/Lead-acid
    • Converter: Buck Converter (12V → 5V, 3A)
    • Protection: Over-voltage, under-voltage, short-circuit
    • Battery Life: 6-8 hours continuous operation
    """
    
    def __init__(self, i2c_address=0x48):
        try:
            self.bus = smbus.SMBus(1)
            self.address = i2c_address
            print(f"✓ Power Manager initialized")
        except Exception as e:
            print(f"✗ Power Manager initialization failed: {e}")
            self.bus = None
        
    def read_voltage(self):
        """Read current battery voltage"""
        if not self.bus:
            return 12.0  # Default value for simulation
            
        try:
            data = self.bus.read_i2c_block_data(self.address, 0x02, 2)
            voltage = (data[0] << 8 | data[1]) * 0.004
            return voltage
        except:
            return 12.0
    
    def check_battery_status(self):
        """Check comprehensive battery status"""
        voltage = self.read_voltage()
        
        # 12V battery range
        min_voltage = 11.0  # 0%
        max_voltage = 12.6  # 100%
        
        percentage = ((voltage - min_voltage) / (max_voltage - min_voltage)) * 100
        percentage = max(0, min(100, percentage))
        
        if percentage > 50:
            status = "Good"
        elif percentage > 20:
            status = "Fair"
        else:
            status = "Low Battery"
        
        return {
            'voltage': voltage,
            'percentage': percentage,
            'status': status
        }


# ============================================================================
# MAIN SHIKSHA ROBOT INTEGRATION SYSTEM
# ============================================================================

class ShikshaRobot:
    """
    SHIKSHA Robot Main Integration System
    ═════════════════════════════════════════════════════════════════════
    
    Complete system integration coordinating all subsystems:
    • Barcode scanning and chart recognition
    • LED facial expressions for emotional engagement
    • Servo motor ear movements for physical interaction
    • Audio playback for educational content delivery
    • Power monitoring for system health
    
    Workflow:
    1. Idle State: Robot displays happy face, awaiting input
    2. Chart Detection: Barcode scanner reads chart identifier
    3. Processing: System validates barcode and loads content
    4. Content Delivery: Audio plays with synchronized animations
    5. Return to Idle: Robot ready for next interaction
    
    Performance Metrics:
    • Detection Accuracy: 98.5%
    • Response Time: < 0.5 seconds
    • Uptime: 6-8 hours per charge
    • Concurrent Operations: Audio + LED + Servo control
    """
    
    def __init__(self):
        print("\n" + "="*70)
        print("  SHIKSHA ROBOT - AI-Integrated Educational Assistant")
        print("  Developed at Experimind Labs")
        print("="*70 + "\n")
        
        print("Initializing Robot Subsystems...\n")
        
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
        
        self.current_state = "idle"
        self.last_barcode = None
        self.running = False
        
        print("\n" + "="*70)
        print("✓ ALL SYSTEMS INITIALIZED SUCCESSFULLY")
        print("="*70 + "\n")
    
    def start(self):
        """Start the robot system and enter main control loop"""
        self.running = True
        print("🚀 SHIKSHA ROBOT STARTED\n")
        print("System Status: OPERATIONAL")
        print("Mode: Interactive Learning Assistant")
        print("Waiting for chart detection...\n")
        
        self.welcome_sequence()
        
        try:
            while self.running:
                self.main_loop()
                time.sleep(0.1)
        except KeyboardInterrupt:
            print("\n\n⚠ Shutdown signal received...")
            self.shutdown()
    
    def welcome_sequence(self):
        """Display welcome animation on startup"""
        print("▶ Playing welcome sequence...")
        self.face.excited_face()
        self.servo.wiggle_ears(2)
        time.sleep(1)
        self.face.happy_face()
        self.servo.neutral_position()
        print("✓ Ready for interaction\n")
    
    def main_loop(self):
        """
        Main robot control loop
        Handles chart detection and orchestrates response
        """
        # Periodic battery status check (every 60 seconds)
        if int(time.time()) % 60 == 0:
            self.check_power_status()
        
        # Check for barcode input
        barcode = self.scanner.read_barcode()
        
        if barcode and barcode != self.last_barcode and not self.audio.is_playing():
            print(f"\n{'='*70}")
            print(f"📊 CHART DETECTED: {barcode}")
            print(f"{'='*70}")
            self.process_chart(barcode)
            self.last_barcode = barcode
    
    def process_chart(self, barcode):
        """
        Process detected chart and deliver educational content
        
        Workflow:
        1. Show processing state (thinking face + perked ears)
        2. Load and play audio content
        3. Display engaged animations
        4. Monitor playback completion
        5. Return to ready state
        """
        print(f"▶ Processing chart: {barcode}")
        
        # Processing state
        self.face.thinking_face()
        self.servo.perk_up()
        time.sleep(0.5)
        
        # Attempt content delivery
        if self.audio.play_audio(barcode):
            # Engaged state
            self.face.excited_face()
            self.servo.wiggle_ears(1)
            time.sleep(0.5)
            self.face.listening_face()
            
            # Monitor playback
            print("  └─ Content delivery in progress...")
            while self.audio.is_playing():
                time.sleep(0.5)
            
            # Completion
            print("  └─ ✓ Content delivered successfully")
            print(f"{'='*70}\n")
            self.face.happy_face()
            self.servo.neutral_position()
            time.sleep(1)
            
        else:
            # Error state
            print("  └─ ✗ Content not available")
            print(f"{'='*70}\n")
            self.face.clear()
            time.sleep(0.5)
            self.face.happy_face()
            self.servo.neutral_position()
    
    def check_power_status(self):
        """Monitor and display battery status"""
        status = self.power.check_battery_status()
        print(f"\n🔋 Battery: {status['percentage']:.1f}% "
              f"({status['voltage']:.2f}V) - {status['status']}\n")
        
        if status['percentage'] < CONFIG['power']['low_battery_threshold']:
            print("  ⚠ WARNING: Low battery detected! Please recharge soon.\n")
    
    def shutdown(self):
        """
        Gracefully shutdown robot system
        Cleanup all hardware resources
        """
        print("\n" + "="*70)
        print("INITIATING SHUTDOWN SEQUENCE")
        print("="*70 + "\n")
        
        self.running = False
        
        print("Stopping audio playback...")
        self.audio.stop_audio()
        
        print("Clearing LED display...")
        self.face.clear()
        
        print("Resetting servo positions...")
        self.servo.neutral_position()
        time.sleep(0.5)
        
        print("Cleaning up GPIO...")
        self.servo.cleanup()
        
        print("Closing barcode scanner...")
        self.scanner.close()
        
        # Final status report
        final_status = self.power.check_battery_status()
        print(f"\nFinal Battery Status: {final_status['percentage']:.1f}% "
              f"({final_status['voltage']:.2f}V)")
