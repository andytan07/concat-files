# concat_files

A small command-line utility that finds and concatenates multiple files' content, wrapping them in XML-style tags and copying to clipboard. Perfect for quickly gathering related source files for documentation, code review, or AI assistance (mostly for Claude Projects)

## Features

- 🔍 Supports glob patterns for file matching
- 📁 Recursively searches in current directory and subdirectories
- 🚫 Configurable directory exclusion (node_modules, .git, etc.)
- 📋 Automatically copies to clipboard
- 💡 Preserves original file content and formatting
- 🏷️ Wraps content in XML-style tags with file paths
- 🌟 Cross-platform support (macOS, Linux, Windows)

## Installation

1. Clone this repository:
```bash
git clone https://github.com/andytan07/concat-files
cd concat_files
```

2. Make the script executable:
```bash
chmod +x concat_files
```

3. (Optional) Create a symlink to make it globally available:
```bash
# For single user
ln -s "$(pwd)/concat_files" ~/.local/bin/concat_files

# Or system-wide (requires sudo)
sudo ln -s "$(pwd)/concat_files" /usr/local/bin/concat_files
```

### Requirements

- Python 3.x
- Platform-specific clipboard utilities:
  - macOS: Built-in `pbcopy` (no additional installation needed)
  - Linux: `xclip` (install via `sudo apt-get install xclip` or your distro's package manager)
  - Windows: Built-in `clip` (no additional installation needed)

## Usage

### Basic Usage

```bash
concat_files [file_patterns...]
```

### Examples

1. Find all related component files:
```bash
concat_files task.component.*
```
This will find files like:
- task.component.ts
- task.component.html
- task.component.scss
- task.component.spec.ts

2. Use wildcards in the middle:
```bash
concat_files user*.component.*
```
This will find files like:
- user.component.ts
- user-details.component.ts
- user-list.component.html

3. Mix exact filenames with patterns:
```bash
concat_files user.component.* user.service.ts
```

4. Use multiple patterns:
```bash
concat_files "auth*.service.*" "user*.component.*"
```

### Output Format

The script copies the content to your clipboard in this format:
```xml
<file path="src/app/components/user.component.ts">
// Original file content here
</file>
<file path="src/app/components/user.component.html">
<!-- Original file content here -->
</file>
```

### ZSH Users

If you're using ZSH, you'll need to either:

1. Quote the glob patterns:
```bash
concat_files "user.component.*"
```

2. Or add this to your `~/.zshrc` (recommended):
```bash
alias concat_files='noglob concat_files'
```

## Customization

You can customize excluded directories by modifying the `excluded_directories` set in the script:

```python
excluded_directories = {
    'node_modules',
    '.git',
    'dist',
    'build',
    'coverage',
    'vendor'    # Add more directories to exclude
}
```