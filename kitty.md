# kitty

## Tab:

New tab: ctrl + shift + t

Close tab: ctrl + shift + q

Next tab: ctrl + shift + right

Previous tab: ctrl + shift + left

## Window:

New window: ctrl + shift + enter

Close window: ctrl + shift + w

Next window: ctrl + shift + ]

Previous window: ctrl + shift + [

F5: vsplit

F6: split

F7: rotate

## How to send keys to neovim

### metakeys

macos_option_as_alt yes

### ctrl+i

- [kitty keyboard-protocol](https://sw.kovidgoyal.net/kitty/keyboard-protocol/)
- [keycodes](http://www.leonerd.org.uk/hacks/fixterms/)
- vim document: `:h tui-input`

```
map ctrl+i send_text normal,application \x1b[73;5u
```

