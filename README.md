
# Aeronix Hackothon

A Python toolkit built during the **Aeronix Hackothon** to automate device bring-up and verification workflows.
The repository currently centers around the `lora-bringup-gen` module, intended for streamlining LoRa/LoRaWAN node setup, configuration scaffolding, and basic sanity checks.

---

## ✨ Features

* Generate bring-up scaffolding for LoRa devices (configs, scripts, and checklists).
* Simple CLI to run device setup and smoke tests.
* Modular Python code for extending to new boards/radios.
* Developer-friendly structure (VS Code settings included).

---

## 🗂️ Project Structure

```
Aeronix-Hackothon/
├─ lora-bringup-gen/        # Core Python package / scripts for LoRa bring-up
├─ .vscode/                 # Editor settings/tasks for consistent dev env
├─ .gitignore
└─ README.md
```
---

## 🚀 Quickstart

### Prerequisites

* Python 3.10+
* [Optional] GNU Make (if you keep make targets)
* [Optional] Docker (if you plan to containerize)

### Setup

```bash
# clone
git clone https://github.com/parvathinalla/Aeronix-Hackothon.git
cd Aeronix-Hackothon

# create & activate a venv
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# install
pip install --upgrade pip
pip install -r requirements.txt  # if you have this file
# or, if it's a module:
pip install -e ./lora-bringup-gen
```

---

## 🧰 Usage

> Adjust the command names to match your actual entrypoints/scripts.

### CLI

```bash
# show help
python -m lora_bringup_gen --help

# generate a bring-up template for a device
python -m lora_bringup_gen init --device [DEVICE_NAME] --band [EU868|US915|AS923] --out out/[DEVICE_NAME]

# run basic connectivity/sanity checks
python -m lora_bringup_gen check --port [SERIAL_PORT] --baud [115200]
```

### Common Examples

```bash
# 1) Create project scaffolding
python -m lora_bringup_gen init --device nodeA --band US915 --out out/nodeA

# 2) Populate credentials (DevEUI/AppEUI/AppKey or similar)
python -m lora_bringup_gen creds set \
  --deveui [HEX] --appeui [HEX] --appkey [HEX] \
  --project out/nodeA

# 3) Flash and verify
python -m lora_bringup_gen flash --port /dev/ttyUSB0 --project out/nodeA
python -m lora_bringup_gen check  --port /dev/ttyUSB0
```

---

## ⚙️ Configuration

Place project settings in one of the following (whichever your code expects):

* `out/<project>/bringup.yaml` – main bring-up config
* `.env` – environment variables (tokens, broker endpoints, etc.)

**Environment variables (examples):**

```
LORA_REGION=US915
LNS_HOST=[your-network-server]
LNS_API_KEY=[token]
SERIAL_PORT=/dev/ttyUSB0
```

---

## 🧪 Testing

```bash
# if you use pytest
pytest -q

# or if tests are inside the module
python -m pytest lora-bringup-gen/tests -q
```

---

## 🛠️ Development

* Code style: `ruff` / `black` (add note if you use them)
* Type checking: `mypy` (optional)
* Pre-commit: include config if present

```bash
pip install -r dev-requirements.txt
pre-commit install
```

---

## 🗺️ Roadmap

* [ ] Support additional frequency plans and boards
* [ ] Add end-to-end bring-up demo with sample telemetry
* [ ] CI: lint + test workflow
* [ ] Docker image for repeatable lab runs

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch: `git checkout -b feat/something`
3. Commit changes: `git commit -m "feat: add something"`
4. Push and open a PR

---

## 🙌 Acknowledgments

* Built for **Aeronix Hackothon** by **parvathi and Bindhu**
* Thanks to the maintainers of the LoRa/LoRaWAN ecosystem tools we rely on

---
