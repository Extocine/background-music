A Python script that plays continuous background music and automatically pauses/fades out the music whenever other audio is detected on the system (e.g., watching a video, playing a game). It will resume/fade in the background music once system silence is detected again.

# ✨ Features
Smooth Fading: Can smoothly fade the music volume in and out.

Configurable: Easily adjust the music folder, volume, and fade speed.

Looping & Shuffling: Plays a shuffled, infinite loop of music from a specified directory.

Resume Delay: Configurable delay to prevent the music from immediately resuming after a very short silence.

# 🚀 Getting Started
This script is designed for Linux systems using PulseAudio or PipeWire (which often uses a PulseAudio compatibility layer) for audio management.

Python 3:

```Bash
python3 --version
```
mpv Media Player: Used for music playback and volume control via its Inter-Process Communication (IPC) socket.

```Bash
# Debian/Ubuntu
sudo apt install mpv
# Fedora
sudo dnf install mpv
# Arch
sudo pacman -S mpv
```
pactl: A utility for controlling the PulseAudio sound server, used here to detect active audio streams. This is usually part of the pulseaudio-utils or base installation.

```Bash
# Debian/Ubuntu
sudo apt install pulseaudio-utils
```

# Installation and Usage
Download `background-music` to your system or run `git clone https://github.com/Extocine/background-music`

Configure Music Folder: Edit the `background-music` file and change the MUSIC_FOLDER variable to the absolute path of your music collection.

```Python
# === CONFIGURATION ===
MUSIC_FOLDER = os.path.expanduser("/DIR/TO/MUSIC") # <--- CHANGE THIS
# ...
```
Run the script:

```Bash
python3 background-music
```
Stop: Press Ctrl+C to stop the program

# ⚙️ Configuration
You can customize the script by changing the variables under the CONFIGURATION section in `background-music`:

|Variable|Default Value|Description|
|-|-|-|
|MUSIC_FOLDER|/DIR/TO/MUSIC|	The directory containing your music files.|
|BASE_VOLUME|	70	|The volume (0-100) for the background music.|
|RESUME_DELAY|	0	|Seconds to wait after silence is detected before resuming music.|
|FADE_INTERVAL	|0.05	|Seconds between each fade step (lower = faster fade).|

# 🐞 Known Bugs & Limitations
Linux-Only: The script relies on the pactl command, which is specific to Linux systems using PulseAudio/PipeWire for detecting active audio clients. It will not work on Windows or macOS without significant modification.

mpv IPC Errors: If mpv is manually closed or crashes while the daemon is running, the script may temporarily log mpv IPC error until it attempts to restart mpv (though the current script does not explicitly handle restarting the mpv process if it dies after initial launch).

False Positives/Negatives: The list of active audio clients from pactl can sometimes include applications that are not actively playing sound or might miss very niche sound sources, leading to occasional false pauses or missed resumptions.

Unwanted Delays: Certain apps like Google Chrome will internally say its playing audio for a short while even though no sound is being played. You can check this in your volume settings in your OS or using `pavucontrol`

My crappy coding skills: I'm hardly a programmer and am not the best with this kinda stuff ^^
