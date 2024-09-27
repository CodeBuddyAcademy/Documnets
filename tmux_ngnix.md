# Tmux Guide
```tmux``` is a terminal multiplexer that allows you to create multiple terminal sessions, keep them running in the background, and reattach to them later. This guide will help you get started with tmux, run scripts, and manage sessions efficiently.

# 1. Install tmux
If ```tmux``` is not already installed on your server, you can install it using your package manager.
For Ubuntu/Debian:
```bash
$ sudo apt-get install tmux
```

# 2. Start a New tmux Session
To start a new ```tmux``` session, use the following command:
```bash
$ tmux new -s mysession
```

Replace ```mysession``` with a name you want for your session.

# 3. Running a Command
Once you're in the ```tmux``` session, you can run your Python script or any other command:
```bash 
$ python your_script.py
```

# 4. Detaching from the Session
To detach from the session and leave it running in the background, press:
```bash
$ Ctrl + B, then D
```
This will take you back to your normal terminal.


# 5. Reattaching to the Session
To reattach to your ```tmux``` session later, use the command:
```bash
$ tmux attach -t mysession
```

# 6. Listing Sessions
If you have multiple ```tmux``` sessions and want to see a list, you can run:
```bash 
$ tmux ls
```

# 7. Killing a Session
To kill a tmux session when you’re done, reattach to it and then type:
```bash
$ exit
```
# 8. Kill it from another terminal
Alternatively, you can kill it from another terminal by using:
```bash
$ tmux kill-session -t mysession
```

# 9. Basic tmux Commands
Here are some helpful basic commands for working with ```tmux```:
- Split Window Horizontally: Ctrl + B, then %
- Split Window Vertically: Ctrl + B, then "
- Switch Between Panes: Ctrl + B, then use arrow keys
- Resize Pane: Hold Ctrl + B, then hold Ctrl and use arrow keys
- Close Pane: Type exit in the pane or press Ctrl + D
