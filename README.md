# Intermediate Code Generator

A full-featured compiler pipeline that generates intermediate code (Three Address Code and Quadruples) from a C-like programming language. Includes lexical analysis, parsing, semantic analysis, code generation, and optimization with an interactive GUI frontend.

## Features

### Supported Language Elements
- **Declarations**: `int x;`, `int a, b = 1, c;`, `int x = expr;`
- **Assignments**: `x = expr;`
- **I/O Operations**: 
  - `printf(expr);` or `printf("fmt", args...);`
  - `scanf("fmt", &var, ...);`
- **Control Flow**:
  - `if/else` statements
  - `while` loops
  - `for` loops
  - `do-while` loops
  - Block statements `{ ... }`
- **Expressions**:
  - Arithmetic: `+`, `-`, `*`, `/`
  - Comparisons: `==`, `!=`, `<`, `<=`, `>`, `>=`

### Compiler Pipeline

1. **Phase 1 - Lexical Analysis & Parsing**: Tokenizes and parses source code
2. **Phase 2 - Three Address Code (TAC)**: Generates three-address code representation
3. **Phase 3 - Quadruples**: Converts TAC to quadruple format
4. **Phase 4 - Optimization**: Applies code optimization techniques

### Input Formats
- Accepts complete C programs with `#include` and `int main()`
- Accepts individual statement snippets
- Automatic source normalization and preprocessing

## Project Structure

```
intercodegenerator/
├── frontend.py          # GUI application using Tkinter
├── phase1.py            # Lexical analysis, parsing, semantic analysis
├── phase2.py            # Three Address Code generation
├── phase3.py            # Quadruples generation
├── phase4.py            # Code optimization
└── README.md            # This file
```

## Installation

### Prerequisites
- Python 3.7 or higher
- tkinter (usually included with Python)

## Usage

### GUI Application

Launch the interactive compiler frontend:

```bash
python frontend.py
```

The GUI provides:
- Real-time compilation pipeline visualization
- Input code editor
- Output displays for each compilation phase
- Syntax error detection and reporting

### Command Line Usage

```python
from phase1 import lex, Parser, CodeGenerator, SemanticAnalyzer

# Tokenize
tokens = lex(source_code)

# Parse
parser = Parser(tokens)
ast = parser.parse()

# Semantic Analysis
analyzer = SemanticAnalyzer()
analyzer.analyze(ast)

# Code Generation
generator = CodeGenerator()
intermediate_code = generator.generate(ast)
```

## Example

### Input
```c
int main() {
    int a = 5;
    int b = 3;
    int c = a + b * 2;
    printf(c);
    return 0;
}
```

### Output (TAC)
```
t1 = b * 2
t2 = a + t1
c = t2
```

### Output (Quadruples)
```
(*, b, 2, t1)
(+, a, t1, t2)
(=, t2, _, c)
```

## Architecture

### Lexical Analysis
- Tokenizes input source code
- Identifies keywords, identifiers, operators, and literals
- Generates token stream for parser

### Parser
- Recursive descent parser
- Builds Abstract Syntax Tree (AST)
- Validates syntax correctness

### Semantic Analyzer
- Type checking
- Variable scope verification
- Symbol table management
- Semantic error detection

### Code Generator
- Converts AST to intermediate code
- Generates Three Address Code (TAC)
- Manages temporary variables

### Optimizer
- Removes redundant instructions
- Constant folding
- Dead code elimination

## Supported Platforms

- Windows
- macOS
- Linux

## Contributing

Contributions are welcome! Please feel free to submit issues and pull requests.

## License

This project is open source and available under the MIT License.

## Author

Created as a compiler design educational project.

## Troubleshooting

### Issue: GUI doesn't open
**Solution**: Ensure tkinter is installed. On Linux, run: `sudo apt-get install python3-tk`

### Issue: Compilation errors
**Solution**: Check input syntax. The compiler supports the language elements listed in Features.

### Issue: Tokenization fails
**Solution**: Verify source code follows C-like syntax rules. Check for unclosed strings or invalid operators.

## References

This project implements standard compiler design concepts including:
- Lexical analysis (scanning)
- Syntax analysis (parsing)
- Semantic analysis
- Intermediate code generation
- Code optimization

Based on classical compiler design patterns (Dragon Book style).
