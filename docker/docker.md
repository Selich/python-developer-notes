### Docker



#### https://www.youtube.com/watch?v=BdxdRlTnPEE
why I use RUN + a colon in a dockerfile with multiple commands

```bash
RUN : \
    && ... \
    && :
```

For example:
If we want to add another requiremnets requirements-dev.txt
```bash
FROM ubuntu:focal

#...

# First example
RUN :  \
    && virtualenv /venv -p python3 \
    && /venv/bin/pip install -r requirements.txt \
    && /venv/bin/pip install -r requirents-dev.txt \
    && :

# Second example
RUN  virtualenv /venv -p python3 && \
    /venv/bin/pip install -r requirements.txt && \
    /venv/bin/pip install -r requirents-dev.txt

```
In the first example we only need to add one line, which is different to the number of changes in the secound example, three.

":" is a shell builtin.
No effect; the command does nothing beyond exapnding arguments and performing any specified redirections. The return status is zero.
```bash
:
```





