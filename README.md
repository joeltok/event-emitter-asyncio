# event-emitter-asyncio

Super simple event emitter in Python 3, built with asyncio. No decorators required. Built around a subset of the NodeJS [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter) API. 

A full write up and explanation for how this module works can be found [here](https://joeltok.com/blog/2021-3/building-an-event-bus-in-python).

## Usage

```python
from event_emitter_asyncio.EventEmitter import EventEmitter
event_emitter = EventEmitter()

async def func(event):
  for pet in event['pets']:
    print(pet)
  
event_data = {
  'pets': ['cats', 'dogs']  
}
event_emitter.add_listener('some-event', func)
event_emitter.emit('some-event', event_data)
event_emitter.remove_listener('some-event', func)
```

This will give:
```sh
> cats
> dogs
```

## Using this repo

### Development

```sh
git clone git@github.com:joeltok/py-event-bus.git
cd ./py-event-bus
python3 -m venv ./venv
source venv/bin/activate
pip3 install pytest
pip3 install pytest-asyncio
```

### Testing 

```sh
python3 -m pytest src/py-event-bus/
```

### Packaging

```sh
source venv/bin/activate
python3 -m pip install --upgrade build
python3 -m pip install --upgrade twine
```

```sh
python3 -m build
twine upload dist/*
```