# SafeDataBackup v1.0.0

### 高信頼・高機能なWindows向けバックアップアプリ

Python + Tkinter GUIの単一ファイルで動く、完全オフラインの安全なバックアップソリューションです。

- ✅ 完全オフライン / 外部送信なし
- ✅ VSSシャドウコピー対応 - 使用中ファイルも安全にバックアップ
- ✅ AES暗号化・重複排除・差分保存対応

**最新安定版：v1.0.0** | **単一ファイル版**

## ⬇ ダウンロード

[最新版 v1.0.0 をダウンロード]([https://github.com/Unknown777hello/SafeDataBackup/releases/tag/v1.0.0](https://github.com/Unknown777hello/SafeDataBackup/releases))

- Windows 10 / 11 (64bit) 対応
- インストーラー版 / ポータブル版あり（予定）
- インターネット接続不要

## 今回のアップデート (v1.0.0)
- 公開リリース版として `0.1.0` から `1.0.0` にバージョン更新
- トレイメニュー「最近の履歴」でトレイアイコンが停止する不具合を修正 - `functools.partial` への置換で `pystray` のシグネチャ検証に対応
- ウィンドウを閉じてもトレイに格納されない不具合を修正 - `TrayIcon.start()` の例外ハンドリングと二重起動防止ロジックを改善
- Zip Slip対策、復元前空き容量チェック、SHA-256復元後検証、分割アーカイブ全パート検証を追加

## 主な機能
- フル / 増分 / 差分バックアップ対応、世代管理・保持ポリシー
- VSSシャドウコピー対応 (Windows) - Outlookの.pstなどロック中ファイルも読取可能
- ローリングハッシュによるバイナリ差分保存 - 100MB以上の大容量ファイルは変更ブロックのみ保存
- 重複排除 (DedupStore) - 内容ハッシュで重複ファイルを1回だけ保存
- 分割アーカイブ - サイズ上限ごとに自動分割（既定2000MB）、全パート個別チェックサム検証
- クラッシュレジューム - 50件ごとにチェックポイント作成、電源断後も続きから再開
- Zip Slip (ディレクトリトラバーサル) 対策、復元後SHA-256検証、空き容量事前チェック
- AES暗号化 (pyzipper)、Argon2idマスターパスワード保護、OS資格情報ストア保存 (keyring)
- ランサムウェア対策 - カナリアファイル保護、大量リネーム検知、ソース消失保護
- システムトレイ常駐 (pystray)、二重起動防止、バイト数ベースの正確な進捗率・残り時間
- ドラッグ&ドロップ対応 (tkinterdnd2)、アーカイブ内容検索、スケジューラー内蔵、外部ミラー同期
- ダークモード (sv_ttk + darkdetect でOSテーマ自動追従)、ミニ進捗ウィンドウ、ディスクI/O自動調整 (psutil)
- 改ざん検知ログ、ログの個人情報マスキング (<HOME>/<USER>)、拡張長パス対応、ロック中ファイルのリトライ

## インストール方法
### インストーラー版（予定）
1. `SafeDataBackup_Setup.exe` をダウンロードして実行
2. 画面に従ってインストール
3. スタートメニューから起動

インストール後、以下のファイルがアプリフォルダに配置されます：
```
SafeDataBackup.exe
README.txt
LICENSE.md
THIRD-PARTY-LICENSES.txt
LICENSES/
app_icon.ico
```

### Python版 (v1.0.0)

```bash
# 推奨フルセット
pip install pyzipper pystray pillow tkinterdnd2 sv_ttk darkdetect argon2-cffi keyring psutil zstandard

# 実行
python SafeDataBackup.py

# バージョン確認
python SafeDataBackup.py --version
```

単一ファイルなので `SafeDataBackup.py` だけをUSBに入れて持ち運びも可能です。設定・履歴は同階層の `config.json` / `backup_history.json` に自動生成されます。

## 使い方
1. 対象フォルダを指定（ドラッグ&ドロップ対応）
2. 保存先を指定（分割保存は設定でON）
3. フル / 増分 / 差分を選択してバックアップ実行
4. 履歴から選択して復元（SHA-256検証オプションあり）
5. ウィンドウを閉じるとトレイに格納 - トレイメニューから「今すぐバックアップ」「最近の履歴」

## ライセンス

### 同梱ファイルについて
公開ZIP (SafeDataBackup_vX.X.X.zip) と Inno Setup インストーラー (SafeDataBackup_Setup.exe) には、以下のライセンスファイルが同梱されています。
- LICENSE.md : 自作コードのライセンス (SafeDataBackup License v1.0)
- THIRD-PARTY-LICENSES.txt : 第三者ライブラリのライセンス一覧
- LICENSES/ : 第三者ライセンス原文
- README.txt

### 自作コード
本プロジェクトの自作コードには、独自ライセンス「SafeDataBackup License v1.0」を適用します（MITではありません）。
Copyright (c) 2026 Unknown777hello (aka Unknown777)

主な条件（詳細は LICENSE.md を必ず確認）:
- 個人の非商用利用は無償・自由
- Python版は学習・レビュー目的の閲覧・実行を許可
- 改造版の再配布には事前許可が必要。Forkは学習・PR目的に限り自由
- 商用利用は要許可（紹介動画・ブログは収益化しても自由）
- 現状有姿で提供、法令の範囲内で免責

### 第三者ライブラリ
詳細は THIRD-PARTY-LICENSES.txt を参照
- pyzipper - MIT / BSD系 (AES暗号化)
- pystray / Pillow - LGPL-3.0 / HPND
- tkinterdnd2 - MIT
- sv_ttk - MIT
- darkdetect - BSD-3-Clause
- argon2-cffi - MIT
- keyring - MIT
- psutil - BSD-3-Clause
- zstandard - BSD-3-Clause
- Python標準ライブラリ - PSF License

## 要件
- Windows 10 / 11 (64bit) 推奨（VSSはWindowsのみ、基本機能はLinux/macOSでも動作）
- Python 3.10+ 推奨 (3.8+で動作)

## プライバシー
本アプリは完全オフラインで動作し、外部へのデータ送信は一切行いません。バックアップデータはすべてローカルに保存され、暗号化はローカルで完結します。詳細は PRIVACY.md をご覧ください。

注意：本ツールはご自身が所有・管理するデータ、または所有者から明確な許可を得た範囲でのみご使用ください。

## 作者
Unknown777hello (aka Unknown777)
Repository: https://github.com/Unknown777hello/SafeDataBackup


## ⚠️ 重要な注意事項

SafeDataBackupは、バックアップおよび復元を支援するためのソフトウェアです。

本ソフトウェアは可能な限り安全な処理および整合性確認を行いますが、ハードウェア障害、ストレージ障害、OSやファイルシステムの問題、予期しない電源断、ソフトウェア上の不具合、その他の原因によるデータ消失や復元不能を完全に防止するものではありません。

重要なデータについては、SafeDataBackupだけに依存せず、複数の保存先やバックアップ方法を併用することを推奨します。

「高信頼」「安全」といった表現は、絶対的なデータ保全を保証するものではありません。
