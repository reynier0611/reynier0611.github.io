## Profiling python code
[Back to table of Contents](../README.md)

If you run your code nominally as ```python myscript.py```, you can profile this code to see which parts of the code take longer to run by following a couple of simple steps. First, run the code as ```python -m cProfile -o out.profile myscript.py``` instead. This produces a file called ```out.profile```. Then, install snakeviz: ```pip install snakeviz```. Finally, run: ```snakeviz out.profile```. This opens a page in your default value with an onion-shell interactive diagram that describes which functions take most of the run time.

<img src="https://github.com/reynier0611/personal_notes/blob/master/misc/snakeviz.jpg"
    style="width: 50%;"
    alt="snakeviz"
    style="float: left; margin-right: 10px;" />
