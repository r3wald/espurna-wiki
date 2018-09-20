# Espurna OTA Manager

Espurna comes with a built in OTA management script located at `code/ota.py`. This script can be used for discovering and updating existing devices running espurna on your network.

## Setup (using virtualenv)

```
cd ~/code
virtualenv .venv
source .venv/bin/activate
pip install -r requirements.txt
```
### Usage

`python ota.py -h`