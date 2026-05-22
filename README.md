# tuvpn

Pixi-based TU Berlin VPN setup using `openconnect-sso` for SAML/SSO authentication with 2FA.

## Motivation

The [official TU Berlin guide](https://www.tu.berlin/campusmanagement/it-support/vpn-installation-und-nutzung-unter-linux-mit-openconnect-sso) installs everything system-wide via `apt` and `pip`. This repo instead uses a [pixi](https://pixi.sh) virtual environment, keeping all dependencies self-contained in the project folder without touching the system. This is particularly useful on immutable distros like Fedora Silverblue/Atomic where system-wide installs are undesirable.

## Requirements

- [pixi](https://pixi.sh)
- A TU Berlin account with TOTP set up

## Setup

Clone the repo:

```bash
git clone git@github.com:bxiong/tuvpn.git ~/tuvpn
cd ~/tuvpn
pixi install
```

Add aliases to your `~/.zshrc` and/or `~/.bashrc`:

```bash
alias tuvpn-split='cd ~/tuvpn && pixi run vpn-split'
alias tuvpn-full='cd ~/tuvpn && pixi run vpn-full'
```

Then reload your shell:

```bash
source ~/.zshrc
```

## Usage

Connect with split tunnel (recommended for everyday use — only TU traffic goes through VPN):

```bash
tuvpn-split
```

Connect with full tunnel (all traffic routed through TU Berlin):

```bash
tuvpn-full
```

A browser window will open for SSO login. Enter your TUB username, password, and TOTP code.

## Notes

- Tested on Fedora Silverblue with a HiDPI screen (`QT_SCALE_FACTOR=2.2`)
- The `setuptools==69.5.1` pin is required due to `pkg_resources` being removed in newer versions
- Certificate warning `signer not found` is expected and harmless
