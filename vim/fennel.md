# fennel

## set up

Makefile

```make
all: lua/showmarks.lua lua/mapinfo.lua lua/init.lua

lua/%.lua: fnl/%.fnl
	fennel --compile $< > $@
```

トランスパイルされる.
