# Python asyncio

`async.py`

```python
import asyncio


async def ma(c):
    print("start", c)
    await asyncio.sleep(c)
    print("end", c)


async def doit():
    await asyncio.gather(*[ma(c) for c in [6, 5, 4, 3, 2, 1]])


def main():
    loop = asyncio.get_event_loop()
    loop.run_until_complete(doit())
    loop.close()


if __name__ == '__main__':
    main()
```

## Output:
```sh
$ python async.py
loop = asyncio.get_event_loop()
start 6
start 5
start 4
start 3
start 2
start 1
end 1
end 2
end 3
end 4
end 5
end 6
```
