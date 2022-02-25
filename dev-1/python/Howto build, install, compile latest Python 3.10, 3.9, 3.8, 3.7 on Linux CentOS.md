Howto build, install, compile latest Python 3.10, 3.9, 3.8, 3.7 on Linux CentOS
========================================



[https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/)**




[Skip to content](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#content) 




[
Python, Django tips and code snippets.
](https://www.workaround.cz/)




Some useful Python, Django code snippets from my practice.










[
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#)



Menu 


- [I am Python and Django developer. Hire me.](https://www.workaround.cz/python-django-developer-hire-me/)

- [















# Howto build, compile and install latest Python 3.10, 3.9, 3.8, 3.7 on Linux CentOS 7, 8

22/11/202120/11/2019 by Hanz](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#) 





Do you want to install latest [Python](https://www.python.org/) 3.10.0 (resp. 3.9.9, 3.8.12 or 3.7.11) on Linux [CentOS](https://www.centos.org/) 7 or 8 and don’t want to break up the shipped Python?

You are in the right place.  

I have for you a short tutorial on **how to build, compile and install Python 3.10, 3.9, 3.8 or 3.7 on Linux CentOS 7 or 8 **and run it  without destroying the shipped Python in Centos.

**HINT** – At the end of the article you find [the cheatsheet](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#cheatsheet), a set of Bash commands that you can COPY & PASTE  and run in your Linux command line.

 

**What we are going to solve**


- update your CentOS box and install needed developer libraries and tools

- download and unpack latest Python source code

- compile Python source code

- install Python source code and do some post-install stuff for easy using in Bash command line

- check of created Python binaries

- create and test the Python virtual environment



At the time of writing this post Python 3.10.0 (resp. 3.9.9, 3.8.12 or 3.7.11) is the most current stable version of the language and the most used version CentOS is 7, the newest one is version 8. CentOS 7 is shipped with Python 2.7.5 and CentOS 8 is shipped with Python 3.6.8.


Table of contents** 
[hide](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#)



[
Prerequisites
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#Prerequisites)
[
Step 1 – prepare CentOS for Python compilation
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#Step_1_prepare_CentOS_for_Python_compilation)
[
Step 2 – download and unpack Python source code
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#Step_2_download_and_unpack_Python_source_code)
[
Step 3 – compile Python source code into binaries
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#Step_3_compile_Python_source_code_into_binaries)
[
Step 4 – make post-install stuff
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#Step_4_make_post-install_stuff)
[
Step 5 – checking Python binaries
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#Step_5_checking_Python_binaries)
[
Step 6 – setting up the Python virtual environment (venv)
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#Step_6_setting_up_the_Python_virtual_environment_venv)
[
Conclusion
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#Conclusion)
[
COPY & PASTE cheatsheet – for installing latest Python 3.10, 3.9, 3.8 or 3.7 on Linux CentOS 7, 8
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#COPY_PASTE_cheatsheet_for_installing_latest_Python_310_39_38_or_37_on_Linux_CentOS_7_8)




## Prerequisites

You will need functional Linux CentOS 7 or 8 machine,  an access to the root account and of course an internet connection.

All the steps you can perform as an non-root user but with a support of the  sudo
```
sudo
```
command.



 

## Step 1 – prepare CentOS for Python compilation

It is a good idea to have up-to-date OS system before you start doing anything else. Let’s update your CentOS with the  yum
```
yum
```
command.

Update your the linux boxsudo yum -y updatesudo yum -y update
```
sudo yum -y update

```

You also need some necessary libraries and developer tools to allow you to build and compile software from source code. I chose the minimal amount of packages those are included in CentOS as well. To install them use again   yum
```
yum
```
  command .

Install libraries and developer toolssudo yum -y install wget yum-utils gcc openssl-devel bzip2-devel libffi-develsudo yum -y install wget yum-utils gcc openssl-devel bzip2-devel libffi-devel
```
sudo yum -y install wget yum-utils gcc openssl-devel bzip2-devel libffi-devel
```

 

## Step 2 – download and unpack Python source code

We download the a source code of latest Python from the official Python page[ https://www.python.org/ftp/python/](https://www.python.org/ftp/python/) and extract Python-3.10.0.tgz
```
Python-3.10.0.tgz
```
to the  /tmp 
```
/tmp 
```
directory.

To do that perform this set of bash commands.

Download and unpack Python source codecd /tmp/wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgztar xzf Python-3.10.0.tgzcd Python-3.10.0cd /tmp/
wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz
tar xzf Python-3.10.0.tgz
cd Python-3.10.0
```
cd /tmp/
wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz
tar xzf Python-3.10.0.tgz
cd Python-3.10.0
```

 

## Step 3 – compile Python source code into binaries

At the moment we have everything ready for compiling the actual Python source code.



We are going to use the switch --prefix=/opt/python310
```
--prefix=/opt/python310
```
to set the root directory for all Python binaries and libraries. Of course, you can choose a folder according to your needs.  For better performance we are going to use a switch --enable-optimizations
```
--enable-optimizations
```
  for enabling PGO (profile guided optimisation) and so yielding an extra speed boost of Python binaries around 5-10%.

The command  make -j `nproc`
```
make -j `nproc`
```
  will ensure using of all fo your CPU cores and will decrease a compile-time and the command make altinstall
```
make altinstall
```
  is critical because of preserving the default shipped Python binary  /usr/bin/python
```
/usr/bin/python
```
.

**HINT** – To get the number of cpu cores of your Linux CentOS box, use these Bash commands  grep 'cpu cores' /proc/cpuinfo
```
grep 'cpu cores' /proc/cpuinfo
```
or  nproc
```
nproc
```
.

Now you have two options how to compile Python – with the static libraries or shared libraries. If you don’t know which way to take then use the option a).

Depending on a number of cpu cores, the compilation will take a few minutes.

 

**a) compile Python source with STATIC libraries – **almost in all of your cases or if you don´t know, use this option

Compile Python source with static librariessudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensionssudo make -j "$(nproc)"sudo make altinstallsudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions
sudo make -j "$(nproc)"
sudo make altinstall
```
sudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions
sudo make -j "$(nproc)"
sudo make altinstall
```

**b) compile Python source with SHARED libraries  – **you should know why you want this option otherwise use option a).

Compile Python source with shared librariessudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions --enable-shared LDFLAGS=\"-Wl,-rpath /usr/local/lib\"sudo make -j "$(nproc)"sudo make altinstallldconfigsudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions --enable-shared LDFLAGS=\"-Wl,-rpath /usr/local/lib\"
sudo make -j "$(nproc)"
sudo make altinstall
ldconfig
```
sudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions --enable-shared LDFLAGS=\"-Wl,-rpath /usr/local/lib\"
sudo make -j "$(nproc)"
sudo make altinstall
ldconfig
```

We already won’t need Python source code tarball so let’s delete it.

sudo rm /tmp/Python-3.10.0.tgzsudo rm /tmp/Python-3.10.0.tgz
```
sudo rm /tmp/Python-3.10.0.tgz
```

 

## Step 4 – make post-install stuff

We are going to make some symbolic links that are expected to exist for convenient Python usage.

Add some symbolic linkssudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python3sudo ln -s /opt/python310/bin/python3.10 /usr/bin/python310sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/pythonsudo ln -s /opt/python310/bin/python3.10-config /opt/python310/bin/python-configsudo ln -s /opt/python310/bin/pydoc3.10 /opt/python310/bin/pydocsudo ln -s /opt/python310/bin/idle3.10 /opt/python310/bin/idlesudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python3
sudo ln -s /opt/python310/bin/python3.10 /usr/bin/python310
sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python
sudo ln -s /opt/python310/bin/python3.10-config /opt/python310/bin/python-config
sudo ln -s /opt/python310/bin/pydoc3.10 /opt/python310/bin/pydoc
sudo ln -s /opt/python310/bin/idle3.10 /opt/python310/bin/idle
```
sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python3
sudo ln -s /opt/python310/bin/python3.10 /usr/bin/python310
sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python
sudo ln -s /opt/python310/bin/python3.10-config /opt/python310/bin/python-config
sudo ln -s /opt/python310/bin/pydoc3.10 /opt/python310/bin/pydoc
sudo ln -s /opt/python310/bin/idle3.10 /opt/python310/bin/idle

```

We are also  going to  add some symbolic links for the  pip
```
pip
```
binary.

Add some symbolic links for command pipsudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip3sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pipsudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip3
sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip
```
sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip3
sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip
```

 

## Step 5 – checking Python binaries

After installation you will find the Python interpreter at the location  /opt/python310/bin/
```
/opt/python310/bin/
```
.

Let’s  do some tests of Python binaries by typing:

Check Python binaries/opt/python310/bin/pip -V>>> pip 20.0.4 from /opt/python310/lib/python3.10/site-packages/pip (python 3.10.0)/opt/python310/bin/python -V>>> Python 3.10.0which python310>>> /usr/bin/python310/usr/bin/python310 -V>>> Python 3.10.0/opt/python310/bin/python3.10-config --prefix>>> /opt/python310# test out shipped Python 2.x whether it still ok/usr/bin/python -V>>> Python 2.7.5/opt/python310/bin/pip -V
>>> pip 20.0.4 from /opt/python310/lib/python3.10/site-packages/pip (python 3.10.0)

/opt/python310/bin/python -V
>>> Python 3.10.0

which python310
>>> /usr/bin/python310

/usr/bin/python310 -V
>>> Python 3.10.0

/opt/python310/bin/python3.10-config --prefix
>>> /opt/python310

# test out shipped Python 2.x whether it still ok
/usr/bin/python -V
>>> Python 2.7.5
```
/opt/python310/bin/pip -V
>>> pip 20.0.4 from /opt/python310/lib/python3.10/site-packages/pip (python 3.10.0)

/opt/python310/bin/python -V
>>> Python 3.10.0

which python310
>>> /usr/bin/python310

/usr/bin/python310 -V
>>> Python 3.10.0

/opt/python310/bin/python3.10-config --prefix
>>> /opt/python310

# test out shipped Python 2.x whether it still ok
/usr/bin/python -V
>>> Python 2.7.5

```

 

## Step 6 – setting up the Python virtual environment (venv)

Nowadays [Python virtual environment](https://docs.python.org/3/tutorial/venv.html) is a great tool and almost necessary for every Python project. It enables you to have more isolated Python spaces on one Linux box. Python project have its own set of dependencies and modules.

You can set up as many Python programming environments as you want.  Each of them is basically a directory that includes a few scripts and binaries, e.g. python
```
python
```
  or  pip
```
pip
```
.

So let’s create the one.

Create Python virtual environmentsudo /opt/python310/bin/python -m venv /home/hanz/mydjango.cz/envls -l /home/hanz/mydjango.eu/env>>> total 16>>> drwxr-xr-x 2 root root 4096 Nov 3 18:30 bin>>> drwxr-xr-x 2 root root 4096 Nov 3 18:30 include>>> drwxr-xr-x 3 root root 4096 Nov 3 18:30 lib>>> lrwxrwxrwx 1 root root 3 Nov 3 18:30 lib64 -> lib>>> -rw-r--r-- 1 root root 78 Nov 3 18:30 pyvenv.cfgsudo /opt/python310/bin/python -m venv /home/hanz/mydjango.cz/env

ls -l /home/hanz/mydjango.eu/env
>>> total 16
>>> drwxr-xr-x 2 root root 4096 Nov 3 18:30 bin
>>> drwxr-xr-x 2 root root 4096 Nov 3 18:30 include
>>> drwxr-xr-x 3 root root 4096 Nov 3 18:30 lib
>>> lrwxrwxrwx 1 root root 3 Nov 3 18:30 lib64 -> lib
>>> -rw-r--r-- 1 root root 78 Nov 3 18:30 pyvenv.cfg
```
sudo /opt/python310/bin/python -m venv /home/hanz/mydjango.cz/env

ls -l /home/hanz/mydjango.eu/env
>>> total 16
>>> drwxr-xr-x 2 root root 4096 Nov 3 18:30 bin
>>> drwxr-xr-x 2 root root 4096 Nov 3 18:30 include
>>> drwxr-xr-x 3 root root 4096 Nov 3 18:30 lib
>>> lrwxrwxrwx 1 root root 3 Nov 3 18:30 lib64 -> lib
>>> -rw-r--r-- 1 root root 78 Nov 3 18:30 pyvenv.cfg

```

Now that we have the environment created and next, we have to activate that with a command  source /home/hanz/mydjango.cz/env/bin/activate
```
source /home/hanz/mydjango.cz/env/bin/activate
```
We will again check Python binaries and run a small inline program “Hello, World!”. The command  deactivate
```
deactivate
```
  will disable the Python environment and will set back the shipped Python into our Linux machine.

Check Python virtual environmentsource /home/hanz/mydjango.cz/env/bin/activate>>> (env) [hanz@mydjango_cz /]#(env) [hanz@mydjango_cz /]# pip -V>>> pip 20.0.4 from /home/mydjango.cz/env/lib/python3.10/site-packages/pip (python 3.10.0)>>> (env) [hanz@mydjango_cz /]#(env) [hanz@mydjango_cz /]# python -c 'print("Hello, World!")'>>> (env) [hanz@mydjango_cz /]# Hello, World!(env) [hanz@mydjango_cz /]# deactivate>>> [hanz@mydjango_cz /]#source /home/hanz/mydjango.cz/env/bin/activate
>>> (env) [hanz@mydjango_cz /]#

(env) [hanz@mydjango_cz /]# pip -V
>>> pip 20.0.4 from /home/mydjango.cz/env/lib/python3.10/site-packages/pip (python 3.10.0)
>>> (env) [hanz@mydjango_cz /]#

(env) [hanz@mydjango_cz /]# python -c 'print("Hello, World!")'
>>> (env) [hanz@mydjango_cz /]# Hello, World!

(env) [hanz@mydjango_cz /]# deactivate
>>> [hanz@mydjango_cz /]#
```
source /home/hanz/mydjango.cz/env/bin/activate
>>> (env) [hanz@mydjango_cz /]#

(env) [hanz@mydjango_cz /]# pip -V
>>> pip 20.0.4 from /home/mydjango.cz/env/lib/python3.10/site-packages/pip (python 3.10.0)
>>> (env) [hanz@mydjango_cz /]#

(env) [hanz@mydjango_cz /]# python -c 'print("Hello, World!")'
>>> (env) [hanz@mydjango_cz /]# Hello, World!

(env) [hanz@mydjango_cz /]# deactivate
>>> [hanz@mydjango_cz /]#
```

## 
Conclusion

Congratulations!

At this point, you have installed the latest Python 3.10.0, Python 3.9.9, Python 3.8.12 or Python 3.7.11 on your local CentOS machine and for example, you can start coding any project with my favourite web framework [Django](https://www.djangoproject.com/).  Check out my [tutorial](https://www.workaround.cz/howto-configure-nginx-php-python-uwsgi-letsencrypt-ssl-https-http2-centos7/) for setting up a Django runtime environment build on Nginx web server and uWSGI Python gateway.

I hope this guide will help you and if you have some tips for improvements or found a mistake, let me know.

Enjoy!

Hanz



## COPY & PASTE cheatsheet – for installing latest Python 3.10, 3.9, 3.8 or 3.7 on Linux CentOS 7, 8

Just choose your desired version of Python, copy and paste into your Linux Bash command line and have a cup of coffee.  All is going to be finished in a few minutes.

**INFO** – Don’t worry about the shipped Python that is going to be operative as it is.


### Installing Python 3.10.0 to the directory /opt/python310

COPY & PASTE install script for Python 3.10cd /tmp/;wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz;tar xzf Python-3.10.0;cd Python-3.10.0;sudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;sudo make -j $(nproc);sudo make altinstall;sudo rm /tmp/Python-3.10.0.tgz;# add symbolic linkssudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python3;sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python;sudo ln -s /opt/python310/bin/python3.10-config /opt/python310/bin/python-config;sudo ln -s /opt/python310/bin/pydoc3.10 /opt/python310/bin/pydoc;sudo ln -s /opt/python310/bin/idle3.10 /opt/python310/bin/idle;sudo ln -s /opt/python310/bin/python3.10 /usr/bin/python310;sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip3;sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip;cd /tmp/;
wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz;
tar xzf Python-3.10.0;

cd Python-3.10.0;
sudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;
sudo make -j $(nproc);
sudo make altinstall;

sudo rm /tmp/Python-3.10.0.tgz;

# add symbolic links
sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python3;
sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python;
sudo ln -s /opt/python310/bin/python3.10-config /opt/python310/bin/python-config;
sudo ln -s /opt/python310/bin/pydoc3.10 /opt/python310/bin/pydoc;
sudo ln -s /opt/python310/bin/idle3.10 /opt/python310/bin/idle;
sudo ln -s /opt/python310/bin/python3.10 /usr/bin/python310;
sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip3;
sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip;
```
cd /tmp/;
wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz;
tar xzf Python-3.10.0;

cd Python-3.10.0;
sudo ./configure --prefix=/opt/python310 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;
sudo make -j $(nproc);
sudo make altinstall;

sudo rm /tmp/Python-3.10.0.tgz;

# add symbolic links
sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python3;
sudo ln -s /opt/python310/bin/python3.10 /opt/python310/bin/python;
sudo ln -s /opt/python310/bin/python3.10-config /opt/python310/bin/python-config;
sudo ln -s /opt/python310/bin/pydoc3.10 /opt/python310/bin/pydoc;
sudo ln -s /opt/python310/bin/idle3.10 /opt/python310/bin/idle;
sudo ln -s /opt/python310/bin/python3.10 /usr/bin/python310;
sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip3;
sudo ln -s /opt/python310/bin/pip3.10 /opt/python310/bin/pip;
```



### Installing Python 3.9.9 to the directory /opt/python39

COPY & PASTE install script for Python 3.9cd /tmp/;wget https://www.python.org/ftp/python/3.9.9/Python-3.9.9.tgz;tar xzf Python-3.9.9.tgz;cd Python-3.9.9;sudo ./configure --prefix=/opt/python39 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;sudo make -j $(nproc);sudo make altinstall;sudo rm /tmp/Python-3.9.9.tgz;# add symbolic linkssudo ln -s /opt/python39/bin/python3.9 /opt/python39/bin/python3;sudo ln -s /opt/python39/bin/python3.9 /opt/python39/bin/python;sudo ln -s /opt/python39/bin/python3.9-config /opt/python39/bin/python-config;sudo ln -s /opt/python39/bin/pydoc3.9 /opt/python39/bin/pydoc;sudo ln -s /opt/python39/bin/idle3.9 /opt/python39/bin/idle;sudo ln -s /opt/python39/bin/python3.9 /usr/bin/python39;sudo ln -s /opt/python39/bin/pip3.9 /opt/python39/bin/pip3;sudo ln -s /opt/python39/bin/pip3.9 /opt/python39/bin/pip;cd /tmp/;
wget https://www.python.org/ftp/python/3.9.9/Python-3.9.9.tgz;
tar xzf Python-3.9.9.tgz;

cd Python-3.9.9;
sudo ./configure --prefix=/opt/python39 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;
sudo make -j $(nproc);
sudo make altinstall;

sudo rm /tmp/Python-3.9.9.tgz;

# add symbolic links
sudo ln -s /opt/python39/bin/python3.9 /opt/python39/bin/python3;
sudo ln -s /opt/python39/bin/python3.9 /opt/python39/bin/python;
sudo ln -s /opt/python39/bin/python3.9-config /opt/python39/bin/python-config;
sudo ln -s /opt/python39/bin/pydoc3.9 /opt/python39/bin/pydoc;
sudo ln -s /opt/python39/bin/idle3.9 /opt/python39/bin/idle;
sudo ln -s /opt/python39/bin/python3.9 /usr/bin/python39;
sudo ln -s /opt/python39/bin/pip3.9 /opt/python39/bin/pip3;
sudo ln -s /opt/python39/bin/pip3.9 /opt/python39/bin/pip;
```
cd /tmp/;
wget https://www.python.org/ftp/python/3.9.9/Python-3.9.9.tgz;
tar xzf Python-3.9.9.tgz;

cd Python-3.9.9;
sudo ./configure --prefix=/opt/python39 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;
sudo make -j $(nproc);
sudo make altinstall;

sudo rm /tmp/Python-3.9.9.tgz;

# add symbolic links
sudo ln -s /opt/python39/bin/python3.9 /opt/python39/bin/python3;
sudo ln -s /opt/python39/bin/python3.9 /opt/python39/bin/python;
sudo ln -s /opt/python39/bin/python3.9-config /opt/python39/bin/python-config;
sudo ln -s /opt/python39/bin/pydoc3.9 /opt/python39/bin/pydoc;
sudo ln -s /opt/python39/bin/idle3.9 /opt/python39/bin/idle;
sudo ln -s /opt/python39/bin/python3.9 /usr/bin/python39;
sudo ln -s /opt/python39/bin/pip3.9 /opt/python39/bin/pip3;
sudo ln -s /opt/python39/bin/pip3.9 /opt/python39/bin/pip;
```

### Installing Python 3.8.12 to the directory /opt/python38

COPY & PASTE install script for Python 3.8cd /tmp/;wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz;tar xzf Python-3.8.12.tgz;cd Python-3.8.12;sudo ./configure --prefix=/opt/python38 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;sudo make -j $(nproc);sudo make altinstall;sudo rm /tmp/Python-3.8.12.tgz;# add symbolic linkssudo ln -s /opt/python38/bin/python3.8 /opt/python38/bin/python3;sudo ln -s /opt/python38/bin/python3.8 /opt/python38/bin/python;sudo ln -s /opt/python38/bin/python3.8-config /opt/python38/bin/python-config;sudo ln -s /opt/python38/bin/pydoc3.8 /opt/python38/bin/pydoc;sudo ln -s /opt/python38/bin/idle3.8 /opt/python38/bin/idle;sudo ln -s /opt/python38/bin/python3.8 /usr/bin/python38;sudo ln -s /opt/python38/bin/pip3.8 /opt/python38/bin/pip3;sudo ln -s /opt/python38/bin/pip3.8 /opt/python38/bin/pip;cd /tmp/;
wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz;
tar xzf Python-3.8.12.tgz;

cd Python-3.8.12;
sudo ./configure --prefix=/opt/python38 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;
sudo make -j $(nproc);
sudo make altinstall;

sudo rm /tmp/Python-3.8.12.tgz;

# add symbolic links
sudo ln -s /opt/python38/bin/python3.8 /opt/python38/bin/python3;
sudo ln -s /opt/python38/bin/python3.8 /opt/python38/bin/python;
sudo ln -s /opt/python38/bin/python3.8-config /opt/python38/bin/python-config;
sudo ln -s /opt/python38/bin/pydoc3.8 /opt/python38/bin/pydoc;
sudo ln -s /opt/python38/bin/idle3.8 /opt/python38/bin/idle;
sudo ln -s /opt/python38/bin/python3.8 /usr/bin/python38;
sudo ln -s /opt/python38/bin/pip3.8 /opt/python38/bin/pip3;
sudo ln -s /opt/python38/bin/pip3.8 /opt/python38/bin/pip;
```
cd /tmp/;
wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz;
tar xzf Python-3.8.12.tgz;

cd Python-3.8.12;
sudo ./configure --prefix=/opt/python38 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;
sudo make -j $(nproc);
sudo make altinstall;

sudo rm /tmp/Python-3.8.12.tgz;

# add symbolic links
sudo ln -s /opt/python38/bin/python3.8 /opt/python38/bin/python3;
sudo ln -s /opt/python38/bin/python3.8 /opt/python38/bin/python;
sudo ln -s /opt/python38/bin/python3.8-config /opt/python38/bin/python-config;
sudo ln -s /opt/python38/bin/pydoc3.8 /opt/python38/bin/pydoc;
sudo ln -s /opt/python38/bin/idle3.8 /opt/python38/bin/idle;
sudo ln -s /opt/python38/bin/python3.8 /usr/bin/python38;
sudo ln -s /opt/python38/bin/pip3.8 /opt/python38/bin/pip3;
sudo ln -s /opt/python38/bin/pip3.8 /opt/python38/bin/pip;

```

### Installing Python 3.7.11 to the directory /opt/python37

COPY & PASTE install script for Python 3.7.10cd /tmp/;wget https://www.python.org/ftp/python/3.7.11/Python-3.7.11.tgz;tar xzf Python-3.7.11.tgz;cd Python-3.7.11;sudo ./configure --prefix=/opt/python37 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;sudo make -j $(nproc);sudo make altinstall;sudo rm /tmp/Python-3.7.11.tgz;# add symbolic linkssudo ln -s /opt/python37/bin/python3.7 /opt/python37/bin/python3;sudo ln -s /opt/python37/bin/python3.7 /opt/python37/bin/python;sudo ln -s /opt/python37/bin/python3.7-config /opt/python37/bin/python-config;sudo ln -s /opt/python37/bin/pydoc3.7 /opt/python37/bin/pydoc;sudo ln -s /opt/python37/bin/idle3.7 /opt/python37/bin/idle;sudo ln -s /opt/python37/bin/python3.7 /usr/bin/python37;sudo ln -s /opt/python37/bin/pip3.7 /opt/python37/bin/pip3;sudo ln -s /opt/python37/bin/pip3.7 /opt/python37/bin/pip;cd /tmp/;
wget https://www.python.org/ftp/python/3.7.11/Python-3.7.11.tgz;
tar xzf Python-3.7.11.tgz;

cd Python-3.7.11;
sudo ./configure --prefix=/opt/python37 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;
sudo make -j $(nproc);
sudo make altinstall;

sudo rm /tmp/Python-3.7.11.tgz;

# add symbolic links
sudo ln -s /opt/python37/bin/python3.7 /opt/python37/bin/python3;
sudo ln -s /opt/python37/bin/python3.7 /opt/python37/bin/python;
sudo ln -s /opt/python37/bin/python3.7-config /opt/python37/bin/python-config;
sudo ln -s /opt/python37/bin/pydoc3.7 /opt/python37/bin/pydoc;
sudo ln -s /opt/python37/bin/idle3.7 /opt/python37/bin/idle;
sudo ln -s /opt/python37/bin/python3.7 /usr/bin/python37;
sudo ln -s /opt/python37/bin/pip3.7 /opt/python37/bin/pip3;
sudo ln -s /opt/python37/bin/pip3.7 /opt/python37/bin/pip;
```
cd /tmp/;
wget https://www.python.org/ftp/python/3.7.11/Python-3.7.11.tgz;
tar xzf Python-3.7.11.tgz;

cd Python-3.7.11;
sudo ./configure --prefix=/opt/python37 --enable-optimizations --with-system-ffi --with-computed-gotos --enable-loadable-sqlite-extensions;
sudo make -j $(nproc);
sudo make altinstall;

sudo rm /tmp/Python-3.7.11.tgz;

# add symbolic links
sudo ln -s /opt/python37/bin/python3.7 /opt/python37/bin/python3;
sudo ln -s /opt/python37/bin/python3.7 /opt/python37/bin/python;
sudo ln -s /opt/python37/bin/python3.7-config /opt/python37/bin/python-config;
sudo ln -s /opt/python37/bin/pydoc3.7 /opt/python37/bin/pydoc;
sudo ln -s /opt/python37/bin/idle3.7 /opt/python37/bin/idle;
sudo ln -s /opt/python37/bin/python3.7 /usr/bin/python37;
sudo ln -s /opt/python37/bin/pip3.7 /opt/python37/bin/pip3;
sudo ln -s /opt/python37/bin/pip3.7 /opt/python37/bin/pip;
```

[

](https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fwww.workaround.cz%2Fhowto-build-compile-install-latest-python-310-39-38-37-centos-7-8%2F)[](http://twitter.com/intent/tweet?text=Howto%20build%2C%20compile%20and%20install%20latest%20Python%203.10%2C%203.9%2C%203.8%2C%203.7%20on%20Linux%20CentOS%207%2C%208&url=https%3A%2F%2Fwww.workaround.cz%2Fhowto-build-compile-install-latest-python-310-39-38-37-centos-7-8%2F)[](http://www.linkedin.com/shareArticle?mini=true&url=https%3A%2F%2Fwww.workaround.cz%2Fhowto-build-compile-install-latest-python-310-39-38-37-centos-7-8%2F&title=Howto%20build%2C%20compile%20and%20install%20latest%20Python%203.10%2C%203.9%2C%203.8%2C%203.7%20on%20Linux%20CentOS%207%2C%208)[](http://reddit.com/submit?url=https%3A%2F%2Fwww.workaround.cz%2Fhowto-build-compile-install-latest-python-310-39-38-37-centos-7-8%2F&title=Howto%20build%2C%20compile%20and%20install%20latest%20Python%203.10%2C%203.9%2C%203.8%2C%203.7%20on%20Linux%20CentOS%207%2C%208) 


Categories [Linux sysadmin tips](https://www.workaround.cz/category/linux-sysadmin-tips/), [Python tips](https://www.workaround.cz/category/python-tips/) 
Post navigation

[Howto make upload form and process image in Django](https://www.workaround.cz/howto-make-upload-form-process-image-django/)[Howto build Django form with Ajax and Boostrap 4](https://www.workaround.cz/howto-build-django-form-ajax-boostrap/) 








### 18 thoughts on “Howto build, compile and install latest Python 3.10, 3.9, 3.8, 3.7 on Linux CentOS 7, 8”



- 


![media-tcsRdQ](media/media-tcsRdQ.comavatar425612ded4655c90004fc4927274467d)


tester 


[

27/10/2020 at 10:46 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-8670)






This is sad… Python was a first class citizen on Linux, and now Windows has a newer version of python prepackaged, while we need to compile latest python on Linux…






- 


![media-jBsgvj](media/media-jBsgvj.comavatar98d44f36f28d2f35883474a3e03c2abb)


dchassin 


[

09/06/2020 at 18:57 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7856)








How do I also install python3.x-devel so I can build and link C/C++ modules?








![media-VsaXnU](media/media-VsaXnU.comavatarb2f01e58a1375c0d699676d74b4d7b25)


Hanz 


[

11/06/2020 at 17:19 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7861)








Hi,

you can get all your needs with command 

"/opt/python39/bin/python3.9-config --help""/opt/python39/bin/python3.9-config --help"
```
"/opt/python39/bin/python3.9-config --help"
```

e.g. try to run 

"/opt/python39/bin/python3.9-config --includes""/opt/python39/bin/python3.9-config --includes"
```
"/opt/python39/bin/python3.9-config --includes"
```

Hope it helps.

Hanz








- 


![media-ufWxvo](media/media-ufWxvo.comavatar2101c8df38a72360f7aa6810c0055947)


Jorge 


[

02/06/2020 at 12:59 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7826)








I follow the steps to install 3.9b1

I have:

root@192 /h/h/A/Python-3.9# sqlite3

SQLite version 3.26.0 2018-12-01 12:34:55

Enter “.help” for usage hints.

Connected to a transient in-memory database.

Use “.open FILENAME” to reopen on a persistent database.

Got this error:

Traceback (most recent call last):

File “/media/test.py”, line 2, in

import sqlite3

File “/opt/python39/lib/python3.9/sqlite3/__init__.py”, line 23, in

from sqlite3.dbapi2 import *

File “/opt/python39/lib/python3.9/sqlite3/dbapi2.py”, line 27, in

from _sqlite3 import *

ModuleNotFoundError: No module named ‘_sqlite3’








![media-VsaXnU](media/media-VsaXnU.comavatarb2f01e58a1375c0d699676d74b4d7b25)


Hanz 


[

03/06/2020 at 16:17 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7829)








Hello,

before Python compilation you have to install SQlite into your Linux box.

I hope that helps.

Hanz








- 


![media-EqIbas](media/media-EqIbas.comavatar8c12608bd95493518e9606ffa9056aa7)


Andrei 


[

19/05/2020 at 08:17 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7765)








Thanks, Hanz! It was very useful for me.






- 


![media-iBuBjO](media/media-iBuBjO.comavatarcdff6c365e5e84c3f6a4ebf317931eda)


Andrew 


[

11/04/2020 at 19:05 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7603)








I followed all the steps to install Python 3.7.7 onto my Centos 8 server machine. However when I type python3 -V it returns “Command not found”.

Any ideas what is missing, steps 5 and 6 all work?








![media-VsaXnU](media/media-VsaXnU.comavatarb2f01e58a1375c0d699676d74b4d7b25)


Hanz 


[

12/04/2020 at 11:07 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7606)








Hi,

there is no python3 in my howto. You can fix it with another simlink 

"sudo ln -s /opt/python37/bin/python3.7 /usr/bin/python3;""sudo ln -s /opt/python37/bin/python3.7 /usr/bin/python3;"
```
"sudo ln -s /opt/python37/bin/python3.7 /usr/bin/python3;"
```

Hanz








- 


![media-ucvqql](media/media-ucvqql.comavatar9b6b86b83c4f20c7af09a35fdd217790)


Andreas Siegel 


[

01/04/2020 at 12:13 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7557)








Hi Hanz.

Now that was really useful.

It worked within some minutes (compiling does take some time)

Thanks.

Andy








![media-VsaXnU](media/media-VsaXnU.comavatarb2f01e58a1375c0d699676d74b4d7b25)


Hanz 


[

01/04/2020 at 13:41 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7558)








You are welcome,

Hanz








- 


![media-exIzUS](media/media-exIzUS.comavatare859d5914332e8d4370c0ee24ce27449)


Emmanuel Ngong 


[

02/03/2020 at 18:07 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7458)








Hello,

I followed the steps to configure python3.8 on my machine and ran into this error:

sudo: unable to execute ./configure: Permission denied

Can someone help me fix thus error ?








![media-VsaXnU](media/media-VsaXnU.comavatarb2f01e58a1375c0d699676d74b4d7b25)


Hanz 


[

03/03/2020 at 10:46 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7459)








Hello,

you have to own the execution permission in the script ” ./configure” , you can try something like chmod 777 -R /tmp/python-3.8.2 before run the script.

I houpe that it helps you.

Hanz








- 


![media-RyPbwX](media/media-RyPbwX.comavatard3f06bf7734b3ea7e76b1ec37710c45a)


Samuel 


[

09/01/2020 at 14:19 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7246)








Hi, me again

I did a gist to share my final script. Hope you like too

[https://gist.github.com/arcanosam/9eafe0ad5047e71a3b5ccfe7f23699ea](https://gist.github.com/arcanosam/9eafe0ad5047e71a3b5ccfe7f23699ea)








![media-VsaXnU](media/media-VsaXnU.comavatarb2f01e58a1375c0d699676d74b4d7b25)


admin 


[

09/01/2020 at 16:52 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7247)








Cool. That is good one. When i have a time, I am going to incorporate a few goods ideas from your script to my page. Thanks.








- 


![media-RyPbwX](media/media-RyPbwX.comavatard3f06bf7734b3ea7e76b1ec37710c45a)


Samuel 


[

09/01/2020 at 13:25 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7245)








That’s great! Thanks for sharing!

I think it’s awesome when I find a guide like this with this kind of details.

One thing, to future: If I want to remove (uninstall), I just need to remove the symbolic links and the installation folder in /opt/ ?








![media-VsaXnU](media/media-VsaXnU.comavatarb2f01e58a1375c0d699676d74b4d7b25)


admin 


[

09/01/2020 at 16:54 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-7248)








Yes, for removing just delete a directory e.g. /opt/python38








- 


![media-VVKIsC](media/media-VVKIsC.comavatar2f10e73aef036b200d6db135d30f23b7)


Riccardo 


[

03/01/2020 at 16:07 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-6687)








Hi,

Thanks for guide, but I have some problem.

I already have python 2.7 and 3.4

I wanted to install 3.8 in my /opt/python38

I followed your guide, but I cannot use pip in any way:

WARNING: pip is configured with locations that require TLS/SSL, however the ssl module in Python is not available.

I don’t have this problem with other python and I already had all the libraries for ssl installed (updated) before the configure.

What’s wrong?

Thanks








![media-VsaXnU](media/media-VsaXnU.comavatarb2f01e58a1375c0d699676d74b4d7b25)


admin 


[

05/01/2020 at 19:47 
](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#comment-6832)








Hi,

to compile Python with ssl support you have to installed in your Linux box openssl devel libraries “yum install openssl-devel openssl-static” before the compilation.

I houpe that it helps you.

Hanz











Comments are closed.











## Categories


- [Django tips](https://www.workaround.cz/category/django-tips/)

- [Linux sysadmin tips](https://www.workaround.cz/category/linux-sysadmin-tips/)

- [Python tips](https://www.workaround.cz/category/python-tips/)






## Recent Posts


- 
[Howto build Django form with Ajax and Boostrap 4](https://www.workaround.cz/howto-build-django-form-ajax-boostrap/)


- 
[Howto build, compile and install latest Python 3.10, 3.9, 3.8, 3.7 on Linux CentOS 7, 8](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/)


- 
[Howto make upload form and process image in Django](https://www.workaround.cz/howto-make-upload-form-process-image-django/)


- 
[Howto send html email with embedded image in Django](https://www.workaround.cz/howto-send-html-email-embedded-image-django/)


- 
[Howto make daemon in Python 3](https://www.workaround.cz/howto-make-code-daemon-python-3/)














© 2022 Python, Django tips and code snippets. 




[

](https://www.workaround.cz/howto-build-compile-install-latest-python-310-39-38-37-centos-7-8/#)