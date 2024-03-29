[![LICENSE](https://img.shields.io/pypi/l/async-cleverbot.svg)](https://img.shields.io/pypi/l/async-cleverbot.svg)
[![Downloads](https://img.shields.io/pypi/dd/async-cleverbot.svg)](https://img.shields.io/pypi/dd/async-cleverbot.svg)
[![Python](https://img.shields.io/pypi/pyversions/async-cleverbot.svg)](https://img.shields.io/pypi/pyversions/async-cleverbot.svg)

# async_cleverbot
Asyncio API wrapper for the Travitia Cleverbot API. (https://public-api.travitia.xyz/talk)

# Installation

## Installing with `pip` from PyPI
`pip install -U async_cleverbot`

## Installing with `pip` + `git` from GitHub
`pip install -U git+https://github.com/TheRealchr1s/async-cleverbot`

# Usage
```python
import async_cleverbot as ac

cleverbot = ac.Cleverbot("Your API key here") # Create the Cleverbot client
response = await cleverbot.ask("How are you today?") # Ask a question, returns async_cleverbot.cleverbot.Response
print(response.text) # Text from the Response object
await cleverbot.close()
```

# Getting an API key
Join the [Travitia API Discord server](https://discord.gg/C98nsXt) and use the `> api` command to request an API key.
![Getting a key](https://i.imgur.com/cUJsM3i.png "Getting a key")

# Using context
### This API supports a context parameter for background context, so let's make use of it!
```python
import async_cleverbot as ac

cleverbot = ac.Cleverbot("Your API key here", ac.DictContext())

response = await cleverbot.ask("How are you today?", 246938839720001536) # 2nd param is an identifier, this can be a user id!
print(response.text)

response = await cleverbot.ask("I'm doing good too.", 246938839720001536)
print(response.text)
print(cleverbot.context._storage) # "How are you today?" - returns most recent previous queries
await cleverbot.close()
```

# New in 0.2.1: Emotions
This wrapper's API now supports selecting an emotion to influence its response.  
You can specify a custom emotion using the enum `async_cleverbot.Emotion`.  
(The default emotion is `Emotion.neutral`)

## Supported emotions:
`async_cleverbot.Emotion.neutral/normal` - Neutral response  
`async_cleverbot.Emotion.sad/sadness` - Sad response  
`async_cleverbot.Emotion.fear/scared` - Fearful response  
`async_cleverbot.Emotion.joy/happy` - Excited response  
`async_cleverbot.Emotion.anger/angry` - Angry response

## An example
```python
import async_cleverbot as ac

cleverbot = ac.Cleverbot("Your API key here")
resp = await cleverbot.ask("What's up?", emotion=ac.Emotion.joy)
print(resp.text)
```

# New in 0.2.2: Custom sessions, simpler context
## You can now pass context and your own session when creating a cleverbot client.
```python
import async_cleverbot as ac

cleverbot = ac.Cleverbot("Your API key here", session=my_aiohttp_sess, context=ac.DictContext())
```
## In addition, DictContext no longer needs an argument.
The argument has been preserved for backwards compatibility.
