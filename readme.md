# Overview
Expy is an easy-but-powerful psychology experiment builder. It's designed for psycholinguistic experiment, but also be suitable for any other visual or auditory experiments.

[![PyPI Version][pypi-v-image]][pypi-v-link]
[Document](http://expy.readthedocs.io/en/latest/)

[pypi-v-image]: https://img.shields.io/pypi/v/expy.png
[pypi-v-link]: https://pypi.python.org/pypi/expy
---
# Simple example

```python
# coding:utf-8
from expy import * # Import the needed functions
start() # Initiate the experiment environment

# An RSPV demo
for w in 'ABCDE12345':
    drawWord(w) # Draw something on the canvas(not the screen)
    show(200) # Show the content of current canvas on the screen, and keep for 200ms
```

---
# Cookbook
## *Experiment Structure*
A standard experiment contains 3 levels:
- Run(Session)
- Block
- Trial
So we suggest that your code should have hierarchical structure, as the example below：
```python
def trial(stim):
    draw(stim)
    show(1000)

def block(trialList):
    for stim in trialList:
        trial(stim)

def run():
    for trialList in blockList:
        block(trialList)

run()
```
## *Visual Experiment*
```python
from expy import * # Import the needed functions
start() # Initiate the experiment environment

name = getInput('Please enter your name:')

setting = readSetting()
introduction(setting['introduction1'])

tip(name+', Are you ready?')

def trial(word,pos):
    drawWord('+')
    show(500)

    drawWord(word,x=pos) # Draw text on the canvas
    show()
    key = waitForEvent({K_f:'Left',K_j:'Right'}) # Waiting for pressing 'F' or 'J'
    if key==word:
        alertAndGo('Correct!',1000)
    else:
        alertAndGo('Wrong!',1000)
    show(500)

alertAndGo('The experiment will start after 3s.')
stimuli = [('Left',-0.5),
            ('Right',0.5),
            ('Right',-0.5),
            ('Left',0.5),
            ('Left',-0.5),
            ('Right',-0.5)]
for word,pos in stimuli:
    trial(word,pos)

alertAndQuit('Done!')
```
## *Auditory Experiment*
todo
