# Alchemy 2

This repository is based on this [fork](https://github.com/dylanbeadle/alchemy-2) of the [Alchemy 2 software](https://code.google.com/p/alchemy-2/).  
The source files were modified to resolve the build errors that occurred while trying to compile on a Windows machine.

## Description

Alchemy is a software package providing a series of algorithms for statistical relational learning and probabilistic logic inference, based on the Markov logic representation.

Alchemy 2.0 includes the following algorithms:

- Discriminative weight learning (Voted Perceptron, Conjugate Gradient, and Newton's Method)
- Generative weight learning
- Structure learning
- propositional MAP/MPE inference (including memory efficient)
- propositional and lazy Probabilistic inference algorithms: MC-SAT, Gibbs Sampling and Simulated Tempering
- Lifted Belief propagation
- Support for native and linked-in functions
- Block inference and learning over variables with mutually exclusive and exhaustive values
- EM (to handle ground atoms with unknown truth values during learning)
- Specification of indivisible formulas (i.e. formulas that should not be broken up into separate clauses)
- Support of continuous features and domains
- Online inference
- Decision Theory
- Probabilistic theorem proving (lifted weighted model counting)
- Lifted importance sampling
- Lifted Gibbs sampling

More info at http://alchemy.cs.washington.edu/

## Installation

### Cygwin installation

- Download Cygwin: https://www.cygwin.com/setup-x86_64.exe
- During installation, after chosing a mirror link, select the _Category_ option from the dropdown menu and install all packets in the _Devel_ list (not mandatory but can help reduce headaches). This should install, among others, the necessary requirements for Alchemy to run, namely g++ (version $\geq$ 4.1.2), Bison (version $\geq$ 2.3) and Flex (version $\geq$ 2.5.4).
- Add Cygwin's bin folder (by default in `C:/cygwin64/bin`) to the system's path variables.

### Building Alchemy

- Either git-clone or extract this repository into the desired folder, e.g. `Alchemy`.
- If no `bin` folder is present, run `mkdir bin\obj`.
- Open a shell and navigate to the `src` folder with `cd Alchemy/src`.
- Run `make depend`.
- Run `make`.

**Note**: several changes were made for this command to compile:

- In `Alchemy/src/parser/fol.y`, the expression line 2491 was changed from `'x^2 + x + 3'` to `"x^2 + x + 3"`.
- In `Alchemy/src/parser/fol.cpp`, all instances of `YYEMPTY`, `YYEOF`, and `YYerror` occurring in the file's functions were changed to respectively `YYSYMBOL_YYEMPTY`, `YYSYMBOL_YYEOF`, and `YYSYMBOL_YYerror`.
- To prevent overwriting of the `fol.cpp` file, line 223 (`mv -f fol.tab.c  $(PARSER)/fol.cpp`) of `Alchemy/src/makefile` was commented out. Note that this line could have been replaced with `mv fol.tab.c $(PARSER)/fol.tab.c.bak` instead.

The full consequences of these changes are unknown.

## Usage

To run the binary files generated, either Visual Studio or the Build Tools for Visual Studio should be installed. See this [link](https://learn.microsoft.com/en-us/cpp/build/walkthrough-compile-a-c-program-on-the-command-line?view=msvc-170) for a complete walkthrough.

- In a _Developer Command Prompt for VS 2022_, navigate to the `bin` directory with `cd Alchemy/bin`.
- Add the _.exe_ extension to all binaries in the folder.
- Run any of the commands below.

### Structure learning

Learn the structure of a model given a training database consisting of ground atoms

```
learnstruct.exe -i <input .mln file> -o <output .mln file> -t <training .db file>
```

### Weight learning

Learn parameters of a model given a training database consisting of ground atoms

```
learnwts.exe -i <input .mln file> -o <output .mln file> -t <training .db file>
```

### Inference

Infer the probability or most likely state of query atoms given a test database consisting of evidence ground atoms

```
infer.exe -i <input .mln file> -r <output file containing inference results> -e <evidence .db file> -q <query atoms (comma-separated with no space)>
```

## Tutorials

https://alchemy.cs.washington.edu/tutorial/tutorial.html

## License

By using Alchemy, you agree to accept the license agreement in LICENSE.md
