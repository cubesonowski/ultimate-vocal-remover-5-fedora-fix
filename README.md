# Tested on Fedora 44 (but likely works in any other distro)
## This repository does not contain the Ultimate Vocal Remove GUI. It only provides a custom requirements.txt and guide to make it work on Fedora 44/Linux with GPU acceleration.
## Download the original source code from: [Anjok07/ultimatevocalremovergui](https://github.com/Anjok07/ultimatevocalremovergui/releases)

## 0. Python installation
```bash
sudo dnf install python3.10 python3.10-devel
```

## 1. Environment
```bash
python3.10 -m venv venv
source venv/bin/activate
pip install --upgrade pip setuptools wheel
```

## 2. Torch (GPU acceleration)
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

## 3. Other necessary libraries
```bash
pip install -r requirements.txt
pip install onnxruntime-gpu
```

## FOR FEDORA USERS
```bash
execstack -c ./venv/lib64/python3.10/site-packages/onnxruntime/capi/onnxruntime_pybind11_state.cpython-310-x86_64-linux-gnu.so
```

## 4. In UVR.py do the following things
1. Uncomment 48, 1536, 1537, 1541, 1542 lines
```python
from playsound import playsound
if chosen_font_file:
    pfont.add_file(chosen_font_file)
pfont.add_file(FONT_MAPPER[MAIN_FONT_NAME])
pfont.add_file(FONT_MAPPER[SEC_FONT_NAME])
```
2. In 1313 line in `img.open_image()` in `size=()` change first argument for any number e.g. 800

## 5. Script to run the program
```bash
cd /home/$USER/ultimatevocalremovergui-5.6
source venv/bin/activate
python UVR.py
```

## 6. You can also create a .desktop file that runs this script and put it in '~/.local/share/applications/'.
```bash
[Desktop Entry]
Type=Application
Categories=AudioVideo;Audio;
Comment=
Exec=/home/$USER/ultimatevocalremovergui-5.6/run_uvr.sh
Icon=/home/$USER/ultimatevocalremovergui-5.6/gui_data/img/GUI-Icon.png
Name=Ultimate Vocal Remover
Terminal=false
```

