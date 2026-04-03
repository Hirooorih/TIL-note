# Gitの基本

## 今日学んだこと
- `git clone` : リモートリポジトリをローカルにコピーする
- `git checkout -b` : 新しいブランチを作成して移動する
- `git add` : 変更をステージングする
- `git commit` : 変更を記録する
- `git push` : リモートに送信する

## その他
- GitHubに公開鍵を登録する
GitHub → 右上のアイコン → Settings
左メニュー → SSH and GPG keys
New SSH key をクリック
Title（任意の名前）を入力し、Keyにコピーした公開鍵を貼り付け
Add SSH key をクリック

- 接続確認
bashssh -T git@github.com
Hi <username>! You've successfully authenticated... と表示されれば成功です。

- トラブルシューティング
Git for WindowsのSSHの場所を特定
Get-ChildItem "C:\Program Files\Git" -Recurse -Filter "ssh.exe" 2>$null

git config --global core.sshCommand "C:/Program Files/Git/usr/bin/ssh.exe"

IdentityFileを明示的に指定する
`C:\Users\hnaru\.ssh\config` に以下を追記してください：
```
Host github.com
    HostName github.com
    User git
    IdentityFile C:/Users/hnaru/.ssh/id_ed25519

GitのSSHをWindows OpenSSHに戻す
git config --global core.sshCommand "C:/Windows/System32/OpenSSH/ssh.exe"   

# まず現在の設定を確認
git config --global core.sshCommand

# ログ付きでclone
$env:GIT_SSH_COMMAND="C:/Windows/System32/OpenSSH/ssh.exe -v"
git clone git@github.com:Hirooorih/TIL-note.git

- Repository設定の推奨
基本設定
項目推奨設定理由Repository name TIL-note そのままでOK
Description 📝 Today I Learned - 日々の学びメモあると見やすい
Visibility Public 練習はPublicが後で見返しやすい（Privateでも可）

- 初期化オプション（重要！）
項目推奨設定理由✅ Add a README file チェックする これがないと最初のpullで手間がかかる
.gitignore None でOK テキストファイルなら不要
License None でOK 個人練習なので不要

- ⚠️ 一番大事なポイント
「Add a README file」は必ずチェック！
これをチェックすることで：

リポジトリが空にならない（mainブランチが最初から存在する）
ローカルで git clone してすぐ作業開始できる
最初の git pull がスムーズにできる

チェックしないと、最初のpushで少し複雑なコマンドが必要になります。