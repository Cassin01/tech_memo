## Error
❯ sudo cabal install html-conduit http-conduit
Resolving dependencies...
cabal: Cannot build the executables in the package html-conduit because it
does not contain any executables. Check the .cabal file for the package and
make sure that it properly declares the components that you expect.
Cannot build the executables in the package http-conduit because it does not
contain any executables. Check the .cabal file for the package and make sure
that it properly declares the components that you expect.

## Solution

Just add `--lib`
❯ sudo cabal install --lib html-conduit http-conduit

[reference](https://github.com/haskell/cabal/issues/6246)
