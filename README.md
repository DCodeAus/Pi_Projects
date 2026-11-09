# Pi Projects

Small projects for a **Raspberry Pi** (a credit-card-sized computer) with a Pimoroni **Inky pHAT**, a little e-ink screen that plugs onto the Pi's pins. E-ink is the same kind of display as a Kindle: it keeps showing the last image even with the power off, so it suits things that update every few minutes. I set these up on a Pi Zero 2 W.

| Project | What it does |
|---|---|
| [`bitcoin_ticker/`](bitcoin_ticker/) | Shows the current Bitcoin price (or another coin) and the day's low and high on the screen, refreshing every few minutes. Prices come from the free [Kraken](https://www.kraken.com) public API, so no account or key is needed. Full setup steps are in [its README](bitcoin_ticker/README.md). |
| `name-badge.py` | Turns the screen into a "Hello, my name is…" badge. Based on Pimoroni's example. Run it with your name: `python3 name-badge.py --name "Dan"`. |

## What you need

- A Raspberry Pi with the 40-pin header (any model up to the Pi Zero 2 W has been tested), running Raspberry Pi OS.
- A Pimoroni Inky pHAT (it also works with the larger Inky wHAT).
- The Inky software. Follow the setup steps in [`bitcoin_ticker/README.md`](bitcoin_ticker/README.md); the same steps work for the name badge.

## Getting the code onto the Pi

Connect to your Pi over SSH (or with a keyboard and screen) and run:

```bash
git clone https://github.com/DCodeAus/Pi_Projects.git
cd Pi_Projects
```
