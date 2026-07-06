# Svelte library

This project includes a framework-neutral AI operating layer. Canonical policy, architecture intent, skills, and integrations live under `.ai/`; project facts and vendor-specific adapters are generated.

It is compatible with multiple AI agents when their host supports repository instruction loading, MCP, or manual context attachment. It does not make raw models discover or obey project instructions automatically. The generated project map is a navigation aid, not full semantic code intelligence, and reduced token usage is a design goal rather than a guarantee.

```sh
npm run ai:sync        # regenerate maps, adapters, skills, and MCP config
npm run ai:check       # detect stale or missing generated context
npm run ai:test        # test deterministic governance rules
npm run ai:assess -- --request "change request" --files path1,path2
npm run mcp:project    # start the project MCP over stdio
```

Start with `.ai/manifest.yaml`. `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, Copilot instructions, `PROJECT_MAP.md`, skill adapters, and `.mcp.json` are derived artifacts. See `docs/MCP_CLIENT_SETUP.md` for host integration.

Everything you need to build a Svelte library, powered by [`sv`](https://npmjs.com/package/sv).

Read more about creating a library [in the docs](https://svelte.dev/docs/kit/packaging).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```sh
# create a new project in the current directory
npx sv create

# create a new project in my-app
npx sv create my-app
```

To recreate this project with the same configuration:

```sh
# recreate this project
npx sv@0.16.2 create --template library --no-types --add tailwindcss="plugins:forms,typography" sveltekit-adapter="adapter:vercel" mcp="ide:claude-code+setup:local" --install npm KcevAgent
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```sh
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

Everything inside `src/lib` is part of your library, everything inside `src/routes` can be used as a showcase or preview app.

## Building

To build your library:

```sh
npm pack
```

To create a production version of your showcase app:

```sh
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.

## Publishing

Go into the `package.json` and give your package the desired name through the `"name"` option. Also consider adding a `"license"` field and point it to a `LICENSE` file which you can create from a template (one popular option is the [MIT license](https://opensource.org/license/mit/)).

To publish your library to [npm](https://www.npmjs.com):

```sh
npm publish
```
