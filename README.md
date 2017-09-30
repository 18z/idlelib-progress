# idlelib-progress

1. Build and test python on ubuntu ```./configure --with-pydebug && make -j```, ```./python -m test -j3```
    ```
    [dio@dio-VirtualBox][~][1] $ cat /etc/*-release
    DISTRIB_ID=Ubuntu
    DISTRIB_RELEASE=16.04
    DISTRIB_CODENAME=xenial
    DISTRIB_DESCRIPTION="Ubuntu 16.04.3 LTS"
    NAME="Ubuntu"
    VERSION="16.04.3 LTS (Xenial Xerus)"
    ID=ubuntu
    ID_LIKE=debian
    PRETTY_NAME="Ubuntu 16.04.3 LTS"
    VERSION_ID="16.04"
    HOME_URL="http://www.ubuntu.com/"
    SUPPORT_URL="http://help.ubuntu.com/"
    BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
    VERSION_CODENAME=xenial
    UBUNTU_CODENAME=xenial
    ```
2. ```./python -m test test_idle```
    ```
    [dio@dio-VirtualBox][cpython][2] $ ./python -m test test_idle
    Run tests sequentially
    0:00:00 load avg: 0.23 [1/1] test_idle
    test_idle skipped -- No module named '_tkinter'
    test_idle skipped

    1 test skipped:
        test_idle

    Total duration: 66 ms
    Tests result: SUCCESS
    ```

3. 解決 2. 的方法，就是參考 [build-dependency](https://docs.python.org/devguide/setup.html#build-dependencies)
    ```
    Python build finished successfully!
    The necessary bits to build these optional modules were not found:
    _uuid                                                          
    To find the necessary bits, look in setup.py in detect_modules() for the module's name.


    The following modules found by detect_modules() in setup.py, have been
    built by the Makefile instead, as configured by the Setup files:
    atexit                pwd                   time               

    running build_scripts
    copying and adjusting /home/dio/Documents/cpython/Tools/scripts/pydoc3 -> build/scripts-3.7
    copying and adjusting /home/dio/Documents/cpython/Tools/scripts/idle3 -> build/scripts-3.7
    copying and adjusting /home/dio/Documents/cpython/Tools/scripts/2to3 -> build/scripts-3.7
    copying and adjusting /home/dio/Documents/cpython/Tools/scripts/pyvenv -> build/scripts-3.7
    changing mode of build/scripts-3.7/pydoc3 from 664 to 775
    changing mode of build/scripts-3.7/idle3 from 664 to 775
    changing mode of build/scripts-3.7/2to3 from 664 to 775
    changing mode of build/scripts-3.7/pyvenv from 664 to 775
    renaming build/scripts-3.7/pydoc3 to build/scripts-3.7/pydoc3.7
    renaming build/scripts-3.7/idle3 to build/scripts-3.7/idle3.7
    renaming build/scripts-3.7/2to3 to build/scripts-3.7/2to3-3.7
    renaming build/scripts-3.7/pyvenv to build/scripts-3.7/pyvenv-3.7
    [dio@dio-VirtualBox][cpython][0] $ ./python -m test test_idle
    Run tests sequentially
    0:00:00 load avg: 2.47 [1/1] test_idle
    1 test OK.

    Total duration: 1 sec
    Tests result: SUCCESS

    ```
4. idlelib test
    ```
    [dio@dio-VirtualBox][cpython][0] $ ./python -m test.test_idle
    Ran 372 tests in 6.077s

    OK (skipped=1)
    ```
5. fire up idle ```/home/dio/Documents/cpython/python __main__.py```

6. fire up idle ```cpython -m idlelib```

7. config.py 有 main function。main function 功能是跑 test。所以打算從 test_config 下手。

8. test_config line 32 為切入點，-> line 23 -> config.py.line.784 -> config.py.line.152

9. idlelib.testing = True, testing 值藏在 idlelib/__init__.py 中。
