# BSTokenizer

A Python library for tokenizing and manipulating Beat Saber maps and replays.

## Installation

## Features
- Convert Beat Saber maps to and from a token-based representation
- Support for all common Beat Saber map formats (v2, v3, and v4)
- Automatic map format conversion between versions
- Custom data handling for position modifications
- Extract and manipulate Beat Saber replay data (BSOR format)
- Utilities for time-to-beat conversions

## Basic Usage

### Working with Beat Saber Maps

```python
from bstokenizer import BeatSaberMapTokenizer, convert
import json

# Initialize tokenizer
tokenizer = BeatSaberMapTokenizer(default_bpm=120.0) # default_bpm is the same as the Info.dat bpm

# Load map from file
with open('ExpertPlusStandard.dat', 'r') as f:
    map_data = json.load(f)

# Tokenize the map
tokens = tokenizer.tokenize(map_data)

# Manipulate tokens
for token in tokens:
    if token["type"] == "color_note":
        # Modify note positions
        token["x"] += 1

# Convert back to map format
modified_map = tokenizer.detokenize(tokens)

# Convert between map versions
v3_map = convert(map_data, "v3")
```

### Working with Beat Saber Replays

```python
from bstokenizer import BeatSaberReplayTokenizer

# Initialize tokenizer
replay_tokenizer = BeatSaberReplayTokenizer()

# Load replay from file
replay_tokens = replay_tokenizer.tokenize("path/to/replay.bsor")

# Analyze replay data
for token in replay_tokens:
    if token["type"] == "note":
        # Access note cut data
        if "cut" in token:
            print(f"Note at {token['time']}s - Score: {token['score']}")
```

## For Developers

### Running Tests

Ensure your changes work correctly by running the test suite:

```bash
# Run all tests
pytest bstokenizer/tests/test.py

# Run with verbose output
pytest -v bstokenizer/tests/test.py
```

### Development Setup

1. Clone the repository
2. Install development dependencies:
    ```bash
    pip install -e ".[dev]"
    ```

### Contributing

Contributions are welcome! Please follow these steps:
1. Fork the repository
2. Create a feature branch
3. Add tests for your changes
4. Ensure all tests pass
5. Submit a pull request

## Requirements
- Python 3.7+
- py-bsor library for replay handling

## License
MIT