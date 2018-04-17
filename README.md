# A latex protocol template

**Quickstart**
```sh
git clone git@github.com:tgm-hit/latex-protocol.git protocol
cd protocol
./make
```

**Contents**
- [Usage](#usage)
	- [Latex](#latex)
	- [TexStudio](#texstudio)
- [Options](#options)
- [Variables](#variables)

## Usage
With Python 3 and LaTeX installed you can easily compile your project using the `make` script which simplifies the compilation progress, handles multiple source files and removes unnecessary files.
For most use-cases you only have to run `./make` which compiles the `main.tex` file using `pdflatex` while looking for bibliography and glossary entries.

### Latex
If (for some reason) you do not want to depend on the `make` script you can also use `pdflatex`, `makeglossaries` and `bibtex` from the shell.
```sh
pdflatex -shell-escape main	# Initial compilation
makeglossaries main 		# Compile glossaries
pdflatex -shell-escape main	# Progressive compilation for glossaries
bibtex main 				# Compile bibliography
pdflatex -shell-escape main	# Progressive compilation for bibtex
pdflatex -shell-escape main	# Progressive compilation for bibtex
```

### TexStudio
In TexStudio a custom command can be added under `Options` &rarr; `Configure TexStudio` &rarr; `Build` &rarr; `User Commands`. The following line completely compiles a LaTeX file with glossaries, bibliography and minted.
```sh
pdflatex -shell-escape -interaction=nonstopmode % | txs:///makeglossaries | pdflatex -shell-escape -interaction=nonstopmode % | txs:///bibtex | pdflatex -shell-escape -interaction=nonstopmode % | pdflatex -shell-escape -interaction=nonstopmode % | txs:///view-pdf-internal --embedded
```

Of course you can also add the `make` script as a user command but you might want to set the variable `-l` so TexStudio can find your logfile after cleanup.
```sh
python make -l | txs:///view-pdf-internal --embedded
```

### ShareLaTex
[ShareLaTex](https://www.sharelatex.com/project) is a popular online latex editor and is also fully supported by this template. Just download the archived repository or latest release and upload as a new project.

![ShareLaTex usage](https://media.giphy.com/media/DNwRWMqKcwnE92liHn/giphy.gif)

## Options
Option | Result
------ | ------
`landscape` | Change the page format to landscape orientation
`minted` | Add and configure minted package
`natbib` | Change bibtex backend to natbib
`nobib` | Disable bibliography
`nofonts` | Change font to default
`noglo` | Disable acronyms and glossary
`nologos` | Disable logos on titlepage
`notitle` | Disable titlepage
`notoc` | Disable table of contents
`notable` | Disable table on titlepage
`parskip` | Skip line instead of indent after blank line

## Variables
Variables can be set as commands like
```tex
\myvariable{value}
```

Command | Content
------- | -------
`mysubtitle` | Subtitle of group
`mysubject` | Thematic group / subject
`mycourse` | Current course / class
`myteacher` | Current teacher
`myversion` | Current version of the document
`mybegin` | Start of documentation
`myfinish` | End of documentation
