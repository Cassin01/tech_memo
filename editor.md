```yaml
title: Editor
date: 2022-09-16
categories: [programming, text editor]
tags: [editor]
```

# Helix

## Installation

```sh
git clone https://github.com/helix-editor/helix
cd helix
cargo install --path helix-term
ln -s $PWD/runtime ~/.config/helix/runtime
```

- バイナリ: `$HOME/.cargo/bin`
- コマンド: `hx`

## ドキュメント

[ドキュメント](https://docs.helix-editor.com)

## Configuration

- 場所: `~/.config/helix/config.toml`
- テーマ: `~/.config/helix/themes/*`
