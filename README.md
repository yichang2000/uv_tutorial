# uv 使用教學 (uv Tutorial)

[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://docs.astral.sh/uv/)
[![image](https://img.shields.io/pypi/v/uv.svg)](https://pypi.python.org/pypi/uv)
[![image](https://img.shields.io/badge/python-3.12%20%7C%203.13-blue)](https://github.com/astral-sh/uv)

**uv** 是一款跨平台的 Python 環境與套件管理軟體，由 Rust 編寫，速度極快。專為簡化專案的環境與依賴管理而設計，提供直覺的命令列介面，讓開發者能快速建立、管理和切換虛擬環境，並輕鬆安裝或更新所需套件。uv 支援多個 Python 版本，能自動處理虛擬環境的建立與切換，讓開發者專注於程式開發，而不必擔心繁瑣的環境配置與依賴衝突問題。

---

## ⚡ 快速上手 (Clone 專案後)

如果您從 Git clone 下來的專案已包含 `pyproject.toml` 和 `uv.lock`（這兩個檔案分別用於定義專案依賴與鎖定版本），只需執行以下指令：

```bash
uv sync
```

uv 會自動在專案資料夾內下載對應的 Python 版本、建立 `.venv` 虛擬環境，並安裝所有依賴套件。專案只需維護 `pyproject.toml` 和 `uv.lock`，無需 `requirements.txt`，即可確保跨平台環境的一致性。

若需在開發環境中使用 Jupyter Notebook，請執行 `uv add --dev ipykernel` 將 Jupyter kernel 加入專案的開發依賴中。

---

## 🔒 企業憑證與代理伺服器設定

在某些情況下，您可能需要使用作業系統原生的憑證儲存庫，特別是當您依賴已包含在系統中的企業信任根憑證（例如：強制透過企業 Proxy 上網）時。您可以使用 `--native-tls` 參數執行，或設定環境變數 `export UV_NATIVE_TLS=true`：

```bash
# 建立環境，並指示 uv 使用系統的信任儲存庫
uv venv --python 3.12 --native-tls

# 安裝套件，並指示 uv 使用系統的信任儲存庫
uv add [套件名稱] --native-tls
```

---

## 📦 安裝 uv

**macOS 和 Linux**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

---

## 🚀 專案初始化與同步

```bash
# 初始化專案，自動建立 pyproject.toml 與基本專案結構
uv init

# 建立虛擬環境並指定 Python 版本
# 若專案已包含 pyproject.toml 與 uv.lock，可直接執行 uv sync 自動建立虛擬環境
uv venv --python 3.12

# 根據 pyproject.toml 與 uv.lock 建立或同步所有依賴套件與虛擬環境
uv sync
```

---

## 🐍 Python 版本管理

```bash
# 安裝最新版本的 Python
uv python install

# 安裝指定版本的 Python（如 3.12）
uv python install 3.12

# 列出可用的 Python 版本
# 加上 --only-installed 參數則只顯示目前已安裝的版本與路徑
uv python list

# 查看當前啟動環境中的 Python 版本
uv run python --version

# 設定專案預設使用的 Python 版本（會寫入 .python-version 檔案）
uv python pin 3.12

# 解除安裝指定版本的 Python
uv python uninstall 3.12
```

---

## 📦 套件管理 (Project Management)

```bash
# 顯示目前專案的依賴套件樹狀結構
uv tree

# 新增套件到專案依賴
uv add [套件名稱]

# 新增指定版本的套件
uv add [套件名稱]==1.0.0

# 新增開發用依賴（只在開發環境需要，例如：pytest, ruff）
uv add [套件名稱] --dev

# 移除專案依賴中的套件
uv remove [套件名稱]

# 重新生成或同步 uv.lock 檔案
uv lock

# 單獨將某個套件升級到最新版本
# 若是 Jupyter 開發環境，需再執行一次 uv add --dev ipykernel 來更新套件
uv lock --upgrade-package [套件名稱]

# 從舊有的 requirements.txt 轉換並匯入套件到專案依賴中
uv add -r requirements.txt

# 將目前的依賴匯出成標準的 requirements.txt，方便用於 CI/CD 或 Docker 部署
uv export > requirements.txt
```

---

## ▶️ 執行專案與單一腳本

```bash
# 使用當前虛擬環境執行 main.py
# 若沒有虛擬環境，uv 會自動建立並安裝依賴
uv run main.py

# 使用指定 Python 版本執行 main.py
uv run --python 3.12 main.py
```

> 💡 **單一腳本執行 (Standalone Scripts)**：如果您只有一個獨立的腳本，支援 PEP 723 內聯元資料。例如 `script.py` 中標註了依賴：
>
> ```python
> # /// script
> # requires-python = ">=3.11"
> # dependencies = ["requests", "rich"]
> # ///
> import requests
> ```
>
> 直接執行 `uv run script.py`，uv 會在背景建立臨時且隔離的環境來執行它，不會污染系統環境。

---

## 🔧 全域工具管理 (Tools & uvx)

```bash
# 全域安裝獨立工具（例如：uv tool install ruff）
uv tool install [工具名稱]

# 查詢已安裝工具的版本
[工具名稱] --version

# 升級指定工具，或使用 --all 參數升級所有工具
uv tool upgrade [工具名稱]
```

> 🔥 **免安裝直接執行 (uvx)**：如果想臨時執行某個工具而不想安裝它，可使用 `uvx`（等同於 `uv tool run`）：
>
> ```bash
> # 臨時下載並執行 ruff 進行程式碼檢查
> uvx ruff check .
>
> # 臨時執行 pycowsay
> uvx pycowsay "Hello uv!"
> ```

---

## ⚡ 極速 pip 替代方案 (uv pip)

```bash
# 替代傳統 pip，安裝速度快上數十倍
uv pip install [套件名稱]

# 極速安裝 requirements 檔案內的依賴
uv pip install -r requirements.txt

# 替代 pip-tools 進行依賴編譯
uv pip compile requirements.in -o requirements.txt
```

---

## 🧰 實用維護指令

```bash
# 清理所有快取項目，釋放硬碟空間
uv cache clean

# 清理過期或不再使用的快取項目
uv cache prune

# 顯示 uv 快取目錄路徑
uv cache dir

# 顯示 uv 全域工具的安裝目錄路徑
uv tool dir

# 顯示 uv 自動安裝的 Python 版本存放路徑
uv python dir

# 將 uv 本身更新到最新版本
uv self update
```

---

## 💡 最佳實務建議

- 團隊開發時，請將 `pyproject.toml` 與 `uv.lock` 兩者都加入 Git 版本控制，確保所有成員 `uv sync` 出來的環境 100% 相同。
- 開發用工具（如 Linter、測試框架等）請務必加上 `--dev` 參數進行安裝（`uv add --dev`），以保持正式上線環境（Production）的輕量與純淨。
