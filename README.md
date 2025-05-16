# uv 使用教學


使用 uv 工具來管理 Python 專案的環境與依賴

uv 官方網址 : https://docs.astral.sh/uv/

---

## 🚀 專案初始化

- `uv init`  
  初始化專案，建立 `pyproject.toml`

- `uv venv --python 3.12`  
  建立虛擬環境並指定 Python 版本，若專案從 GitHub clone 下來，且已包含 `pyproject.toml` 與 `uv.lock`，可直接執行 `uv sync` 自動建立虛擬環境

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
