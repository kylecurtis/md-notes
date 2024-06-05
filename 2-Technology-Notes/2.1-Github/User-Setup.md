---
tags: [git]
---


<br>

---

<br>

## Username and Email

<br>

#### Username

```bash
git config --global user.name "<YOUR NAME>"
```

<br>

#### Email

```bash
git config --global user.email "<YOUR EMAIL>"
```

<br>

---

<br>

## Long path Support

Enable long path support to prevent issues with deep directory structures.

<br>

```bash
git config --global core.longpaths true
```

<br>

---

<br>

## Default Pull Behavior


```bash
git config --global pull.rebase false
```

<br>

---

<br>

## GPG Signing

<br>

#### Set GPG Executable Path

```bash
git config --global gpg.program "C:/Program Files (x86)/GnuPG/bin/gpg.exe"
```

<br>

#### Get the GPG Key ID

```bash
gpg --list-secret-keys --keyid-format LONG
```

<br>

#### Set the GPG Key

```bash
git config --global user.signingkey "<KEY>"
```

<br>

#### Automatic Signing

```bash
git config --global commit.gpgsign true
```

<br>

---

<br>