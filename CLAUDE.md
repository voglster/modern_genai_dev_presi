# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Slidev presentation about "GenAI and Software Development" that demonstrates how AI tools enhance modern development workflows. The presentation uses Slidev, a slides maker and presenter powered by Vue.js.

## Common Development Commands

```bash
# Install dependencies (in the presi directory)
cd presi
pnpm install   # or yarn install

# Run development server (auto-opens at http://localhost:3030)
pnpm dev       # or yarn dev

# Build for production
pnpm build     # or yarn build

# Export slides to PDF or other formats
pnpm export    # or yarn export
```

## High-Level Architecture

### Directory Structure
- `/presi/` - Main presentation directory containing all Slidev-related files
  - `slides.md` - The main presentation file with all slide content
  - `components/` - Custom Vue components (e.g., Counter.vue)
  - `images/` - Presentation images and diagrams
  - `package.json` - Dependencies and scripts configuration
- `/notes/` - Detailed presentation notes and outline
  - `main.md` - Comprehensive notes for the presentation
- `/docs/` - Documentation files
  - `slidev-llms.txt` - Slidev framework documentation for LLM context

### Slidev Framework

Slidev uses a Markdown-based format for creating presentations. Key concepts:

1. **Slide Separation**: Use three hyphens (`---`) to separate slides
2. **Frontmatter**: YAML configuration at the beginning of slides.md and individual slides
3. **Layouts**: Pre-built layouts like `center`, `image-right`, `two-cols`
4. **Vue Components**: Can embed Vue components directly in Markdown
5. **Interactive Elements**: Support for click animations, code highlighting, and live coding

### Key Configuration Files

- **Frontmatter in slides.md**: Global presentation settings (theme, title, transition effects)
- **netlify.toml & vercel.json**: Deployment configurations for hosting platforms
- **package.json scripts**:
  - `dev`: Development server with auto-reload
  - `build`: Production build to `dist/`
  - `export`: Export to various formats

## Slidev Documentation Reference

For detailed Slidev formatting and features, refer to `/docs/slidev-llms.txt` which contains comprehensive documentation about:
- Slide syntax and formatting
- Component usage and customization
- Layout options and configurations
- Interactive features (Monaco editor, code runners, animations)
- Deployment and hosting options

## Development Tips

1. **Hot Reload**: The dev server automatically reloads when you edit slides.md
2. **Component Auto-Import**: Vue components in the `components/` directory are automatically available
3. **Code Highlighting**: Use triple backticks with language identifiers for syntax highlighting
4. **Presenter Mode**: Available during development for speaker notes
5. **Export Formats**: Supports PDF, PNG, and other formats via the export command

## Current Presentation Structure

The presentation covers:
1. Introduction to GenAI/LLMs in Development
2. What AI Can and Cannot Do
3. Best Practices for AI-Assisted Development
4. Modern Development Workflows
5. Team and Career Impact

The presenter will share their experience with AI-enhanced development workflows and practical applications.