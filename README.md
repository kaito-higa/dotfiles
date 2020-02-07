# dotfiles


## usage

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/kaito-higa/dotfiles/master/bootstrap.sh)"
```

インストールするとhttpsでcloneされるためパスワード入力が必要となります。  
ノンパスのsshに変更したい場合は下記を実行してください。  

```
cd $DOTFILES_PATH
git remote set-url origin $(git config --get remote.origin.url | sed -e "s/https:\/\/github\.com\//git@github.com:/g")
```


## 更新時

Brewfileやdotfileを追加した場合など、下記を実行して反映させます。  

```
$DOTFILES_PATH/bootstrap.sh
```


## 個人のgithubプロジェクトにdotfilesを持っていない方の作業

### 個人のgithubプロジェクトにdotfilesを作成する手順
個人のgithubプロジェクトに本リポジトリをpublic権限で作成します。  
理由は、curl + bootstrapでセットアップできるようにと、github actionsを使っているため。  

> *リポジトリには、パスワード文字列やシークレットファイルや.ssh/configなど  
> セキュリティ問題に繋がりそうなものは絶対にコミットしないでください。*  

本作業を行うためにはssh agentができgitのnameとemailが設定されていることが前提です。

```
# 個人リポジトリに追加まで
cd $HOME
git clone git@github.com:switch-m/dotfiles.git
cd dotfiles
rm -rf .git
git init
git add .
git commit -m "first commit"
git remote add origin git@github.com:GITHUB_USERNAME/dotfiles.git
git push -u origin master
```

README.md と bootstrap.sh の switch-m/dotfiles を GITHUB_USERNAME/dotfiles に変更しcommit & pushしてください。  

### switch-m/dotfilesを上流ブランチ設定し取り込む方法

switch-m/dotfilesに更新が入るため落ち着くまでは、取り込めるようにする。  

```
git remote add upstream git@github.com:switch-m/dotfiles.git

git pull upstream master
```
