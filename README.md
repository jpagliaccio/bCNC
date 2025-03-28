bCNC Forked
====

---

Forked travis-ci.com/vlachoudis

# For drawing machines 
- Simplify
- Adjusted slider settings 
- Added sound 
- Clear z at Stop 
- Output position to stdout
- Revised status bar message  

---


GrblHAL (formerly GRBL) CNC command sender, autoleveler, g-code editor, digitizer, CAM
and swiss army knife for all your CNC needs.

An advanced fully featured g-code sender for grblHAL (formerly GRBL). bCNC is a cross platform program (Windows, Linux, Mac) written in python. The sender is robust and fast able to work nicely with old or slow hardware like [Raspberry Pi](http://www.openbuilds.com/threads/bcnc-and-the-raspberry-pi.3038/) (As it was validated by the GRBL maintainer on heavy testing).

# Installation (using pip = recommended!)

This is a short overview of the installation process, for more details see the ![bCNC installation](https://github.com/vlachoudis/bCNC/wiki/Installation) wiki page.

This is how you install (or upgrade) bCNC along with all required packages.
You can use any of these commands (you need only one):

    pip install --upgrade bCNC
    pip install --upgrade git+https://github.com/vlachoudis/bCNC
    pip install . #in git directory
    python -m pip install --upgrade bCNC

This is how you launch bCNC:

    python -m bCNC

Only problem with this approach is that it might not install Tkinter in some cases.
So please keep that in mind and make sure it's installed in case of problems.

If you run the `python -m bCNC` command in root directory of this git repository it will launch the git version.
Every developer should always use this to launch bCNC to ensure that his/her code will work after packaging.

Note that on Windows XP you have to use `pyserial==3.0.1` or older as newer version do not work on XP.

PyPI project: https://pypi.org/project/bCNC/

# Installation (manual)
You will need the following packages to run bCNC
- tkinter the graphical toolkit for python
  Depending your python/OS it can either be already installed,
  or under the names tkinter, python3-tkinter, python-tk
- pyserial or under the name python-serial, python-pyserial
- numpy
- Optionally:
- python-imaging-tk: the PIL libraries for autolevel height map
- python-opencv: for webcam streaming on web pendant
- scipy: for 100 times faster 3D mesh slicing

Expand the directory or download it from github
and run the bCNC command

# Installation (Linux package maintainers)
- Copy `bCNC` subdirectory of this repo to `/usr/lib/python3.x/site-packages/`
- Launch using `python -m bCNC` or install bCNC.sh to /usr/bin
- Alternatively you can fetch the bCNC Python package using pip when building Linux package
  - refer to your distro, eg.: https://wiki.archlinux.org/index.php/Python_package_guidelines
  - Py2deb to build Debian package from Python package: https://pypi.org/project/py2deb/


# IMPORTANT! Motion controller (grblHAL) settings
- We strongly recommend you to use 32b microcontroller with grblHAL firmware for the new machine builds. https://github.com/grblHAL (Original GRBL firmware is still supported, but it is currently reaching the end-of-life due to limitations of 8b microcontrollers)
- GRBL should be configured to use **MPos** rather than **Wpos**. This means that `$10=` should be set to odd number. As of GRBL 1.1 we recommend setting `$10=3`. If you have troubles communicating with your machine, you can try to set failsafe value `$10=1`.

- CADs, bCNC and GRBL all work in millimeters by default. Make sure that `$13=0` is set in GRBL, if you experience strange behavior. (unless you've configured your CAD and bCNC to use inches)


# Configuration
You can modify most of the parameters from the "CAM -> Config/Controller" page.

$100=250 Steps/mm  
$101=250
$102=250

$110=3000 Max Rate, eg Rapid  
$111=3000
$112=3000

$120=50.000 Accelaration, greater is faster 
$121=50.000
$122=50.000

You can also enable (up to) 6-axis mode in Config section,
but bCNC restart is required for changes to take place.
Only the changes/differences from the default configuration
file will be saved in your home directory ${HOME}/.bCNC  or ~/.bCNC

The default configuration is stored on bCNC.ini in the
installation directory.

*PLEASE DO NOT CHANGE THIS FILE, IT'S GOING TO BE OVERWRITTEN ON EACH UPGRADE OF BCNC*

# Features:
- simple and intuitive interface for small screens
- 3-axis and 6-axis GUI modes
- import/export **g-code**, **dxf** and **svg** files
- 3D mesh slicing **stl** and **ply** files
- fast g-code sender (works nicely on RPi and old hardware)
- workspace configuration (G54..G59 commands)
- user configurable buttons
- g-code **function evaluation** with run time expansion
- feed override during the running for fine tuning
- Easy probing:
  - simple probing
  - center finder with a probing ring
  - **auto leveling**, Z-probing and auto leveling by altering the g-code during
    sending (or permanently autoleveling the g-code file).
  - height color map display
  - create g-code by jogging and recording points (can even use camera for this)
  - **manual tool change** expansion and automatic tool length probing
  - **canned cycles** expansion
- Various Tools:
  - user configurable database of materials, endmills, stock
  - properties database of materials, stock, end mills etc..
  - basic **CAM** features (profiling, pocketing, drilling, flat/helical/ramp cutting, thread milling, cutout tabs, drag knife)
  - User g-code plugins:
    - bowl generator
    - finger joint box generator
    - simple spur gear generator
    - spirograph generator
    - surface flatten
    - play melody from MIDI file using stepper motor frequency
    - ...
- G-Code editor and display
    - graphical display of the g-code, and workspace
    - graphically moving and editing g-code
    - reordering code and **rapid motion optimization**
    - moving, rotating, mirroring the g-code
- Web pendant to be used via smart phones

# Debugging
You can log serial communication by changing the port to something like:

    spy:///dev/ttyUSB0?file=serial_log.txt&raw
    spy://COM1?file=serial_log.txt&raw

If a file isn't specified, the log is written to stderr.
The 'raw' option outputs the data directly, instead of creating a hex dump.
Further documentation is available at: https://pyserial.readthedocs.io/en/latest/url_handlers.html#spy

# Disclaimer
  The software is made available "AS IS". It seems quite stable, but it is in
  an early stage of development.  Hence there should be plenty of bugs not yet
  spotted. Please use/try it with care, I don't want to be liable if it causes
  any damage :)

# See also
  - G-code simulators that you can use to independently cross-check g-code generated by bCNC or verify any g-code files in case you have troubles running them.
    - https://harvie.github.io/cnc-simulator ([github](https://github.com/Harvie/cnc-simulator))
    - https://camotics.org
    - https://freecad.org
