# MacOS Catalina setup.
> Includes package mgmt (brew), dotfiles, mac system config changes, installing packages, setting up git with pgp.
> Last is recommended apps I use on my mac.

 Setup of a new mac, including all dotfiles and dev related tools. Also a big list of mac apps I have installed and what they do.

## 1. Install brew

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## 2. Install deps

```sh
git clone https://github.com/woodrowpearson/macOS-setup.git
cd macOS-setup/

# edit Brewfile to remove/add things
brew bundle
```

## 3. Install dotfiles

```sh
git clone https://github.com/woodrowpearson/dotfiles.git ~/.dotfiles
cd ~/.dotfiles
./script/bootstrap
zsh # reload zsh
```

MacOS defaults I've found from others dotfiles. I don't use most of them but for posterity I have added them:

```console
./macos/set-defaults
```

## 4. Setup SSH keys

Create a new SSH key or copy the previous one into `~/.ssh`. That should be
it.

```console
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Also fix perms:

```console
$ chmod 0600 ~/.ssh/id_rsa
```

## 5. Setup GPG signing

Create default config files:

```console
gpg --list-keys
```

Setup pinentry:

```console
$ brew install pinentry-mac
$ echo "pinentry-program /usr/local/bin/pinentry-mac" >> ~/.gnupg/gpg-agent.conf
$ killall gpg-agent
```

Import the key:

```console
$ export GPG_TTY=$(tty)
$ keybase pgp export -q C14AB940 | gpg --import
$ keybase pgp export -q C14AB940 --secret | gpg --import --allow-secret-key-import
```

> Change C14AB940 with your key id.

Setup git:

```console
$ git config --global gpg.program $(which gpg)
$ git config --global user.signingkey C14AB940
$ git config --global commit.gpgsign true
```

> Change C14AB940 with your key id.

Test it:

```console
$ mkdir -p /tmp/test
$ cd $_
$ git init
$ git commit --allow-empty -m 'signsss'
$ git log --show-signature
```

That's it!


## 6. Reboot

```console
sudo reboot
```

# MacOS Apps that I love. Some of these were installed when we ran `Brew update`.

- [iTerm](https://www.iterm2.com/): a better terminal emulator; Currently have been using prezto but will be moving over to antibody as it seems to growing choice among zsh users.
- [Alfred](https://www.alfredapp.com/): Alfred is a powerful launcher that you can program to show anything you want. Search local and web at the same time for example
- [2Do](http://www.2doapp.com/mac) - Flexible task manager
- [Typinator](http://www.ergonis.com/products/typinator/) - Text expansions
- [PDF Expert](https://pdfexpert.com/) - PDF reader/editor
- [Clockify](https://clockify.me/) - Free app that tracks your time spent. useful for personal or professional tracking (freelance, contract)
- [Annotate](https://itunes.apple.com/us/app/annotate-capture-screenshot/id918207447?mt=12) - Create and annotate screenshots
- [Little Snitch](https://www.obdev.at/products/littlesnitch/index.html) - Control incoming/outgoing network traffic
- [qBittorrent](https://www.qbittorrent.org/) - Opensource alternative to utorrent
- [Screen](https://screen.so/#/home) - Fast, free, screen sharing with multiple user control, drawing, and recording.
- [Mind Node](https://mindnode.com) - Interactive Mind Mapping. Visually expand upon ideas you have
- [VS Code](https://github.com/Microsoft/vscode) - Code editor
- [Dash](https://kapeli.com/dash) - API Documentation Browser
- [Hazel](https://www.noodlesoft.com) - Automated File Organization
- [GPG Suite](https://gpgtools.org/) - Encrypt, decrypt, sign and verify files or messages.

