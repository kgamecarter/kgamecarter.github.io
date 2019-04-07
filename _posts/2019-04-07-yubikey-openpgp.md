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
  teaser: /assets/images/yubikey-openpgp-1.png
  og_image: /assets/images/yubikey-openpgp-1.png
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
### 建立金鑰對及備份私鑰
1. 開啟 Kleopatra > 工具(T) > Manage Smartcards
![/yubikey-openpgp-1](/assets/images/yubikey-openpgp-1.png)
2. 修改 Cardholder 成自己的名字
3. 使用 Change PIN 修改 PIN 碼，預設值 123456
4. 使用 Change Admin PIN 修改管理 PIN 碼，預設值 12345678
5. 使用 Generate new Keys 產生新的金鑰對，Yubikey NEO系列選RAS 2048，Yubikey 4和5系列選RAS 4096
6. 輸入Name和Email，選擇要備份私鑰
7. 經過漫長的寫入私鑰後，輸入保護私鑰的密碼就可以儲存私鑰備份檔
8. 將公鑰資訊送到 Public key server，或是 Keybase 上使用
9. 將公鑰網址設定進 Smartcard 的 Pubkey URL

### 在新電腦載入金鑰
有兩種方法擇一即可
- 開啟 cmd 輸入 `gpg --card-edit <keyid>` 再輸入 `fetch`
- 自行準備公鑰檔匯入 Kleopatra

### 從備份檔還私鑰原至 YubiKey
1. 開啟 cmd 輸入 `gpg --card-edit <keyid>`
2. 輸入 `bkuptocard sk_<id>.gpg`

## 參考資料
- [Using Your YubiKey with OpenPGP](https://support.yubico.com/support/solutions/articles/15000006420-using-your-yubikey-with-openpgp)
- [How to import backed up](https://support.nitrokey.com/t/how-to-import-backed-up-encryption-key-sk-id-gpg/868)
