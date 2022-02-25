Virtual Env
========================
# ls envname z.B monigomani ###### wichtig 
## apt install python3-pip
Create virtual environment for python 3
Venv command is used in Python to create virtual environment. The venv package is available in Ubuntu repository.

Lets first install venv package using the following command:

### $ apt-get install python3-venv
Now, to create a virtual environment, type:

### $ python3 -m venv my_env_project
The above command creates a directory named 'my_env_project' in the current directory, which contains pip, interpreter, scripts, and libraries.

oltjano@ubuntu:~$ ls my_env_project/
 bin  include  lib  lib64  pyvenv.cfg  share
You can now activate the virtual environment, type:

### $ source my_env_project/bin/activate
Command prompt would change to your environment and will look as shown:

(my_env_project) oltjano@ubuntu:~$
Verify Virtual Environment
Run python command inside virtual environment to open the interpreter:

(my_env_project) oltjano@ubuntu:~$ python
Output
Python 3.8.5 (default, Jul 28 2020, 12:59:40)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
To install a package inside the virtual environment, for example I am installing NumPy package:

(my_env_project) oltjano@ubuntu:~$ pip install numpy --user
If you are getting below error

"ERROR: Can not perform a '--user' install. User site-packages are not visible in this virtualenv."

Set include-system-site-packages to true in pyvenv.cfg file.

Every time you install a new package inside your virtual environment, you should be able to import it into your project.

(my_env_project) oltjano@ubuntu:~/my_env_project$ python
>>> import numpy
Lets test a math function, type:

>>> import math
>>> print(math.sqrt(16))
To exit from interpreter, type:

>>> quit()