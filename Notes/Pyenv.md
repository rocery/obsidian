Install:
```
$ curl -fsSL https://pyenv.run | bash
```
Check available python version:
```
pyenv install --list
pyenv install --list | grep -E ' 3\.([1-9][0-9]+)'
```
Install custom python version:
```
pyenv install 3.13.15
```
Install custom python in local folder:
```
pyenv local 3.13.15
```

Install virtualenv:
```
git clone https://github.com/pyenv/pyenv-virtualenv.git (pyenv root)/plugins/pyenv-virtualenv
Then restart shell:
exec "$SHELL"
```
How to make virtualenv:
```
pyenv virtualenv 3.13.15 venv3.13.15
```
Activate:
```
pyenv activate <name>
pyenv deactivate
```