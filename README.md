# uv 使用教學 (uv Tutorial)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://docs.astral.sh/uv/)
[![image](https://img.shields.io/pypi/v/uv.svg)](https://pypi.python.org/pypi/uv)
[![image](https://img.shields.io/badge/python-3.12%20%7C%203.13-blue)](https://github.com/astral-sh/uv)


**uv** 是一款跨平台的 Python 環境管理工具，專為簡化專案的環境與依賴管理而設計。它提供直覺的命令列介面，讓開發者能快速建立、管理和切換虛擬環境，並輕鬆安裝或更新所需套件。uv 支援多個 Python 版本，能自動處理虛擬環境的建立與切換，讓開發者專注於程式開發，而不必擔心繁瑣的環境配置與依賴問題。

---

如果你從 git clone 下來的專案已包含 `pyproject.toml` 和 `uv.lock` ，這兩個檔案分別用於定義專案依賴與鎖定版本，只需執行以下指令：

```bash
uv sync
```

uv 會自動在專案資料夾內建立 `.venv` 虛擬環境並安裝所有依賴套件，將虛擬環境與系統 Python 隔離，避免衝突。專案只需維護 `pyproject.toml` 和 `uv.lock`，無需 `requirements.txt`，即可確保跨平台環境一致性。

若需在開發環境中使用 `Jupyter Notebook`，請先安裝 `uv`，然後執行下列指令將 Jupyter kernel 加入專案依賴：

```powershell
uv add --dev ipykernel
```

---

## 📦 安裝 uv

```bash
# macOS 和 Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

```powershell
# Windows
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## 🚀 專案初始化

- `uv init`  
  初始化專案，建立 `pyproject.toml`

- `uv venv --python 3.12`  
  建立虛擬環境並指定 Python 版本。若專案從 GitHub clone 下來，且已包含 `pyproject.toml` 與 `uv.lock`，可直接執行 `uv sync` 自動建立虛擬環境

- `uv sync`  
  根據 `pyproject.toml` 與 `uv.lock` 安裝或同步所有依賴套件與虛擬環境

---

## 🐍 Python 版本管理

- `uv python install`  
  安裝最新版本的 Python

- `uv python list`  
  列出可用的 Python 版本（已安裝的會顯示路徑）

- `uv python install 3.12`  
  安裝指定版本的 Python（如 3.12）

- `uv pin python 3.12`  
  設定專案預設使用的 Python 版本

---

## 📦 套件管理

- `uv tree`  
  顯示目前專案的依賴套件樹狀結構

- `uv add [套件名稱]`  
  新增套件到專案依賴

- `uv add [套件名稱]==1.0`  
  新增指定版本的套件

- `uv add [套件名稱] --dev`  
  新增開發用依賴（只在開發環境需要）

- `uv remove [套件名稱]`  
  移除專案依賴中的套件

- `uv add -r requirements.txt`  
  從 `requirements.txt` 匯入套件到專案依賴

- `uv add --dev ipykernel`  
  新增 Jupyter Notebook 開發用依賴

---

## ▶️ 執行專案

- `uv run main.py`  
  使用當前虛擬環境執行 `main.py`

- `uv run --python 3.12 main.py`  
  使用指定 Python 版本執行 `main.py`

---

> 建議：  
> - 所有依賴都用 `uv add` 管理，確保團隊環境一致  
> - 開發用工具（如 linters、測試框架）請加上 `--dev`

---
