# SamsungTvRemote

amsungctl --host 192.168.178.16 --port 8001 --method websocket -i
samsungctl --host 192.168.178.16 --port 8001 --method websocket KEY_ENTER
yad --title "Remote Control" --text "Samsung Smart TV" --width 250 --height 400 --form --columns 2 --field "Power:FBTN" 'bash -c "echo Power"'  --field "Vol +:FBTN" 'bash -c "echo Volume Up"' --field "Vol -":FBTN 'bash -c "echo Volume Down"' --field "Input:FBTN" "bash -c 'echo "Input"'"  --field "Chan +:FBTN" 'echo "Channel up"' --field "Chan -:FBTN" 'bash -c "echo Channel Down"'


#!/usr/bin/env python3

import samsungctl
import time

config = {
    "name": "Remote Control",
    "description": "Samsung Smart TV",
    "id": "",
    "host": "192.168.178.16",
    "port": 8001,
    "method": "websocket",
    "timeout": 0,
}

with samsungctl.Remote(config) as remote:
    for i in range(10):
        remote.control("KEY_MENU")
        time.sleep(0.1)

