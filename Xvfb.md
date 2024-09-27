# Xvfb (X Virtual Framebuffer) Guide
**Xvfb** (X Virtual Framebuffer) is a display server that performs graphical operations in memory without the need for a physical display. It is commonly used to run graphical applications in headless environments such as servers.

## 1. Install Xvfb
If ```Xvfb``` is not already installed on your system, install it using the package manager for your distribution.

For **Ubuntu/Debian**:
```bash
$ sudo apt-get install xvfb
```

For **CentOS/RHEL**:
```bash
$ sudo yum install Xvfb
```

## 2. Start Xvfb
To start ```Xvfb```, specify the display number and resolution:
```bash
$ Xvfb :99 -screen 0 1024x768x16 &
```
Explanation:
- ```:99``` specifies the display number. You can replace ```99``` with any number not in use.
- ```-screen 0 1024x768x16``` defines the screen resolution (1024x768) and color depth (16-bit).
- The ```&``` at the end runs ```Xvfb``` in the background.

### 3. Set the Display Environment Variable
After starting ```Xvfb```, you need to set the ```DISPLAY``` environment variable to the display number you used (```:99``` in this case):
```bash
$ export DISPLAY=:99
```
Now, any graphical applications you run will use ```Xvfb``` to render in memory instead of a physical display.

## 4. Running Applications with Xvfb
You can now run graphical applications in the background. For example, to run a Python script that uses ```Tkinter``` or other graphical interfaces:
```bash
$ python your_script.py
```

## 5. Killing the Xvfb Session
To stop the ```Xvfb``` server, find the process ID (PID) using the ```ps``` command, then kill it.
List the running ```Xvfb``` processes:
```bash
$ ps aux | grep Xvfb
```

### Kill the process:
```bash
$ kill <PID>
```

### Alternatively, if you started ```Xvfb``` in the background with ```&```, you can use the ```kill``` command directly with the job number:
```bash
$ kill %1  # Use %1 or the job number shown in the background process list
```

## 6. Common Issues
**Display already in use**: If you see an error like ```Fatal server error: (EE) Cannot establish any listening sockets```, this means the display number is already in use. Try using a different display number (```:100```, ```:101```, etc.).

**Lock file issues**: If you encounter an error related to ```.X99-lock``` file, try removing the lock file:

```bash
$ rm /tmp/.X99-lock
```

## 7. Running Xvfb with a Command in One Line
You can start ```Xvfb```, run a command, and stop ```Xvfb``` in one line by using ```xvfb-run```. This is useful for running short-lived commands without manually managing ```Xvfb```:

```bash
$ xvfb-run python your_script.py
```
This command will automatically start ```Xvfb```, run the script, and clean up once the script finishes.


## Example Use Case: Running Selenium with Xvfb
If you're using Selenium and need to run browser tests in a headless environment, you can use ```Xvfb``` as follows:

```bash
$ Xvfb :99 -screen 0 1920x1080x24 &
$ export DISPLAY=:99
$ python selenium_test_script.py
```

This guide covers the essentials of setting up and using **Xvfb**. You can now run graphical applications on a headless server without the need for a physical display!