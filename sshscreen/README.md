You have discovered sshscreen. 

sshscreen works identically to sshmux, except that it is built on top of screen rather than tmux:

    sshscreen me@myserver -t sessionname

<h3>Installation</h3>

    $ wget https://raw.githubusercontent.com/Russell91/sshmux/master/sshscreen/sshscreen && 
    chmod +x sshscreen && 
    sudo mv sshscreen /usr/local/bin #or anywhere else on your PATH
