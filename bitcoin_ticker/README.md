# Bitcoin ticker

Shows the current Bitcoin price in US dollars, plus the day's low and high, on a Pimoroni Inky pHAT e-ink screen. Prices come from the free [Kraken](https://www.kraken.com) public API, so no account or key is needed. A cron job (a timer built into Linux) re-runs it every few minutes to keep the screen up to date.

Based on [naviavia/bitcoin_ticker](https://github.com/naviavia/bitcoin_ticker), adapted for the Pi Zero 2 W.

## Table of contents
* [Requirements](#requirements)
* [Setup](#setup)
* [Config](#config)


## Requirements
- Raspberry Pi (all models up to the Pi Zero 2 W, tested 08/2022)
- Inky pHAT e-ink display

## Setup

These steps are typed into the Pi's terminal. Connect over SSH from your computer (`ssh <username>@<pi-name>.local`) or plug in a keyboard and screen.

1. **Install the Inky software** with Pimoroni's installer. It turns on the connections the screen needs and installs the Inky Python library:
   ```bash
   curl https://get.pimoroni.com/inky | bash
   ```
   Follow its questions, then **reboot** the Pi (`sudo reboot`).

2. **If you get an "externally-managed-environment" error** when installing Python packages: newer Raspberry Pi OS versions stop `pip` from installing into the system's Python, to protect the system. Don't delete or move the `EXTERNALLY-MANAGED` file to get around it. Instead, create a *virtual environment* (a private copy of Python just for this project) and install into that:
   ```bash
   python3 -m venv ~/inky-env
   ~/inky-env/bin/pip install inky requests pillow font-fredoka-one
   ```
   Then use `~/inky-env/bin/python3` wherever these steps say `python3`. (Pimoroni's installer may offer to create a virtual environment for you; if it does, use that one instead.)

3. **Download this code:**
   ```bash
   cd ~
   git clone https://github.com/DCodeAus/Pi_Projects.git
   ```

4. **Test it** by running it once. The screen should update within about 30 seconds:
   ```bash
   python3 ~/Pi_Projects/bitcoin_ticker/bitcoin.py
   ```

5. **Make it refresh automatically** with cron, which runs commands on a timer. Open your cron list:
   ```bash
   crontab -e
   ```
   (If it asks which editor to use, pick `nano`.) Add this line at the bottom, then save and exit (in nano: `Ctrl+O`, Enter, `Ctrl+X`):
   ```
   */5 * * * * python3 /home/<username>/Pi_Projects/bitcoin_ticker/bitcoin.py
   ```
   Replace `<username>` with your username on the Pi (run `whoami` to check). `*/5` means every 5 minutes; use `*/15` for every 15 minutes. E-ink screens flash while they refresh, and don't need updating every minute. Add any options from [Config](#config) to the end of the line.

## Config

Add these options to the end of the command (or of the cron line):

| Option | What it does |
|---|---|
| `--flip true` | Turns the image upside down, for when the Pi is mounted the other way up. |
| `--pair adagbp` | Shows a different coin and currency, here Cardano in British pounds. Use any pair Kraken offers, but the currency (the last three letters) must be USD, AUD, GBP, EUR or CAD, the ones the script knows a symbol for. If Kraken doesn't recognise it, the script prints `Invalid coin pair`. |
| `--debug true` | Prints extra details in the terminal, useful when something isn't working. |

For example:

```
*/5 * * * * python3 /home/<username>/Pi_Projects/bitcoin_ticker/bitcoin.py --pair ethaud --flip true
```
