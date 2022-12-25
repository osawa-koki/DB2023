# sample-hugo

Hugoの学習用プロジェクト。  

## 環境構築方法

### Chocolateyのインストール

ChocolateyというWindows用のパッケージマネージャをインストール。  
Powershellで以下のコマンドを実行。

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

> <https://chocolatey.org/install#individual>

### Hugoのインストール

```shell
choco install hugo-extended
```

### 新規プロジェクトの作成

```shell
hugo new site <プロジェクト名>
```

### デバグ実行

```shell
hugo server
```

### デプロイ用ビルド

```shell
hugo
```

## 開発環境

| モジュール | バージョン |
| ---- | ---- |
| Windows | 11 Home |
| Hugo | v0.109.0 |

## 参考文献

- <https://gohugo.io/getting-started/quick-start/>
- <https://www.pc-koubou.jp/magazine/30737>
- <https://maku77.github.io/hugo/>
- <https://girigiribauer.com/tech/20200128/>
