---
title:  "使用 Yubikey 儲存 OpenPGP 私鑰"
date:   2019-04-07 15:13:00 +0800
categories:
  - GnuPG
  - yubikey
tag:
  - yubikey
  - openpgp
  - gpg
toc: true
header:
  teaser: https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/01.png
  og_image: https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/01.png
---
本篇文章記錄如何在 Windows 下使用 YubkiKey 搭配 GnuPG 工具，在 Yubikey 上建立金鑰對並儲存備份，以及如何將備份還原至 YubiKey 之中。

## 準備需求
- 支援 OpenPGP 的 Yubikey

| YubiKey 4 | YubiKey NEO | YubiKey 4 Nano |
| YubiKey NEO-n | YubiKey 5 NFC | YubiKey 5 Nano |
| YubiKey 4C | YubiKey 4C Nano | YubiKey 5C |
| YubiKey 5C Nano | --- | --- |


- GnuPG 軟體 [GPG4Win](https://www.gpg4win.org/download.html)

## 操作步驟
### 初始設定 Yubikey
1. 開啟 Kleopatra > 工具(T) > Manage Smartcards
![1](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/01.png)
2. 修改 Cardholder 成自己的名字
3. 使用 Change PIN 修改 PIN 碼，預設值 123456
4. 使用 Change Admin PIN 修改管理 PIN 碼，預設值 12345678

### 建立金鑰對及備份私鑰
1. 檔案(F) > New Key Pair...
![2](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/02.png)
2. 建立個人 OpenPGP 金鑰配對 > 輸入Name和Email
![3](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/03.png)
3. 進階設定 > Yubikey NEO系列選RAS 2048，Yubikey 4和5系列選RAS 4096，自行決定是否需要合法到期時間
![4](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/04.png)
3. OK > 下一個 > Create > 輸入金鑰保護密碼
![5](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/05.png)
4. 先直接完成，還不要備份
![6](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/06.png)
5. 複製 Key-ID
![7](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/07.png)
6. 開啟 cmd 輸入 `gpg --expert --edit-key <keyid>` Enter
![8](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/08.png)
7. 新增 Authenticate Key，輸入 `addkey` Enter，輸入 `8` Enter，輸入 `S` Enter，輸入 `E` Enter，輸入 `A` Enter
![9](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/09.png)
8. 輸入 `8` Enter，輸入金鑰大小，輸入期限如 `2y` Enter，輸入 `y` Enter，輸入 `y` Enter，輸入金鑰保護密碼，輸入 `save` Enter 儲存
![10](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/10.png)
9. 回到 Kleopatra ，對列表上的金鑰右鍵 > 匯出私密金鑰，並妥善備份
![11](https://blob.kgame.tw/blog/2019-04-07-yubikey-openpgp/11.png)

### 移動私鑰至 Yubikey

### 在新電腦載入金鑰
有兩種方法擇一即可
- 開啟 cmd 輸入 `gpg --card-edit` 再輸入 `fetch`
- 自行準備公鑰檔匯入 Kleopatra

### 從備份檔還私鑰原至 YubiKey
將備份私鑰的asc檔匯入 Kleopatra 後再次操作[移動私鑰至 Yubikey](#移動私鑰至-yubikey)

## 參考資料
- [Using Your YubiKey with OpenPGP](https://support.yubico.com/support/solutions/articles/15000006420-using-your-yubikey-with-openpgp)
