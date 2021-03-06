# Sourcegraph extension manifest - package.json

Sourcegraph extensions use a `package.json` file for metadata and configuration.

## Fields

Name | Required | Type | Details
---- |:--------:| ---- | -------
`name` | ✔️ | `string` | Extension identifier: all lowercase, alphanumeric with hyphens and underscores.
`title` | ✔️ | `string`| The name displayed in the extension registry. Can be used to indicate a [work-in-progress extension](publishing.md#wip-extensions).
`description` | ✔️ | `string` | The extension's description, which summarizes the extension's purpose and features.
`version` | | `string` | [Semantic versioning](https://semver.org/) format.
`publisher` | ✔️ | `string` | Your [Sourcegraph username](development_environment#sourcegraph-com-account-and-the-sourcegraph-cli) (or the name of an organization you're a member of)
`license` | | `string` | The type of license chosen.
`main` | | `string` | Path to the transpiled JavaScript file for your extension.
`contributes` | | `object` | An object describing the contributions (features) this extension provides.
[`activationEvents`](activation.md) | ✔️ | `array` | A list of events that cause this extension to be activated.
`dependencies` | | `object` | npm dependencies.
`devDependencies` | | `object` | npm dependencies needed for development.
`scripts` | ✔️ | `object` | npm's scripts with Sourcegraph specific entries such as `sourcegraph:prepublish`.
`browserslist` | | `string` | Modern list of browsers for build tools to target when transpiling.
`repository` | | `object` | npm field for the repository location.

See the [npm package.json documentation](https://docs.npmjs.com/creating-a-package-json-file) for other fields.

**Note:** Including the `repository` field is recommended so anyone can follow the link from the extension detail page to view the source code.

```json
"repository": {
  "type": "git",
  "url": "https://github.com/sourcegraph/sourcegraph-codecov.git"
}
```

## Example

Here is an example `package.json` created by the [Sourcegraph extension creator](creating.md#creating-an-extension-the-easy-way).

```json
{
  "name": "my-extension",
  "title": "WIP: My extension",
  "description": "An awesome Sourcegraph extension",
  "publisher": "your-sourcegraph-username",
  "activationEvents": [
    "*"
  ],
  "contributes": {
    "actions": [
      {}
    ],
    "menus": {
      "editor/title": [],
      "commandPalette": []
    },
    "configuration": {}
  },
  "version": "0.0.0-DEVELOPMENT",
  "license": "MIT",
  "main": "dist/my-extension.js",
  "scripts": {
    "tslint": "tslint -p tsconfig.json './src/**/*.ts'",
    "typecheck": "tsc -p tsconfig.json",
    "build": "parcel build --out-file dist/my-extension.js src/my-extension.ts",
    "serve": "parcel serve --no-hmr --out-file dist/my-extension.js src/my-extension.ts",
    "watch:typecheck": "tsc -p tsconfig.json -w",
    "watch:build": "tsc -p tsconfig.dist.json -w",
    "sourcegraph:prepublish": "npm run build"
  },
  "browserslist": [
    "last 1 Chrome versions",
    "last 1 Firefox versions",
    "last 1 Edge versions",
    "last 1 Safari versions"
  ],
  "devDependencies": {
    "@sourcegraph/tsconfig": "^3.0.0",
    "@sourcegraph/tslint-config": "^12.0.0",
    "parcel-bundler": "^1.10.3",
    "sourcegraph": "^19.0.3",
    "tslint": "^5.11.0",
    "typescript": "^3.1.6"
  }
}
```
