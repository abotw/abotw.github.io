---
layout: post
title:  "使用 Github Pages 搭建博客"
---

# 使用 Github Pages 搭建博客

## Quicklinks

- [Github Pages](https://pages.github.com/)
- [Jekyll](https://jekyllrb.com/docs/)（[Github](https://github.com/jekyll/jekyll)）
-  ✅ [Why You Shouldn't Use the System Ruby to Install Gems on a Mac](https://www.moncefbelyamani.com/why-you-shouldn-t-use-the-system-ruby-to-install-gems-on-a-mac/)
- [chruby](https://github.com/postmodern/chruby)
- [Home Is Where the Heart Is](https://www.moncefbelyamani.com/home-is-where-the-heart-is/)
- [5 Ways to Read and Edit Hidden Files or Dotfiles on Your Mac](https://www.moncefbelyamani.com/5-ways-to-open-hidden-files-on-your-mac/)

## Step 1: Github Pages

```bash
# After creating the repo.
cd ~
git clone git@github.com:abotw/abotw.github.io.git
cd abotw.github.io
echo "This is abotw" > index.html
git add --all
git commit -m "Initial commit"
git push -u origin main
```

:warning: 记得使用 ssh 协议而不是 https 协议，否则 `git push` 的时候可能会出现以下错误：

```bash
# git clone https://github.com/abotw/abotw.github.io.git
# ..
# git push -u origin main

Username for 'https://github.com': abotw
Password for 'https://abotw@github.com':
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
fatal: Authentication failed for 'https://github.com/abotw/abotw.github.io/'
```

## Step 2: Jekyll

### Step 2.1: Install Ruby

* [Installation](https://jekyllrb.com/docs/installation/)

*  ✅ [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/)

- :ballot_box_with_check: [The fastest and easiest way to install Ruby on a Mac in 2023](https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/)
  [Step3](https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/#step-3-install-a-gem) 以下的暂时不需要看

```bash
brew install chruby ruby-install
ruby-install ruby 3.1.3
```

Configure the shell: 

```bash
# echo $(brew --prefix) => /opt/homebrew
echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
echo "chruby ruby-3.1.3" >> ~/.zshrc # run 'chruby' to see actual version
```

```bash
ruby -v
ruby 3.1.3p185 (2022-11-24 revision 1a6b16756e) [arm64-darwin22] #🎉
```

#### 2.1.1 查看是否已经安装 homebrew

```bash
ls /usr/local
ls /opt/homebrew # If you’re on a Mac with the Apple Silicon chip (M1/M2)
```

![image-20230310151033230](./assets/image-20230310151033230.png)

#### 2.1.2 查看当前的系统架构

```bash
# uname
# Print details about the current machine and the operating system running on it.

# To print the hardware instruction set:
uname -m
arm64 # if you’re on an Apple Silicon Mac
```

### Step 2.2 Install Jekyll

- [Why You Should Never Use sudo to Install Ruby Gems](https://www.moncefbelyamani.com/why-you-should-never-use-sudo-to-install-ruby-gems/)

```bash
gem install jekyll
gem install bundler
# OR `gem install jekyll bundler`
```

### Steps 2.3 Others

-  ✅ [Quickstart](https://jekyllrb.com/docs/)

```bash
jekyll new blog
cd blog
bundle exec jekyll serve --livereload # Pass the --livereload option to serve to automatically refresh the page with each change you make to the source files
# => Now browse to `http://localhost:4000` = `http://127.0.0.1:4000/`
```

* `127.0.0.1` = `localhost`

## Step 3: Deploy

- [Creating a GitHub Pages site with Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

## Others

### 1. find out the shell you are using

*  ✅ [Which Shell Am I Using? How Can I Switch?](https://www.moncefbelyamani.com/which-shell-am-i-using-how-can-i-switch/)

#### methods

```bash
echo $0 #-zsh
monfresh #zsh: command not found: monfresh
```

#### the configuration file

| shell | /path/to/the/configuration/file       | /path/to/the/shell |
| ----- | ------------------------------------- | ------------------ |
| zsh   | `~/.zshrc`                            | `/bin/zsh`         |
| bash  | `~/.bash_profile` NOT ~~`~/.bashrc`~~ | `/bin/bash`        |

### 2. change shells: `chsh`

```bash
# chsh
# Change user's login shell.

# Set a specific login shell for the current user interactively:
chsh

# [l]ist available shells:
chsh -l

# Set a specific login [s]hell for the current user:
chsh -s path/to/shell
```

### 3. find out the path to a shell

```bash
which SHELLNAME
```

### 4. `$()`

![image-20230310143010916](./assets/image-20230310143010916.png)

### 5. `/etc/shells` - macOS

![image-20230310143505507](./assets/image-20230310143505507.png)

### 6. system ruby on Ventura (macOS 13.x)

```bash
ruby -v
ruby 2.6.10p210 (2022-04-12 revision 67958) [universal.arm64e-darwin22]
# 2.6.10
```



