# Subprocess Examples
<blockquote>
The subprocess module allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.
</blockquote>

This tutorial explains about general usage of the subprocess module. If you want to start this, write the test.py and follow the example codes. I hope you can be a master of the subprocess. enjoy.

The test file in order to tutorial:
``` python
import sys

if len(sys.argv) != 2:
    print("Usage: test.py [signature]")
    exit(1)

def hello_world():
    print("Hello, world!")

def ninetynine_bottles_of_beer():
    for i in range(99, -1, -1):
        if i == 0:
            print("No more bottles of beer on the wall, no more bottles of beer. ")
            print("Go to the store and buy some more, 99 bottles of beer on the wall.")
        elif i == 1:
            print("1 bottle of beer on the wall, 1 bottle of beer. ")
            print("Take one down and pass it around, no more bottles of beer on the wall. ")
        else:
            print("{0} bottles of beer on the wall, {0} bottles of beer. ".format(i))
            print("Take one down and pass it around, ", (i - 1), "bottles of beer on the wall. ")

def multiplication_table():
    for i in range(2, 10):
        for j in range(1, 10):
            print(f"{i} * {j} == {i * j}")
        print()


if sys.argv[1] == "-H":
    hello_world()
elif sys.argv[1] == "-99":
    ninetynine_bottles_of_beer()
elif sys.argv[1] == "-M":
    multiplication_table()
else:
    print(f"{sys.args[1]} is not defined.")
    exit(1)

exit(0)
```

Instance of subprocess:
``` python
import subprocess

completedProcess = subprocess.CompletedProcess(["fake", "*~*"], 1)
print(completedProcess)
```

Basic usage of run function:
``` python
import subprocess

completedProcess = subprocess.run(["python", "test.py", "-H"])
print(completedProcess)
```

Manipulate to subprocess output:
``` python
import subprocess

completedProcess = subprocess.run(["python", "test.py", "-M"])
print(completedProcess)

completedProcess = subprocess.run(["python", "test.py", "-M"], capture_output=False)
print(completedProcess)
```

The *timeout* argumanet and TimeoutExpired exception:
``` python
import subprocess

try:
    maybeYouCanNeverBe = subprocess.run(["python", "test.py", "-H"], timeout=0.01)
    print(maybeYouCanNeverBe)
except subprocess.TimeoutExpired:
    yeahRightImRight = subprocess.CompletedProcess(["TryAgainNot", "-~-"], 1)
    print(yeahRightImRight)
```
