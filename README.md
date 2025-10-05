# 🤖 SHIKSHA Robot

<p align="center">
  <img src="images/overview.jpg" alt="SHIKSHA Robot Overview" width="85%">
  <br>
  <em>Figure 1: SHIKSHA Robot Overview</em>
</p>

An interactive **AI-driven educational robot** designed to make classroom learning more engaging and accessible.  
**SHIKSHA** combines hardware systems, AI modules, and real-time interactivity to assist teachers and enhance student participation.

---

## 🧠 Overview

**SHIKSHA Robot** is an **education-focused humanoid system** built to:
- Deliver interactive lessons and explanations  
- Conduct real-time quizzes and feedback sessions  
- Recognize and respond to educational charts  
- Provide responsive audio-visual communication  

The project integrates **embedded systems**, **AI control**, and **human-robot interaction** to promote hands-on learning in classrooms.

---

## ⚙️ System Architecture

<p align="center">
  <img src="images/working.jpg" alt="System Architecture" width="85%">
  <br>
  <em>Figure 2: System Architecture of SHIKSHA Robot</em>
</p>

### 🧩 AI Version
- **Main Controller:** Raspberry Pi 5  
- **Connectivity:** Jio-Fi for wireless cloud access  
- **Logic Interface:** Level shifter (3.3V ↔ 5V)  
- **USB Expansion:** Multi-port hub for peripherals  

### ⚡ Chart Version
- **Microcontroller:** Arduino Nano  
- **Power Regulation:** Buck converter (5V constant output)  
- **Audio System:** DFPlayer Mini + Amplifier + Speaker  
- **Animations:** NeoPixel LEDs & MG90S Servo motors (eyes, mouth, ears)  

---

## 🧮 Chart Mode

<p align="center">
  <img src="images/chartmode.jpg" alt="Chart Mode Working" width="85%">
  <br>
  <em>Figure 3: Chart Mode and Low-Cost Chart Identification</em>
</p>

A **low-cost chart identification system** was developed using the **TCS34725 color sensor**, replacing expensive barcode scanning.  
- Uses **five color spots** across **five pattern positions**  
- Generates **625 unique combinations**  
- Enables affordable and accurate classroom activity recognition  

---

## 🧱 Challenges

- Integrating AI control with embedded hardware  
- Designing and debugging custom circuits  
- Achieving reliable chart detection under varying conditions  
- Synchronizing servos and LEDs with real-time audio output  

---

## ✅ Conclusion

**SHIKSHA** demonstrates how **AI and robotics** can reshape education by blending technology with teaching.  
The system successfully delivers an **interactive, scalable, and cost-effective** platform for classrooms — turning traditional learning into an engaging, hands-on experience.

---

<p align="center">
  <em>Designed and Developed with passion for Smart Education 💡</em>
</p>
