# SDP

## Convert png to ico

```
from PIL import Image
filename = r'logo.png'
img = Image.open(filename)
img.save('logo.ico')
```

## Convert icon to python

1. Navigate to the WX tool directory, on my installation that's C:
   \Python24\Lib\site-packages\wx-2.8-msw-unicode\wx\tools

2. Run "img2py.py -i pycon.ico iconfile.py"

3. Copy the iconfile.py to your project's directory

4. Put these lines in your app:

```
import iconfile
myicon = iconfile.GetIcon()
self.SetIcon(myicon)
```

## Using UPX with PyInstaller

### Prerequisites

- Python installed on your system.
- PyInstaller installed (`pip install pyinstaller`).
- UPX installed and accessible in your system's PATH. Download UPX from [https://upx.github.io/](https://upx.github.io/).

### Installation

#### Install UPX

1. **Windows**: Download UPX from the official website, unzip it, and add the UPX folder to your system's PATH.
2. **Linux/Mac**: Use a package manager to install UPX. For example, on Debian-based systems, use `sudo apt-get install upx-ucl`. On macOS, use `brew install upx`.

#### Verify Installation

Open a terminal or command prompt and type `upx --version` to verify that UPX is correctly installed and accessible from the command line.

### Using UPX with PyInstaller

#### Basic Usage

To use UPX to compress your PyInstaller-generated executable, simply run PyInstaller with your script as usual. If UPX is in your PATH, PyInstaller automatically uses it to compress the executable binaries.

## Compile an exe

```
pyinstaller -F --icon="gui//icons//sdp_icon.ico" --clean SDP.pyw
```

## Convert exe to setup exe for distribution

The exe is prepared for distribution using [Inno Setup](https://jrsoftware.org/isinfo.php)

A good guide for using Inno Setup is provided [here](https://www.blog.pythonlibrary.org/2019/03/19/distributing-a-wxpython-application/)

## Setting up a virtual environment

Good step by step guides are found at the links below:
https://towardsdatascience.com/virtual-environments-for-absolute-beginners-what-is-it-and-how-to-create-one-examples-a48da8982d4b
https://towardsdatascience.com/virtual-environments-104c62d48c54

In short, if you are not using a virtual environment for your project, then all packages that you have imported for python are being used for all projects, this creates several issues and conflicts, especially when projects are shared between multiple engineers or you are working on multiple projects at once. In the context of making exes, it results in all your packages being bundled into a massive exe with slow load times.

1. It is best practice to create a virtual environment for each python project you are working on. First, I found it useful to create a list of all packages in your global python environment. In CMD window with project root as your current working directory save a list of all your python packages to a file in your current directory. These are all the packages that would have been compiled into an exe without switching to a virtual environment approach.

pip freeze > globalpythonpackages.txt

(If you get:'pip' is not recognized as an internal or external command, operable program or batch file, then add "python -m " before all pip commands.

2. Next create a virtual environment (make sure you add venv/ to your .gitignore file if you are using git)

python -m venv venv

3. Now activate your environment:

venv\scripts\activate

3. You can see your python packages in the virtual environment at any time by typing:

pip list

4. Create a requirements file for the project (will be emptyish at first but we will import packages until the project is working:

pip freeze > requirements.txt

5. Suggest hand picking (copy/pasting) packages you know you need from "globalpythonpackages.txt" and adding them to the requirements.txt file. (Its OK if you miss some/most)

6. Install all packages from the updated requirements file:

pip install -r requirements.txt

7. Try running your program, if you get an error, you are still missing packages. copy/paste missing packages from "globalpythonpackages.txt" and adding them to the "requirements.txt" file

Repeat steps 6 and 7 until your program runs without error. Congratulations, you've made it.

8. Record the python version you are using and the complete project requirements:

python --version > pythonversion.txt
pip freeze > requirements.txt

It is recommended to keep the requirements.txt and pythonversion.txt files in your project root directory (these can be used by other engineers who get your project through git).

## Using the virtual environment

1. Activate your virtual environment:

venv\scripts\activate

2. Deactivate when you are done

deactivate
