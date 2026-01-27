# Generator

Compiles source files (`src/`) into platform-specific distributions (`dist/`).

## Usage

```bash
# Generate all platforms
npm run build

# Generate specific platform
npm run build -- --platform opencode
npm run build -- --platform claude-code

# Clean generated files
npm run clean
```

## How It Works

1. **Reads config** from `src/config/platforms/*.ts`
   - Platform-specific templates and file extensions
   - Output directory structure

2. **Reads content** from `src/content/`
   - Agents: `agents/*.md`
   - Skills: `skills/*/skill.md`
   - Commands: `commands/*.md`

3. **Generates output** to `dist/<platform>/`
   - Applies platform-specific templates
   - Creates directory structure
   - Copies/transforms content

## Platform Configs

Each platform config defines:

```typescript
interface PlatformConfig {
  name: string;                    // Platform identifier
  outputDir: string;               // Output directory name
  fileExtensions: {                // File extensions for each type
    agent: string;
    skill: string;
    command: string;
  };
  agentTemplate: (content: string) => string;   // Transform agent content
  skillTemplate: (content: string) => string;   // Transform skill content
  commandTemplate: (content: string) => string; // Transform command content
}
```

### OpenCode Platform

- Output: `dist/opencode/`
- Extensions: `.md` for all types
- Templates: Pass-through (no transformation)

### Claude Code Platform

- Output: `dist/claude-code/`
- Extensions: `.md` for all types
- Templates: Pass-through (no transformation)

## Troubleshooting

### Build fails with "Cannot find module"

```bash
npm install
```

### Generated files missing

Check that source files exist:
- `src/content/agents/*.md`
- `src/content/skills/*/skill.md`
- `src/content/commands/*.md`

### Platform not generating

Verify platform config is registered in `src/config/platforms/index.ts`.

### Changes not reflected

1. Run `npm run build` after editing source files
2. Run `make install` to copy to `~/.claude` or `~/.opencode`

## Adding a New Platform

See [CONTRIBUTING.md](../CONTRIBUTING.md#adding-platform-support) for details.

## Technical Details

- **Language**: TypeScript
- **Entry point**: `generator/generate.ts`
- **Config**: `src/config/`
- **Content**: `src/content/`
- **Output**: `dist/` (git-ignored)

The generator is stateless and idempotent—running it multiple times produces the same output.
