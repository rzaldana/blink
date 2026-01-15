# blink 👁️
A small utility that bundles a Bash script and all of its sourced files into a single, self‑contained executable.

`blink` makes it easy to distribute Bash projects that rely on multiple script files by collapsing them into one portable artifact. No more juggling `source` calls or worrying about missing dependencies.

> **Note:** This tool grew organically as a convenience for packaging my own scripts, so it currently has no dedicated unit or integration tests. I do plan to introduce proper test coverage in the future as the project evolves.

## Usage 🚀 
This script bundles a Bash program and all of its sourced library files into a single, self‑contained executable. It scans the source script for `source` statements, resolves each referenced file, and inlines the contents directly into the output file. 

### Basic command 
```bash 
./blink <source_script> <output_script>
```
- `source_script` — the Bash script you want to bundle

- `output_script` — the path where the combined script will be written

Example:
```bash
./blink ./src/my_script.bash ./dist/my_script
```

This produces a standalone script at `./dist/my_script` with all sourced libraries embedded.

### How it works
The script performs the following steps:

- Resolves the absolute path of the source script
- Scans for lines beginning with source
- Resolves each sourced file relative to the script’s directory
- Replaces each source line with the full contents of the referenced file
- Writes the final bundled script to the destination path

### Ignoring specific sources
If you want to prevent a particular source line from being embedded, add the following comment immediately above it:

```bash
# blink disable
source ./path/to/library.bash
```

The script will detect this tag and skip embedding that library.
