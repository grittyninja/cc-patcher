# cc-patcher

A modular patching tool for Claude Code binary that enhances functionality through targeted modifications.

## Overview

cc-patcher is a shell script that applies modular patches to Claude Code binary files to unlock enhanced features and customization options. The tool creates automatic backups and validates all changes before applying them.

## Features

- **Context Limit Enhancement**: Increases Claude Code's context limit through environment variable configuration
- **Security Context Cleaning**: Removes security-related context restrictions for enhanced functionality
- **Temperature Control**: Allows custom temperature settings via environment variables
- **Modular Design**: Apply individual patches or all at once
- **Automatic Backups**: Creates timestamped backups before patching
- **Pattern Validation**: Validates all patterns exist before applying changes
- **Cross-Platform**: Compatible with Unix-like systems (Linux, macOS)

## Installation

1. Clone or download the repository:
   ```bash
   git clone <repository-url>
   cd cc-patcher
   ```

2. Make the script executable:
   ```bash
   chmod +x cc-patcher.sh
   ```

3. Verify the script is working:
   ```bash
   ./cc-patcher.sh --version
   ```

### Requirements

- Unix-like operating system (Linux, macOS, WSL)
- Basic shell utilities (sed, grep, awk)
- Write permissions to the target binary file
- Claude Code binary file to patch

### Compatibility

**Tested Version:**
- Claude Code v2.0.19

**Note:** This patcher is designed to work with Claude Code binary files. Pattern matching is version-specific, and compatibility may vary with different Claude Code versions. Always create backups before applying patches.

## Usage

### Basic Usage

Apply all available patches to a binary:
```bash
./cc-patcher.sh --binary /path/to/claude-code-binary
```

Apply specific modules:
```bash
./cc-patcher.sh --binary /path/to/claude-code-binary --modules context_limit,temperature_setting
```

### Command Line Options

- `-b, --binary <path>`: Path to the binary file to patch (required)
- `-m, --modules <list>`: Comma-separated list of modules to apply (optional, default: all)
- `-l, --list-modules`: List all available patch modules
- `-h, --help`: Show help message
- `-v, --version`: Show version information

### Examples

1. **List available modules:**
   ```bash
   ./cc-patcher.sh --list-modules
   ```

2. **Apply all patches:**
   ```bash
   ./cc-patcher.sh --binary /usr/local/bin/claude-code
   ```

3. **Apply specific modules:**
   ```bash
   ./cc-patcher.sh --binary ./claude-code --modules context_limit
   ```

4. **Apply multiple specific modules:**
   ```bash
   ./cc-patcher.sh -b ./claude-code -m context_limit,temperature_setting
   ```

## Available Modules

### context_limit
Increases Claude Code's context limit by modifying the function return value and adding support for environment variable configuration.

**Environment Variables:**
- `CLAUDE_CONTEXT_LIMIT`: Set custom context limit (overrides default 200000)

**Example:**
```bash
export CLAUDE_CONTEXT_LIMIT=1000000
./claude-code
```

### security_context_clean
Cleans security-related context restrictions by modifying DTB template handling and file processing logic.

**Environment Variables:**
- `CLAUDE_PERSISTENT_PROMPT`: Set custom persistent prompt (fallback to DTB if not set)

**Example:**
```bash
export CLAUDE_PERSISTENT_PROMPT="Your custom system prompt"
./claude-code
```

### temperature_setting
Allows setting custom temperature values via environment variables, with support for different modes.

**Environment Variables:**
- `CLAUDE_TEMPERATURE`: Set global temperature (0.0-1.0)
- `CLAUDE_PLAN_TEMPERATURE`: Set temperature for plan mode
- `CLAUDE_CURRENT_MODE`: Current mode detection (automatically set)

**Examples:**
```bash
# Set global temperature
export CLAUDE_TEMPERATURE=0.7
./claude-code

# Set different temperature for plan mode
export CLAUDE_TEMPERATURE=0.5
export CLAUDE_PLAN_TEMPERATURE=0.9
./claude-code
```

## Safety and Backups

### Automatic Backups
The script automatically creates timestamped backups before applying any patches:
```
original-file.backup.20241006_143022
```

### Validation
- All patterns are validated before applying changes
- If any pattern is not found, the module will not be applied
- Partial module failures are reported and handled safely

### Recommendations
1. **Always test on a copy** of your binary first
2. **Keep backups** in a safe location
3. **Verify functionality** after patching
4. **Document your changes** for future reference

### Troubleshooting
- If patching fails, check the error messages for missing patterns
- Ensure the binary file is writable
- Verify you're using the correct binary version
- Check that all required utilities are available

## Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork the repository** and create a feature branch
2. **Test your changes** thoroughly on multiple binary versions
3. **Update documentation** for any new modules or features
4. **Follow the existing code style** and conventions
5. **Submit a pull request** with a clear description of changes

### Development Guidelines
- Use descriptive variable names
- Add comments for complex pattern matching
- Validate all user inputs
- Handle errors gracefully
- Maintain backward compatibility when possible

## License

This project is released under the MIT License. See the LICENSE file for details.

## Disclaimer

This tool is provided as-is for educational and research purposes. The authors are not responsible for any damage or loss of functionality that may result from using this software. Always create backups and use at your own risk.

## Changelog

### Version 1.0.2
- Initial release
- Three core patch modules: context_limit, security_context_clean, temperature_setting
- Automatic backup functionality
- Pattern validation system
- Cross-platform compatibility
- Support for v2.0.14

### Version 1.0.3
- Added support for v2.0.19
