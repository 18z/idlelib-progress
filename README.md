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
