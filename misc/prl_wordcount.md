## PRL word count
[Back to table of Contents](../README.md)

- Follow steps from [here](https://tex.stackexchange.com/questions/292323/how-to-produce-a-pdf-with-modifications-visible-with-overleaf) to flatten the multiple tex files into one:

	- ```pip3 install latex_proj_tool```

	- ```python3 -m latex_proj_tool flat my_project/main.tex --output flat_tex.tex```

- Follow steps from [here](https://github.com/matteoacrossi/texprlcount) to do a word count on the flattened ```out.tex``` file:

	- ```wget https://raw.githubusercontent.com/matteoacrossi/texprlcount/master/texprlcount.pl```

	- ```perl texprlcount.pl flat_tex.tex```

- The PRL word limit as of today (Dec 2, 2022) is: ```3,750 words```.