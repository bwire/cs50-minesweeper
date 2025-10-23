# Minesweeper AI

An intelligent AI agent that plays Minesweeper using propositional logic and knowledge-based reasoning. This project implements a sophisticated AI that can make safe moves and infer mine locations through logical deduction.

## Overview

This project is part of CS50's Introduction to Artificial Intelligence with Python. The AI uses propositional logic to represent knowledge about the Minesweeper game state and makes intelligent decisions about which cells are safe to click or likely to contain mines.

## Background

### Minesweeper Game
Minesweeper is a puzzle game consisting of a grid of cells, where some cells contain hidden mines. The goal is to identify all mine locations without detonating any. When a safe cell is clicked, it reveals a number indicating how many neighboring cells contain mines.

### Knowledge Representation
The AI represents its knowledge using logical sentences of the form `{cells} = count`, where:
- `cells` is a set of board cells
- `count` is the number of those cells that are mines

This representation enables efficient inference and deduction about mine locations.

## Features

### Core Components

1. **Minesweeper Class**: Game logic and board management
2. **Sentence Class**: Logical representation of game knowledge
3. **MinesweeperAI Class**: Intelligent agent with reasoning capabilities

### AI Capabilities

- **Safe Move Detection**: Identifies cells guaranteed to be safe
- **Mine Inference**: Determines cells that must contain mines
- **Knowledge Base Management**: Maintains and updates logical sentences
- **Subset Inference**: Derives new knowledge from existing sentences
- **Random Move Fallback**: Makes educated guesses when no safe moves are available

## Implementation Details

### Sentence Class Methods

- `known_mines()`: Returns cells known to be mines
- `known_safes()`: Returns cells known to be safe
- `mark_mine(cell)`: Updates sentence when a cell is identified as a mine
- `mark_safe(cell)`: Updates sentence when a cell is identified as safe

### MinesweeperAI Class Methods

- `add_knowledge(cell, count)`: Processes new information and updates knowledge base
- `make_safe_move()`: Returns a guaranteed safe move
- `make_random_move()`: Returns a random move when no safe moves are available

### Key Algorithms

1. **Direct Inference**: When count = 0, all cells are safe; when count = number of cells, all cells are mines
2. **Subset Inference**: If sentence A is a subset of sentence B, derive new knowledge from the difference
3. **Knowledge Propagation**: Iteratively apply inference rules until no new knowledge can be derived

## Usage

### Running the Game

```bash
python runner.py
```

The game provides both manual and AI-controlled gameplay:
- Click cells to reveal them
- Right-click to flag suspected mines
- Use "AI Move" button to let the AI make decisions
- Use "Reset" button to start a new game

### AI Behavior

The AI follows this decision-making process:
1. Look for guaranteed safe moves
2. If no safe moves exist, make a random move from unvisited, non-mine cells
3. Update knowledge base with each move
4. Apply logical inference to derive new information

## Project Structure

```
cs50-minesweeper/
├── minesweeper.py          # Core AI implementation
├── runner.py              # Game interface and visualization
├── README.md              # This file
└── venv/                  # Virtual environment
```

## Technical Implementation

### Knowledge Base Management

The AI maintains a knowledge base of logical sentences that represent constraints about mine locations. Each sentence has the form `{cell1, cell2, ..., cellN} = count`, meaning exactly `count` of the specified cells contain mines.

### Inference Rules

1. **Zero Count Rule**: If count = 0, all cells in the sentence are safe
2. **Full Count Rule**: If count = number of cells, all cells in the sentence are mines
3. **Subset Rule**: If sentence A ⊆ sentence B, then B - A = countB - countA

### Optimization Techniques

- **Knowledge Propagation**: Iteratively apply inference rules until convergence
- **Sentence Simplification**: Remove known mines/safes from sentences
- **Duplicate Prevention**: Avoid adding redundant sentences to knowledge base

## Dependencies

- Python 3.12+
- pygame (for game visualization)
- Standard library modules: itertools, random

## Installation

1. Clone the repository
2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install pygame
   ```

## Testing

Run the automated tests:
```bash
check50 ai50/projects/2024/x/minesweeper
```

Check code style:
```bash
style50 minesweeper.py
```

## Performance Characteristics

- **Time Complexity**: O(n²) for knowledge base updates, where n is the number of sentences
- **Space Complexity**: O(n) for storing knowledge base
- **Win Rate**: Varies based on board configuration and mine density

## Limitations

- The AI may need to make random moves when insufficient information is available
- Performance degrades with very large boards due to exponential growth in possible mine configurations
- Some game states may be unsolvable without guessing

## Educational Value

This project demonstrates key concepts in artificial intelligence:
- Knowledge representation using propositional logic
- Inference and deduction algorithms
- Search and constraint satisfaction
- Game theory and decision making

## Future Enhancements

Potential improvements could include:
- Advanced inference techniques (resolution theorem proving)
- Probabilistic reasoning for uncertain situations
- Machine learning approaches for pattern recognition
- Optimization for larger board sizes

## License

This project is part of CS50's Introduction to Artificial Intelligence with Python course materials.

## Acknowledgments

- CS50 AI course staff for project design and specifications
- Harvard University for educational resources
- Python community for excellent libraries and documentation
