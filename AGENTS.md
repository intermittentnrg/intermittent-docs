# intermittent-docs

This repository contains documentation for electricity grid data sources around the world.

## Build/Lint/Test Commands

This is a documentation repository - there are no build or test commands. However, when editing markdown files:

1. **Markdown Linting**: Ensure proper markdown formatting
2. **Link Validation**: Always verify external links work before committing
3. **Internal Links**: Use relative links between markdown files (e.g., `[JAPAN.md](JAPAN.md)`)

## Template

See [importers.md](importers.md) for the documentation template.

## Japan Documentation Specific

When documenting Japan data sources:

1. **CSV Offsets**: Always document header row, data start row, and data end row - these are critical for parsing
2. **Units**: Note 万 (10,000 kW = 10 MW)
3. **Encoding**: Document Shift_JIS encoding requirement
4. **Consolidation**: Keep Juyo (demand) data in main JAPAN.md, nuclear data in separate files

## Important Notes

1. **Verify Source Code**: Before adding links, verify the referenced files exist in the external repositories
2. **Check for Updates**: Source code structure may change - verify links are current
3. **No Duplicates**: Consolidate similar data sources (e.g., Japan regions share Juyo format)
4. **Links at Bottom**: Always place Links section at the bottom of the file

## Before Submitting Changes

- [ ] All external links are valid
- [ ] Follows `importers.md` template structure
- [ ] Links section includes all relevant source code repositories
- [ ] No duplicate content exists
- [ ] Markdown formatting is correct
