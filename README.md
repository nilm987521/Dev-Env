# 開發環境表準化

主要是透過容器技術，打造輕量化且可版控的開發環境。

## Linux / Mac 
如果是使用VSCode作為IED，僅需要安裝devcontainer外掛。
或是使用其他可支持遠端開發(在容器安裝後端)的IDE(如IntelliJ系列)。
> 1. 雖然Mac同Windows一樣是用虛擬機執行Docker，但因編譯效能問題較小，故可採用devcontainer方案。
> 2. XForwarding會因效能問題，影響使用者體驗，暫時不考慮。

## Windows 
將容器變成WSL虛擬機。
IDE不限於VSCode，但須安裝在WSL虛擬機內，透過XForwarding使用。
> 1. Windows有無完成WSL的XForwarding效能問題。

## WSL的操作流程

0. 抓最新的編譯環境Image

1. 執行指令，建立Image
```bash
docker build -t dev-env .
```

2. 用建立好的Image，產生容器
```bash
docker run -d --name dev-wsl dev-wsl
```

3. 將容器輸出成tar檔
```
docker export -o dev-wsl.tar dev-wsl
```

4. 透過wsl指令，將容器的tar檔建立成虛擬機
```
wsl --import <wsl名稱> <虛擬機硬碟的存放位置> <dev-wsl.tar檔位置> --version 2
```

## VSCode的devcontainer使用方法

1. 將此專案放置開發專案的.devcontainer資料夾內(示意圖如下)
> 開發專案
> ├ .devcontainer
> │ ├ .sysinit  
> │ ├ Dockerfile-CICD  
> │ ├ Dockerfile-Dev  
> │ ├ README.md  
> │ └ devcontainer.json
> ├ <Source Code> 
 
