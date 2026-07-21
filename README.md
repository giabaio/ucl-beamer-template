# UCL official branding beamer template

This is the beamer theme for the UCL official branding (2026). The style needs the folders
`css/fonts` with the official UCL fonts and `images` with the official logo (in different sizes and formats).

At present, the style handles compilation with `lualatex` only -- but `xelatex` and possibly `pdflatex` should
not be too complicated to create.

## Example
1. Download/fork this repository
2. Open the `.tex` file and compile using `lualatex`, for instance on a terminal type
   ```
   lualatex presentation.tex
   ```
 
## .tex file
The `.tex` file contains a section in which the user can specify their details, including the possibility to
add social media links and icons (via `fontawesome5`). These are of course only optional and more could be 
customised.

Simply change name, title, date, etc in the block below in the `presentation.tex` file. 

```
%------------------------------------------------------------
% PRESENTATION METADATA
%------------------------------------------------------------
\title[A short title]{A very long title for my slides, which may span across two lines}
\author{Your Name}
\date[20 Jul 2026]{20 July 2026}

% Using your new automated conference metadata macro
\conference[SHORTER TITLE OF THE CONFERENCE]{The full name of the conference, Where it is\\ The name of the session}

% Affiliation
\institute{Department of Statistical Science ~ | ~ University College London}

% These can be commented out if you don't want email/website/social media links
\newcommand{\insertsocials}{%
  {\setlength{\baselineskip}{9pt}%
  \faEnvelope~\href{mailto:n.surname@ucl.ac.uk}{\texttt{n.surname@ucl.ac.uk}} \\
  \faGlobe~\href{https://yourwebsite.com}{\texttt{https://yourwebsite.com}}\\
  \faGithub~\href{https://github.com/you}{\texttt{https://github.com/you}} \\
% Can also add social media links, e.g.
  \faMastodon~\href{https://mas.to/@yourmastodon}{\texttt{@yourmastodon@mas.to}} \,\textbar\, 
  \faLinkedinIn~\href{https://www.linkedin.com/in/name-surname/}{\texttt{name-surname}}
  }%
}
```

## Potential issues
The code may potentially complain when processing the command `\mathcolor`. A suitable fix should be to add
```
\usepackage{xcolor}
\makeatletter
\def\mathcolor#1#{\@mathcolor{#1}}
\def\@mathcolor#1#2#3{%
  \protect\leavevmode
  \begingroup
    \color#1{#2}#3%
  \endgroup
}
\makeatother
```
to the `beamerthemeUCL.sty` file (thanks to Phil Dawid for pointing this out). This, however, was not happening on a Linux PopOS 24.04 machine, when developing the code and performing some (limited!) testing.
