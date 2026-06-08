# newdoc

`newdoc` creates a starter LaTeX document that is compatible with
`autodoc`, `docbld`, and `tlc-article`.  It seeds the document source,
`docbld` builder file, layout hooks, version data, signature boilerplate, and
optional shared header/footer, logo, and Test Output Factory files.

The generated document uses the standard autodoc report macros and prints
glossaries by default, matching the current autodoc boilerplate pattern.

## Prerequisites

- [autodoc](https://github.com/Traap/autodoc.git)
- [docbld](https://github.com/Traap/docbld.git)
- [tlc-article](https://github.com/Traap/tlc-article.git)
- A LaTeX distribution such as [MiKTeX](https://miktex.org/download)
- Ruby

## Installation

```bash
cd "$HOME"
git clone git@github.com:Traap/newdoc.git
```

Set `NEWDOCPATH` to the cloned repository and expose the executable from your
shell startup file:

```bash
export NEWDOCPATH="${HOME}/git/newdoc"

newdoc() {
  "${NEWDOCPATH}/newdoc" "$@"
}
```

## Usage

```text
Usage: newdoc --dir=path/to/dir [other options]

OPTIONS
  --dir=path/to/dir              Directory to create.
  --file=fileName                File to create.
  --title='Your Document Title'  Document title to use.

  --type=(one of:) stdCodeReviewDoc stdDesignReviewDoc stdDhfDoc
                   stdTechPlanDoc stdTechReportDoc stdTestPlanDoc
                   stdTestRecordDoc stdTestReportDoc stdToolTestDoc
                   stdUnitTestDoc stdVerTestDoc

  --logo                         Seed document with a logo.
  --shared                       Use shared header and footer data.

  --tof                          Hook into Test Output Factory.

  --help                         Display this help message.
```

When `--type` is omitted, the generated `.tex` file contains an empty document
macro placeholder.  Pass a type when you want the new source to compile without
manual macro selection.

## Examples

```bash
newdoc --dir=report/summary --file=001 --title='Summary' \
  --type=stdTechReportDoc --shared --logo

newdoc --dir=report/test-plan --file=test-plan --title='Test Plan' \
  --type=stdTestPlanDoc --shared --tof

newdoc --dir=report/unit-test --file=unit-test --title='Unit Test Report' \
  --type=stdUnitTestDoc
```

## Generated Files

| Option | Generated files | Destination |
| --- | --- | --- |
| `--dir` | Document directory and `data` directory | `path/to/dir`, `path/to/dir/data` |
| `--file` | Primary `.tex`, `.texx`, change summary, signatures, version, layout, and header/footer files | `path/to/dir`, `path/to/dir/data` |
| `--shared` | Shared project layout and header/footer hooks | `path/to/shared/data` |
| `--logo` | `logo.png` | `path/to/dir/data` |
| `--tof` | `test-output/test-results.tex` | `path/to/dir/test-output` |

## Development

Run the default checks with:

```bash
rake
```

The default task runs RuboCop and a smoke test.  The smoke task creates
`/tmp/newdoc` when needed, regenerates `/tmp/newdoc/smoke`, builds the smoke
document with `docbld deploy` from `/tmp/newdoc`, and leaves the generated
fixture and `/tmp/newdoc/_build/tech-report.pdf` for inspection.
