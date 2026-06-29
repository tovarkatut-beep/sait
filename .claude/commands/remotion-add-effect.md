---
name: add-effect
description: Add a new effect to @remotion/effects, including implementation, package exports, docs, demos, preview images, Remotion skill updates, tests, formatting, and builds.
---

# Add a new `@remotion/effects` effect

Use this skill when adding a new effect to `@remotion/effects`.

## 1. Pick the effect shape

- Prefer the WebGL2 backend for new effects. Use 2D only when WebGL cannot express the effect.
- Use a single file at `packages/effects/src/<effect-name>.ts` for simple effects.
- Use a folder at `packages/effects/src/<effect-name>/` plus a top-level re-export file when the effect needs multiple shaders, runtime helpers, or multiple files.
- Follow naming already used by the package:
  - File/subpath: kebab-case (`chromatic-aberration`)
  - Function: camelCase (`chromaticAberration`)
  - Type: PascalCase params (`ChromaticAberrationParams`)
  - Effect type string: `remotion/<kebab-case-name>`

## 2. Implement the effect

In the effect file:

- Import `SequenceSchema` and `Internals` from `remotion`.
- Use `const {createEffect, createWebGL2ContextError} = Internals;`.
- Define defaults as `const` values.
- Define a schema with `satisfies SequenceSchema`; these fields appear in Studio visual editing.
- Export the params type.
- Resolve defaults in a `resolve()` helper.
- Validate params using helpers from:
  - `packages/effects/src/validate-effect-param.ts`
  - `packages/effects/src/color-utils.ts`
- Throw `createWebGL2ContextError('<effect name> effect')` if WebGL2 cannot be acquired.
- Set `documentationLink` to `https://www.remotion.dev/docs/effects/<slug>`.
- Include every resolved parameter in `calculateKey()`.

For WebGL2 effects, use this general structure:

```ts
import type {SequenceSchema} from 'remotion';
import {Internals} from 'remotion';
import {assertOptionalFiniteNumber, validateUnitInterval} from './color-utils.js';
import {assertEffectParamsObject} from './validate-effect-param.js';

const {createEffect, createWebGL2ContextError} = Internals;

const DEFAULT_AMOUNT = 1 as const;

const myEffectSchema = {
	amount: {
		type: 'number',
		min: 0,
		max: 1,
		step: 0.01,
		default: DEFAULT_AMOUNT,
		description: 'Amount',
	},
} as const satisfies SequenceSchema;

export type MyEffectParams = {
	readonly amount?: number;
};

type MyEffectResolved = {
	amount: number;
};

const resolve = (p: MyEffectParams): MyEffectResolved => ({
	amount: p.amount ?? DEFAULT_AMOUNT,
});

const validateMyEffectParams = (params: MyEffectParams): void => {
	assertEffectParamsObject(params, 'My effect');
	assertOptionalFiniteNumber(params.amount, 'amount');
	validateUnitInterval(params.amount ?? DEFAULT_AMOUNT, 'amount');
};

export const myEffect = createEffect<MyEffectParams, unknown>({
	type: 'remotion/my-effect',
	label: 'My Effect',
	documentationLink: 'https://www.remotion.dev/docs/effects/my-effect',
	backend: 'webgl2',
	calculateKey: (params) => {
		const r = resolve(params);
		return `my-effect-${r.amount}`;
	},
	schema: myEffectSchema,
	validateParams: validateMyEffectParams,
});
```

Look at existing WebGL2 effects such as `halftone.ts`, `blur/blur-runtime.ts`, `chromatic-aberration/chromatic-aberration-runtime.ts`, and `wave/wave-runtime.ts` before adding new helpers.

## 3. Register package entry points

Update:

- `packages/effects/bundle.ts` — add the new `src/<effect-name>.ts` entrypoint.
- `packages/effects/package.json`:
  - Add `exports["./<effect-name>"]`.
  - Add the `typesVersions` entry.

## 4. Add tests

Update `packages/effects/src/test/effect-params.test.ts`:

- Import the new effect.
- Add it to the documentation link test.
- Test default params when all fields are optional.
- Test invalid values and exact error substrings.
- Test that meaningful params produce distinct `effectKey` values.

Run:

```bash
cd packages/effects
bun test src/test
bunx turbo make --filter="@remotion/effects"
```

## 5. Add docs

Create `packages/docs/docs/effects/<effect-name>.mdx`.

Follow existing effect pages:

- Frontmatter: `slug`, `title`, `sidebar_label`, `crumb: '@remotion/effects'`.
- Add `image:` only after running `bun render-cards.ts`.
- H1: `# effectName()<AvailableFrom v="..." />`.
- Include `_Part of the [@remotion/effects](/docs/effects/api) package._`.
- Add a short description.
- Add `<EffectsDemo type="effects-<effect-name>" />`.
- Add a twoslash example with `title="MyComp.tsx"`.
- Document each option as its own `###` heading, using `?` for optional parameters.
- Add a `disabled?` section.
- Add a See also section.

Update:

- `packages/docs/sidebars.ts` — add `'effects/<effect-name>'` in alphabetical order.
- `packages/docs/docs/effects/table-of-contents.tsx` — add a card in the right category.

Use the `writing-docs` skill for documentation wording.

## 6. Add the interactive docs demo

Create `packages/docs/components/effects/effects-<effect-name>-preview.tsx`.

Register the demo in `packages/docs/components/effects-demos/registry.ts`.

## 7. Add and render the table-of-contents preview composition

Add a `Still` to `packages/docs/src/remotion/Root.tsx` under the `effect-previews` folder, then render:

```bash
bunx remotion still src/remotion/entry.ts effects-my-effect-preview static/img/effects-my-effect-preview.png --overwrite --image-format=png
```

## 8. Generate docs card

```bash
cd packages/docs
bun render-cards.ts
```

## 9. Update the Remotion skill

Update `packages/skills/skills/remotion/SKILL.md`:

- Add `effectName()` to the `Available effects:` line under `## Visual and pixel effects`.
- Keep the list sorted in the same order as `packages/docs/docs/effects/table-of-contents.tsx`.

## 10. Format, build, and verify

```bash
cd packages/effects
bunx oxfmt src --write
cd ../..
bun run build
bun run formatting
```

## Common pitfalls

- Do not forget `package.json` `exports` and `typesVersions`.
- Do not forget `bundle.ts`.
- Do not forget to update the top-level available effects list in `packages/skills/skills/remotion/SKILL.md`.
- Do not leave temporary render entry points in `packages/docs/src/remotion`.
- Do not use a hand-written SVG for the effect TOC preview.
- Preserve alpha unless the effect intentionally changes it.
- For pixel math, be aware canvases store premultiplied alpha.
