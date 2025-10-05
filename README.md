# BA(I)SH - A stupid simple AI helper for your bash

A simple command-line interface that supports both single-shot queries and interactive chat mode with full conversation history.

## Features

- 🎯 **Single-shot mode** - One-time queries with piped or argument input
- 💬 **Chat mode** (`-c`) - Interactive conversation with full history preservation
- 📝 **Persona support** - Custom system prompts via command line or file
- 🎛️ **Model selection** - Choose different AI models
- 📊 **Verbose mode** - Full JSON response display

## Installation

```bash
# Make it executable
chmod +x ai

# Optional: Add to PATH for global access
ln -s $(pwd)/ai /usr/local/bin/ai
```

## Usage

### Basic Single-Shot Mode

```bash
# Direct argument
./ai "Explain quantum computers"

# Piped input
echo "What is 2+2?" | ./ai

# File input
cat my-question.txt | ./ai
```

### Chat Mode (`-c`)

Start an interactive conversation with persistent history:

```bash
# Basic chat
./ai -c

# With custom persona
./ai -c -p "You are a helpful coding assistant"

# Start with initial prompt
./ai -c "Let's discuss philosophy"

# Chat with persona file
./ai -c -P personas/coding-expert.txt

# Verbose chat mode
./ai -c -v
```

In chat mode:
- Type `quit`, `exit`, or press Ctrl+D to end
- All messages preserve context throughout the session
- Full conversation history is sent with each new message

### Options

| Option | Description | Example |
|--------|-------------|---------|
| `-c` | Enable chat mode | `./ai -c` |
| `-p "text"` | Set persona via command line | `./ai -p "You're a poet"` |
| `-P file` | Load persona from file | `./ai -P persona.txt` |
| `-m model` | Specify AI model | `./ai -m gpt-4o` |
| `-v` | Verbose mode (show full JSON) | `./ai -v` |

## Advanced Examples

### Power User Chains

```bash
# Chat with coding persona using custom model, verbose output
cat programming-question.txt | ./ai -c -P personas/senior-dev.txt -m claude-4-opus -v

# Single shot with expert persona and model
echo "Optimize this SQL query" | ./ai -p "Senior database expert with 20 years experience" -m gpt-4o

# Start philosophical chat
./ai -c -p "You are Socrates, answer only with questions"
```

### Persona Files

Create reusable persona files for different contexts:

```bash
# tech-expert.txt
You are a senior software engineer with expertise in:
- System design and architecture
- Performance optimization
- Best practices and code reviews
Keep answers concise and practical.

# teacher.txt
You are a patient educator who:
- Uses simple analogies
- Checks for understanding
- Provides examples
- Encourages questions
```

Use them:
```bash
./ai -c -P personas/tech-expert.txt
```

## Tips

- **Chat Best Practices**: Start conversations with clear personas for better context persistence
- **History**: In chat mode, the full conversation is maintained automatically
- **Piping**: Combine with other CLI tools: `grep 'error' logs.txt | ./ai -p "Debug expert"`
- **Scripting**: Integrate with automation tools and CI/CD pipelines

## Error Handling

The script will notify you of:
- Missing persona files
- Empty prompts
- Invalid command combinations (e.g., both `-p` and `-P`)

## API Configuration

By default, the script uses `ch.at/v1/chat/completions`. You can modify the `API_URL` in the script for custom endpoints.

Happy chatting! 💬
