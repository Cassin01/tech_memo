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

## LSP

### rust-analyzer

[reference](https://rust-analyzer.github.io/manual.html#rust-analyzer-language-server-binary)


```sh
mkdir -p ~/.local/bin
$ curl -L https://github.com/rust-lang/rust-analyzer/releases/latest/download/rust-analyzer-x86_64-apple-darwin.gz | gunzip -c - > ~/.local/bin/rust-analyzer
$ chmod +x ~/.local/bin/rust-analyzer
```

# CUI Editor

- [helix](https://github.com/helix-editor/helix)
- [xi-editor](https://github.com/xi-editor/xi-editor)

# GUI Editor
- [text-editors-written-in-rust](https://github.com/flosse/text-editors-written-in-rust)

- [lite](https://github.com/rxi/lite)
- [CotEditor](https://github.com/coteditor/CotEditor)
- [lapce](https://github.com/lapce/lapce)
