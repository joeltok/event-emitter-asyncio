# Event Emitter (asyncio)

Super simple event emitter in Python 3, built with asyncio. No decorators required. Built around a subset of the NodeJS [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter) API. 

A full write up and explanation for how this module works can be found [here](https://joeltok.com/blog/2021-3/building-an-event-bus-in-python).

## Installation

```sh
pip install event_emitter_asyncio
```

## Usage (Working example)

```py
import asyncio

from event_emitter_asyncio.EventEmitter import EventEmitter
event_emitter = EventEmitter()

async def run():
  # add a listener
  async def func(event):
    for pet in event['pets']:
      print(pet)
  event_emitter.add_listener('some-event', func)

  # emit an event every second for 3 seconds
  n = 0
  while n < 3:
    event_data = { 'pets': ['cats', 'dogs'] }
    event_emitter.emit('some-event', event_data)
    await asyncio.sleep(1)
    n += 1

  # remove the listener
  event_emitter.remove_listener('some-event', func)

loop = asyncio.get_event_loop()
loop.run_until_complete(run())
```

This will give:
```sh
> cats
> dogs
> cats
> dogs
> cats
> dogs
```

## Developing on this repo

### Development

```sh
git clone git@github.com:joeltok/event-emitter-asyncio.git
cd ./event-emitter-asyncio
python3 -m venv ./venv
source venv/bin/activate
pip3 install pytest
pip3 install pytest-asyncio
```

### Testing 

```sh
python3 -m pytest src/event_emitter_asyncio/
```

### Packaging

```sh
source venv/bin/activate
python3 -m pip install --upgrade build
python3 -m pip install --upgrade twine
```

```sh
rm -rf dist && python3 -m build
twine upload dist/*
```