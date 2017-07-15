Pegasus supports calling external scripts and executables on certain program events.

### 1. The scripts directory

First, create a new directory called `scripts` inside the config directory:

- Linux: `~/.config/pegasus-frontend` or `/etc/xdg/pegasus-frontend`
- Windows: `C:\Users\<User Name>\AppData\Roaming\pegasus-frontend`

### 2. Event directories

Inside the `scripts` folder, create a new directory for the kind of event you want to script:

Name | When
:--- | ----
`quit` | on program quit
`reboot` | on system reboot (also calls `quit` first)
`shutdown` | on system shutdown (also calls `quit` first)
`config` | on the change of any configuration option
`controls` | on change of the control settings (also calls `config` first)
`settings` | on change of the regular (non-control) settings (also calls `config` first)

### 3. Script calling

Put your executable scripts or binaries into these new directories. They will be called in **alphabetic order** when the event happens.
