---
title: "Zettelkasten Method"
date: 2024-01-16
tags: [zettelkasten, notes, methodology]
categories: [methods]
---

# Zettelkasten Method

The Zettelkasten method is a note-taking and knowledge management system that emphasizes creating atomic notes and linking them together.

## Core Principles

1. **Atomic Notes**: Each note contains one idea
2. **Unique Identifiers**: Every note has a distinct reference
3. **Linking**: Notes connect to related concepts
4. **No Hierarchy**: Flat structure with emergent organization

## Benefits

- Encourages deep thinking
- Reveals unexpected connections
- Creates a personal knowledge web
- Supports creative thinking

## Implementation in Jekyll

This site implements Zettelkasten principles using Jekyll collections:
- Each note is a markdown file in the `_notes` collection
- Cross-references use Jekyll's `{% raw %}{% link %}{% endraw %}` tag
- Tags and categories help organize content

## Related Notes

- {% link _notes/001-knowledge-management.md %}
- {% link _notes/003-note-taking-strategies.md %}

## References

Originated by sociologist Niklas Luhmann, the method has been adapted for digital tools.