# Microbit Customization Guide

Welcome to the Microbit repository! This guide will show you how to safely customize your BBC micro:bit, a small programmable computer designed for education and fun.

## What is a micro:bit?

The micro:bit is a pocket-sized computer that you can program to do all sorts of things, from displaying messages to controlling robots. It's completely safe to use and experiment with at home.

## How to Customize Your micro:bit

### Option 1: Using MakeCode (Beginner-Friendly)

1. **Go to the MakeCode website**: Visit [makecode.microbit.org](https://makecode.microbit.org) in your web browser.

2. **Create a project**: Click on "New Project" and start coding using blocks or JavaScript.

3. **Add your custom code**: Use the block editor to drag and drop blocks, or switch to JavaScript for text-based coding. For example, make the LEDs display a smiley face or respond to button presses.

4. **Download the program**: Click the download button to get a .hex file.

5. **Flash to your micro:bit**: Connect your micro:bit to your computer via USB. Drag the .hex file onto the MICROBIT drive that appears.

### Option 2: Using Python

1. **Use the Python Editor**: Go to [python.microbit.org](https://python.microbit.org) or use Mu Editor.

2. **Write Python code**: For example:
   ```python
   from microbit import *

   while True:
       display.show(Image.HEART)
       sleep(1000)
       display.clear()
       sleep(1000)
   ```

3. **Flash the code**: Click "Flash" or "Download" and transfer the file to your micro:bit as above.

### Option 3: Custom Serial Control Script

![MakeCode JavaScript Editor](/Images/makecode-screenshot.png)

This advanced script allows you to control the micro:bit's LED display remotely via serial communication and receive input events from the micro:bit.

1. **Open MakeCode**: Visit [makecode.microbit.org](https://makecode.microbit.org).

2. **Create a new project**: Click "New Project".

3. **Switch to JavaScript**: Click the "{} JavaScript" button to switch from blocks to text editor.

4. **Paste the script**: Replace the default code with the following:

   ```javascript
   serial.onDataReceived("!", () => {
       let c = serial.readUntil("!")
       let x = parseInt(c.charAt(0))
       let y = parseInt(c.charAt(1))
       let s = parseInt(c.charAt(2))
       if (s == 1) led.plot(x, y)
       else led.unplot(x, y)
   })
   input.onButtonPressed(Button.A, () => serial.writeLine("EVT:BUTTON_A"))
   input.onButtonPressed(Button.B, () => serial.writeLine("EVT:BUTTON_B"))
   input.onButtonPressed(Button.AB, () => serial.writeLine("EVT:BUTTON_AB"))
   input.onLogoEvent(TouchButtonEvent.Touched, () => serial.writeLine("EVT:LOGO"))
   input.onGesture(Gesture.Shake, () => serial.writeLine("EVT:SHAKE"))
   ```

5. **Download and flash**: Download the .hex file and drag it to your micro:bit as in Option 1.

   ![Flashing micro:bit](/Images/microbit-flashing.png)

   2.) Download and flash it - drag your hex file to the micro:bit

This script listens for serial data in the format "!xys!" (where x and y are LED coordinates 0-4, s is 1 to turn on or 0 to turn off) and sends events like "EVT:BUTTON_A" when buttons are pressed.

### Step 3: Connect via Browser Interface

3.) Use a modern browser and run the `microbitcustom.html` file. When you open it, press the **Connect** button to open a browser prompt for selecting the serial port, then click **Connect**.

   ![Browser Serial Prompt](/Images/microbit-browserprompt.png)

### Safety Tips

- Your micro:bit won't break from programming – it's designed for experimentation!
- Always use the official tools to avoid any issues.
- If something doesn't work, try resetting by holding the reset button on the back.
- If you feel like your micro:bit is broken, just drag another hex file with a project on it – that's it! Your micro:bit will be restored.

## Resources

- Official micro:bit website: [microbit.org](https://microbit.org)
- MakeCode tutorials: [makecode.microbit.org/tutorials](https://makecode.microbit.org/tutorials)
- Python documentation: [microbit-micropython.readthedocs.io](https://microbit-micropython.readthedocs.io)

Have fun customizing your micro:bit!
