# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Quartz v4 is a static site generator for publishing digital gardens and notes as websites. It transforms Markdown content into a fully-featured website with search, graph visualization, backlinks, and more.

Documentation: https://quartz.jzhao.xyz/

## Commands

```bash
# Development - serve docs with hot reload
npx quartz build --serve -d docs

# Build only (no server)
npx quartz build

# Type check and format check
npm run check

# Format code
npm run format

# Run tests
npm test

# Profile build performance
npm run profile
```

## Architecture

### Build Pipeline

The build process flows through three stages, orchestrated by `quartz/build.ts`:

1. **Parse** (`quartz/processors/parse.ts`) - Reads Markdown files, applies transformer plugins to convert content through text → Markdown AST → HTML AST
2. **Filter** (`quartz/processors/filter.ts`) - Applies filter plugins to exclude content (e.g., drafts)
3. **Emit** (`quartz/processors/emit.ts`) - Applies emitter plugins to generate output files (HTML pages, search index, RSS, sitemap)

### Plugin System

Three plugin types in `quartz/plugins/`:

- **Transformers** (`transformers/`) - Modify content during parsing. Can hook into `textTransform`, `markdownPlugins` (remark), or `htmlPlugins` (rehype)
- **Filters** (`filters/`) - Decide what content to publish via `shouldPublish()` returning boolean
- **Emitters** (`emitters/`) - Generate output files. Implement `emit()` and optionally `partialEmit()` for incremental builds

Plugin configuration is in `quartz.config.ts`. Plugin order matters - transformers are applied sequentially.

### Component System

Preact components in `quartz/components/` render pages. Components are configured in `quartz.layout.ts` which defines what appears in headers, sidebars, and footers for content vs list pages.

### Key Files

- `quartz.config.ts` - Main config: theme, plugins, analytics, base URL
- `quartz.layout.ts` - Page layout: which components where
- `quartz/bootstrap-cli.mjs` - CLI entry point, bundles Quartz with esbuild
- `quartz/build.ts` - Main build orchestration
- `quartz/worker.ts` - Worker thread for parallel Markdown parsing (used for >128 files)

### Directory Structure

- `/content` - User's Markdown content
- `/public` - Generated static output
- `/quartz` - The SSG engine source code
- `/docs` - Quartz documentation (also example content)

## Tech Stack

- TypeScript with Preact for components (static rendering only)
- unified/remark/rehype ecosystem for Markdown processing
- esbuild for bundling
- shiki for syntax highlighting
- Worker threads for parallel processing
