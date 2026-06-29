---
name: writing-docs
description: Guides for writing and editing Remotion documentation. Use when adding docs pages, editing MDX files in packages/docs, or writing documentation content.
---

# Writing Remotion Documentation

Documentation lives in `packages/docs/docs` as `.mdx` files.

## Adding a new page

1. Create a new `.mdx` file in `packages/docs/docs`
2. Add the document to `packages/docs/sidebars.ts`
3. Write the content following guidelines below
4. Run `bun render-cards.ts` in `packages/docs` to generate social preview cards

**Breadcrumb (crumb)**: If a documentation page belongs to a package, add `crumb: '@remotion/package-name'` to the frontmatter.

```md
---
image: /generated/articles-docs-my-package-my-api.png
title: '<MyComponent>'
crumb: '@remotion/my-package'
---
```

**One API per page**: Each function or API should have its own dedicated documentation page.

**Public API only**: Documentation is for public APIs only. Do not mention internal/private APIs.

**Use headings for all fields**: Use `###` for top-level properties and `####` for nested properties. Do not use bullet points for individual fields.

## Language guidelines

- **Keep it brief**: Developers don't like to read. Extra words cause information loss.
- **Link to terminology**: Use [terminology](/docs/terminology) page for Remotion-specific terms.
- **Avoid emotions**: Remove filler like "Great! Let's move on..."
- **Separate into paragraphs**: Break up long sections.
- **Address as "you"**: Not "we".
- **Don't blame the user**: Say "The input is invalid" not "You provided wrong input".
- **Don't assume it's easy**: Avoid "simply" and "just".

## Code snippets

Basic syntax highlighting:

```ts
const x = 1;
```

### Type-safe snippets (preferred)

Use `twoslash` to check snippets against TypeScript:

```ts twoslash
import {useCurrentFrame} from 'remotion';
const frame = useCurrentFrame();
```

### Hiding imports

Use `// ---cut---` to hide setup code:

```ts twoslash
import {useCurrentFrame} from 'remotion';
// ---cut---
const frame = useCurrentFrame();
```

### Adding titles

Always add a `title` to code fences that show example usage:

```ts twoslash title="MyComponent.tsx"
console.log('Hello');
```

## Special components

### Steps

```md
- <Step>1</Step> First step
- <Step>2</Step> Second step
```

### Experimental badge

```md
<ExperimentalBadge>
<p>This feature is experimental.</p>
</ExperimentalBadge>
```

### Interactive demos

```md
<Demo type="rect"/>
```

### AvailableFrom

For page-level version indicators:

```md
# &lt;MyComponent&gt;<AvailableFrom v="4.0.123" />
```

For section headings:

```md
## Saving to another cloud<AvailableFrom v="3.2.23" />
```

### CompatibilityTable

```md
## Compatibility

<CompatibilityTable chrome firefox safari nodejs="" bun="" serverlessFunctions="" clientSideRendering={false} serverSideRendering player studio hideServers />
```

### Optional parameters

1. **Add `?` to the heading** — do not add `_optional_` text
2. **Include default value in description**

```md
### onError?

Called when an error occurs. Default: errors are thrown.
```

### Combining optional and AvailableFrom

```md
### onError?<AvailableFrom v="4.0.50" />
```

### "Optional since" pattern

```md
### codec?<AvailableFrom v="5.0.0" inline />

Optional since <AvailableFrom v="5.0.0" inline />. Previously required.
```

## Generating preview cards

```bash
cd packages/docs && bun render-cards.ts
```

## Verifying docs compile

```bash
bun run build-docs
```
