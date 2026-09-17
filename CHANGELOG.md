# Changelog

All notable changes to Edito will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed
- Changed build system to CMake.
- Improved main window apperance with layouts.

### Fixed
- Disabled maximizing and resizing for main window.

## [v1.0.0]

### Added
- Added automatic spellchecking to the editor. Misspelled words are now underlined in red, and right-clicking offers suggested replacements.
- Added search for the selected text in the editor when the user selects texts and uses the find and replace feature.

### Fixed
- Fixed broken character encoding detection by improving BOM detection logic and using uchardet library for better accuracy.