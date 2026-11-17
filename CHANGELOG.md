# Changelog

## 1.1.0

Release date 2026-11-17

- New section H with four patterns for standalone scripts and CLI tools: threading primitives inside asyncio, two libraries for one job, portability guards nobody asked for, and terminal boxes measured by hand
- Pattern 20 now covers a stray import inside a function when the rest sit at the top
- Warns against overcorrecting into code with no comments at all
- Fixed the self-check step, which pointed at pattern 15 for inflated words instead of 16

## 1.0.0

Release date 2026-11-17

- First release with 24 patterns in seven sections
- Behavior ledger that records public names, return values, errors, and side effects before editing and checks the rewrite against them
- Reads neighboring files so the rewrite follows the codebase's own conventions
- Pasted, file, embedded, and review modes
- Hands commit messages and PR prose to qalam when it is installed
