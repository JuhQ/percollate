# percollate

Percollate is a command-line tool to turn web pages as beautifully formatted PDFs.

## Installation

You can install `percollate` globally:

```bash
# using npm
npm install -g percollate

# using yarn
yarn global add percollate
```

To keep the package up-to-date, you can run:

```bash
# using npm, upgrading is the same command as installing
npm install -g percollate

# yarn has a separate command
yarn global upgrade --latest percollate
```

## Usage

> 💡 Run `percollate --help` for a list of available commands. For a particular command, `percollate <command> --help` lists all available options.

### Available commands

| Command           | What it does                                                             |
| ----------------- | ------------------------------------------------------------------------ |
| `percollate pdf`  | Bundles one or more web pages into a PDF                                 |
| `percollate epub` | _Not implemented [yet](https://github.com/danburzo/percollate/issues/8)_ |
| `percollate html` | _Not implemented [yet](https://github.com/danburzo/percollate/issues/7)_ |

### Available options

The `pdf`, `epub`, and `html` commands have these options:

| Option         | What it does                                    |
| -------------- | ----------------------------------------------- |
| `-o, --output` | (**Required**) The path of the resulting bundle |
| `--template`   | Path to a custom HTML template                  |
| `--style`      | Path to a custom CSS                            |

## Examples

### Generating a PDF

To transform a single web page to PDF:

```bash
percollate pdf --output some.pdf https://example.com
```

To bundle _several_ web pages into a single PDF, specify them as separate arguments to the command:

```bash
percollate pdf --output some.pdf https://example.com/page1 https://example.com/page2
```

You can use common Unix commands and keep the list of URLs in a newline-delimited text file:

```bash
cat urls.txt | xargs percollate pdf --output some.pdf
```

### Using a custom HTML template

> ⚠️ TODO add example here

### Using a custom CSS stylesheet

> ⚠️ TODO add example here

### Customizing the page header / footer

> ⚠️ TODO add example here

## How it works

1. Fetch the page(s) using [`got`](https://github.com/sindresorhus/got)
2. [Enhance](./src/enhancements.js) the DOM using [`jsdom`](https://github.com/jsdom/jsdom)
3. Pass the DOM through [`mozilla/readability`](https://github.com/mozilla/readability) to strip unnecessary elements
4. Apply the [HTML template](./templates/default.html) and the [print stylesheet](./templates/default.css) to the resulting HTML
5. Use [`puppeteer`](https://github.com/GoogleChrome/puppeteer) to generate a PDF from the page

## Troubleshooting

On some Linux machines you'll need to [install a few more Chrome dependencies](https://github.com/GoogleChrome/puppeteer/blob/master/docs/troubleshooting.md#chrome-headless-doesnt-launch) before `percollate` works correctly. (_Thanks to @ptica for [sorting it out](https://github.com/danburzo/percollate/issues/19#issuecomment-428496041)_)

## See also

Here are some other projects to check out if you're interested in building books using the browser:

-   [weasyprint](https://github.com/Kozea/WeasyPrint)
-   [bindery.js](https://github.com/evnbr/bindery)
-   [HummusJS](https://github.com/galkahana/HummusJS)
