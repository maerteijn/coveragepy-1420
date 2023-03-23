# coveragepy-1420
A demonstration of issue [#1420](https://github.com/nedbat/coveragepy/issues/1420)


## How to test the issue

```bash
pip install -r requirements.txt
pytest --cov=my_module.py
```
This installs coverage version `6.4.1`. You'll see that the breakpoint is two lines "too late":

```shell
============================================================================================= test session starts ==============================================================================================
platform darwin -- Python 3.9.13, pytest-7.1.3, pluggy-1.0.0
rootdir: /Users/martijn/Dev/oss/coveragepy-1420
plugins: cov-3.0.0
collected 1 item

test_breakpoint_example.py
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>> PDB set_trace (IO-capturing turned off) >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
Just after the breakpoint
--Return--
> /Users/martijn/Dev/oss/coveragepy-1420/my_module.py(5)my_function()->True
-> return True
```

Now install version `6.4.0`:

```bash
pip install "coverage==6.4.0"
pytest --cov=my_module.py
```

The breakpoint is on the correct line:

```shell
============================================================================================= test session starts ==============================================================================================
platform darwin -- Python 3.9.13, pytest-7.1.3, pluggy-1.0.0
rootdir: /Users/martijn/Dev/oss/coveragepy-1420
plugins: cov-3.0.0
collected 1 item

test_breakpoint_example.py
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>> PDB set_trace (IO-capturing turned off) >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
> /Users/martijn/Dev/oss/coveragepy-1420/my_module.py(4)my_function()
-> print("Just after the breakpoint")
```
