
<h2>Usage</h2>

sshmux makes your ssh sessions more robust by hosting server sessions in tmux and adding client side reconnect logic.
The simplest usage (which requires tmux on the server) is:

    $ sshmux me@myserver

Once the connection is established, it is persistent. You can turn close your laptop and put it to sleep, restart your wifi connection,
or put your laptop in your backpack and go home for the day. When you open it back up, the connection will be automatically reestablished.
Sshmux is a simple bash wrapper around ssh. It is platform independent, works with all other ssh command line arguments, and requires no configuration.

<h2>Installation</h2>

    $ wget https://raw.githubusercontent.com/Russell91/sshmux/master/sshmux && 
    chmod +x sshmux && 
    sudo mv sshmux /usr/local/bin #or anywhere else on your PATH
    
<h2>Details</h2>

<h3>Named Sessions</h3>

You do not need to know tmux to use sshmux and only want the persistent server feature. But if you do know tmux, 
you'll immediately notice
that sshmux creates a tmux session with the name "default" by default. If you want to create a second tmux session with the name
"session2", you can use the `-t` flag as in `tmux attach -t session2`:

    $ sshmux me@myserver -t session2
    
This will create a new session if no session beginning with the letters "session2" exists, and join an existing session otherwise.
The original `-t` flag of ssh is not supported when using sshmux (sshmux already uses this flag internally).

<h3>Debugging</h3>

If sshmux isn't connecting well, you can pass it the `-v` flag for more verbose output, as you would do with ssh.
If you want to kill the sshmux process locally without disturbing a script running on the server, try either closing your
local terminal emulator or passing a SIGTSTP with ctrl-Z. These are safer than killing sshmux with ctrl-C, as they will not risk
killing your remote script.

<h3>Comparison to other tools</h3>

sshmux is related to <a href="http://www.harding.motd.ca/autossh/">autossh</a> and <a href="https://mosh.mit.edu/">mosh</a>. Like sshmux,
autossh will automatically attempt to reconnect the client when wifi is restarted. However, unlike sshmux, autossh does not provide server
side persistence by default.

Mosh is another tool supporting persistent ssh sessions, having additional features including immediate
local rendering of keyboard inputs and UDP connections for improved performance. However, the UDP feature requires the user
to reconfigure the server's firewall prior to using mosh. This requirement is in many cases not satisfiable in commercial environments.

Unlike both autossh and mosh, sshmux has no binary distribution and is instead bash wrapper, exposing exactly the same flags and 
features as the traditional ssh tool.
