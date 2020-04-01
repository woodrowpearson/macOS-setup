# MacOS Catalina setup.
> Includes package mgmt (brew), dotfiles, mac system config changes, installing packages, setting up git with pgp.
> Last is recommended apps I use on my mac.

 Setup of a new mac, including all dotfiles and dev related tools. Also a big list of mac apps I have installed and what they do.

## Step 0: Install Xcode from the app store.j

## Step 1: Install Mac packages and deps

###  Install brew

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Install deps

```sh
git clone https://github.com/woodrowpearson/macOS-setup.git
cd macOS-setup/

# edit Brewfile to remove/add things then run command:
brew bundle
```

## Step 2: Install dotfiles

```sh
git clone https://github.com/woodrowpearson/dotfiles.git ~/.dotfiles
cd ~/.dotfiles
./script/bootstrap
zsh # reload zsh
```


## Step 3: Change MacOS system configurations

## Step 4:  Setup tools, security, & identity for development

### Generate SSH Key
Create a new SSH key or copy an existing  one into `~/.ssh`.

```console
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```



# Set permissions
```console
$ chmod 0600 ~/.ssh/id_rsa
```

> Make sure the permissions are set correctly for the key.
> .rw-------

## 5. Setup GPG signing

> We need to create the gpg conf file
```console
touch ~/.gnupg/gpg-agent.conf
```

> Create your gpg key & verify it.
```console
gpg --full-generate-key

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
$ keybase pgp export -q yourkeyHERE | gpg --import
$ keybase pgp export -q yourkeyHERE --secret | gpg --import --allow-secret-key-import
```

> If you don't know your key `gpg --list-keys`

Setup git:

```console
$ git config --global gpg.program $(which gpg)
$ git config --global user.signingkey yourkeyHERE
$ git config --global commit.gpgsign true
```

Test it:

```console
$ mkdir -p /tmp/test
$ cd $_
$ git init
$ git commit --allow-empty -m 'fooo barrr'
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
- [Dash](https://kapeli.com/dash) - API Documentation Browser
- [Hazel](https://www.noodlesoft.com) - Automated File Organization
- [GPG Suite](https://gpgtools.org/) - Encrypt, decrypt, sign and verify files or messages.
- [Pycharm IDE](https://www.jetbrains.com/pycharm/) - Great IDE if vim isn't
  cutting it.
