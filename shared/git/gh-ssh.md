# GitHub SSH

Linux (bash)

## Global configuration

### Create config dir

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

### Generate auth key

```bash
ssh-keygen -t ed25519 \
  -f ~/.ssh/github-com.key \
  -C "$USER@$(uname -n)"
```

```bash
# X11
xclip -selection clipboard -r < ~/.ssh/github-com.key.pub
# Wayland
wl-copy --trim-newline < ~/.ssh/github-com.key.pub
```

### Enable config

```bash
cat >> ~/.ssh/config <<'EOF'
Host github.com
    User git
    Port 22
    IdentityFile ~/.ssh/github-com.key
    IdentitiesOnly yes
    PreferredAuthentications publickey
    PasswordAuthentication no
EOF

chmod 600 ~/.ssh/config
```

### Generate sign key

```bash
ssh-keygen -t ed25519 \
  -f ~/.ssh/github-com.sign.key \
  -C "$USER@$(uname -n)"
```

```bash
# X11
xclip -selection clipboard -r < ~/.ssh/github-com.sign.key.pub
# Wayland
wl-copy --trim-newline < ~/.ssh/github-com.sign.key.pub
```

### Set default branch

```bash
git config --global init.defaultBranch main
```

### Configure lineending settings

```bash
git config --global core.autocrlf false
git config --global core.eol lf
```

## Setup repository

### New

```bash
git init
```

### Config

```bash
git config user.name 'yotlich'
git config user.email '149834513+yotlich@users.noreply.github.com'
git config gpg.format ssh
git config user.signingKey ~/.ssh/github-com.sign.key.pub
git config commit.gpgSign true
git config tag.gpgSign true
```

### Add remote

```bash
git remote add origin git@github.com:yotlich/
```
