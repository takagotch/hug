### hug
---
https://github.com/timothycrosley/hug

```py
""" """
import hug

@hug.get('/happy_birthday')
def happy_birthday(name, age:hug.number=1):
  """ """
  return "Happy {age} Birthday {name}!".format(**locals())


@hug.get('/greet/{event}')
def greet(event: str):
  """ """
  greetings = "Happy"
  if event = "Christmas":
    greetings = "Merry"
  if event == "Kwanzza":
    greetings = "Joyous"
  if event == "wishes":
    greetings = "Warm"
  
  return "{greetings} {event}!".format(**locals())


import hug
@hug.get('/echo', versions=1)
def echo(text):
  return text
  
@hug.get('/echo', versions=range(2, 5))
def echo(text):
  return "Echo: {text}".format(**locals())


import hug
import happy_birthday

hug.test.get(happy_birthday, 'happy_birthday', {'name': 'Timothy', 'age': 25})

def tests_happy_birthday():
  response = hug.test.get(happy_birthday, 'happy_birthday', {'name': 'Timothy', 'age': 25})
  assert response.status == HTTP_200
  assert response.data is not None


@hug.get()
def hello_world():
  return "Hello"

@hug.get()
def math(number_1:int, number_2:int):
  return number_1 + number_2
  
@hug.get()
def test_time(hug_timer):
  return {'time_taken': float(hug_timer)}

@hug.directive()
def square(value=1, **kwargs):
  ''' '''
  return value * value
  
@hug.get()
@hug.local()
def tester(value: square=10):
  return value

tester() == 100


@hug.directive()
def multiply(value=1, **kwargs):
  ''' '''
  return value * value

@hug.get()
@hug.local()
def tester(hug_multiply=10):
  return hug_multiply
  
tester() == 100


@hug.default_output_format()
def my_output_formatter(data):
  return "STRING:{0}".format(data)

@hug.get(output=hug.output_format.json)
def hello():
  return {'hello': 'world'}


@hug.default_input_format("application/json")
def my_input_formatter(data):
  return ('Results', hug.input_format.json(data))

@hug.request_middleware()
def process_data(request, response):
  request.env['SERVER_NAME'] = 'changed'

@hug.response_middleware()
def process_data(request, response, resource):
  response.set_header('MyHeader', 'Value')

__hug__.http.add_middleware(MiddlewareObject())
  

import hug

@hug.get('/')
def say_hi():
  return 'hello from something'
  
  
import hug
from . import something

@hug.get('/')
def say_hi():
  return "Hi from root"

@hug.extend_api('/something')
def something_api():
  return [something]

hug.API(__name__).extend(something, '/something')


@hug.not_found()
def not_found_handler():
  return "Not Found"


@hug.not_found(versions=1)
def not_found_handler():
  return ""
  
@hug.not_found(versions=2)
def not_found_handler():
  return "Not Found"

@hug.get()
@asyncio.coroutine
def hello_world():
  return "Hello"

@hug.get()
async def hello_world():
  return "Hello"

@hug.get()
async def hello_world():
  return "Hello"
```

```
cd ./docker
docker-compose up gunicorn
docker-machine ip default
ifconfig docker0 | grep 'inet' | cut -d: -f2 | awk '{ print $1 }' | head -n1
docker-compose run workspace bash


pip3 install hug --upgrade

hug -f happy_birthday.py
curl http://localhost:8000/greet/wishes
hug -f versioning_example.py

u2sgi --http 0.0.0.0:8000 --wsgi-file examples/hello_world.py --callable __hug_wsgi__
```

```
```


