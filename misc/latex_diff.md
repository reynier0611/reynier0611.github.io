## LaTeX diff
[Back to table of Contents](../README.md)

- Download the old and new versions of the document from Overleaf

- Follow steps from [here](https://tex.stackexchange.com/questions/292323/how-to-produce-a-pdf-with-modifications-visible-with-overleaf) to flatten the multiple tex files into one.

	- ```pip3 install latex_proj_tool```

	- ```python3 -m latex_proj_tool flat my_project/main.tex --output out.tex```

- Produce a diff file ```latexdiff old.tex new.tex > diff.tex```

- Compile this diff file to produce a pdf