---
title: Grid-world policy iteration
---

# Grid-world policy iteration

A more graphical way to understand how policy iteration functions (and other algorithms as well)  is through [this repo](https://github.com/rlcode/reinforcement-learning/) - see `1-grid-world/1-policy-iteration` that depicts a more elaborate gridworld. 

1. Clone the repo and launch VS Code in its root dir.  
2. Install the dependencies in a new VS Code terminal.

```bash
   python3 -m venv .venv
   source .venv/bin/activate
   pip3 install -r requirements.txt 
```

In VS Code click the Python debug button, click `create a launch.json file` and make sure that the launch configuration matches the one below (you need this for all visualizations to happen) 

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "cwd": "${fileDirname}"
        }
    ]
}
```

