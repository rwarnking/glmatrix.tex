# glmatrix.tex

[<img alt="Linting status of master" src="https://img.shields.io/github/actions/workflow/status/rwarnking/glmatrix.tex/ci.yml?label=CI&style=for-the-badge" height="23">](https://github.com/rwarnking/glmatrix.tex/actions/workflows/ci.yml)
[<img alt="Version" src="https://img.shields.io/github/v/release/rwarnking/glmatrix.tex?style=for-the-badge" height="23">](https://github.com/rwarnking/glmatrix.tex/releases/latest)
[<img alt="Licence" src="https://img.shields.io/github/license/rwarnking/glmatrix.tex?style=for-the-badge" height="23">](https://github.com/rwarnking/glmatrix.tex/blob/main/LICENSE)

## Description
This is a latex package repository.

## Table of Contents
- [glmatrix.tex](#glmatrixtex)
  - [Description](#description)
  - [Table of Contents](#table-of-contents)
  - [List of Features](#list-of-features)
  - [Installation](#installation)
    - [Dependencies](#dependencies)
  - [Usage](#usage)
  - [Contributing](#contributing)
  - [Credits](#credits)
  - [License](#license)

## List of Features

- commands for
  - scalar calculations
  - vector calculations
  - matrix calculations
- source .tex files
- automatically generated .dtx file
- automatically generated .sty file
- automatically generated PDF

## Installation

Including this package in your LaTeX project works in the usual way:

```latex
\usepackage{glmatrix}
```

The package is available on CTAN under the name [glmatrix](https://ctan.org/pkg/glmatrix), so it may already be included in your LaTeX distribution.

If it is not installed yet, you can add it using your distribution’s package manager:

- **TeX Live**: run `tlmgr install glmatrix`
- **MiKTeX**: install it via the MiKTeX Console or allow on-the-fly installation when compiling

When using [Overleaf](https://www.overleaf.com), the package should already be available without any additional steps.

If you encounter issues with these methods, you can alternatively download the package manually from [CTAN](https://ctan.org/pkg/glmatrix) or retrieve the [glmatrix.sty](https://github.com/rwarnking/glmatrix.tex/blob/main/glmatrix.sty) file directly from this repository. Place the file in your project directory so LaTeX can find it during compilation.

### Dependencies

This project uses LaTeX.

## Usage

You can find examples how to use this package in the examples subfolder.
The [documentation](https://github.com/rwarnking/glmatrix.tex/blob/main/glmatrix.pdf) also contains a small example that is also shown here.

Given the following equation:

$$
AB(\vec{v} + \vec{w}) \mid v, w \in \mathbb{R}^3, A, B \in \mathbb{R}^{3 \times 3}
$$

The code below recreates the equation with exemplary values and directly calculates the results.
Then, the results are used to print a step-by-step solution with
the chosen values.

Note:

- While creating a new vector or matrix is done by providing its name as a
simple string, accessing its content after creation is done as a command (with backslash)
- This package mainly provides macros for mathematical calculations. These macros assign the calculated result automatically to a variable using the optional parameter (for example `\addVec`). If you wish to specify the name of the variable yourself, you may pass a string for the optional argument.

```latex
% Initialize two vectors and add them together
\newVec{myVecV}{1, 2, 3}
\newVec{myVecW}{7, 8, 9}
\addVec[addVecResult]{\myVecV}{\myVecW}
% Initialize two matrices and multiply them with each other
\newMat{myMatA}{{{0.5, 2, 3}{4, 5, 6}{7, 8, 9}}}
\newDiagMat{myMatB}{2, 3, 4}
\mulMat[mulMatResult]{\myMatA}{\myMatB}
% Transform the result vector with the created matrix
\transformVec{\mulMatResult}{\addVecResult}
% Print a step -by - step solution
\begin{align}
  \printMat{\myMatA} \printMat{\myMatB}
  \left(\printVec{\myVecV} + \printVec{\myVecW}\right)
\end{align}
\begin{align}
  =
  \printMat{\mulMatResult}
  \printVec{\addVecResult}
  =
  \printVec{\transformVecResult}
\end{align}
```

When compiling the above LaTeX code, the following output is created.

$$\begin{pmatrix}0.5&2&3\\\4&5&6\\\7&8&9\end{pmatrix}\begin{pmatrix}2&0&0\\\0&3&0\\\0&0&4\end{pmatrix}\left(\begin{pmatrix}1\\\2\\\3\end{pmatrix}+\begin{pmatrix}7\\\8\\\9\end{pmatrix}\right)=\begin{pmatrix}1&6&12\\\8&15&24\\\14&24&36\end{pmatrix}\begin{pmatrix}8\\\10\\\12\end{pmatrix}=\begin{pmatrix}212\\\502\\\784\end{pmatrix}$$

All three classes provide various macros to print the content of a variable for all kinds of use cases. For example, you can print a vector inside a line of text using the `\printVecT`, which prints a transposed version of the vector’s contents.

## Contributing

I encourage you to contribute to this project, in form of bug reports, feature requests
or code additions. Although it is likely that your contribution will not be implemented.

Please check out the [contribution](docs/CONTRIBUTING.md) guide for guidelines about how to proceed
as well as a styleguide.

## Credits
Up until now there are no further contributors other than the repository creator.

## License
This project is licensed under the [MIT License](LICENSE).
