# Major Tagging Action

Move a major tag to the latest tag

## Usage example

```yml
name: Move a major tag to the latest release

on:
  push:
    tags:
      - v** # Trigger on every tag push

jobs:
  tag:
    name: Move major tag
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: phwt/major-tagging-action@v1
```

## Example behavior

Currently `v1` tag is pointing to the same commit as `v1.0.1` tag:

```bash
> git log --oneline
dd3168d (tag: v1.0.1, tag: v1) fix: add support for 2 digit number
53f0899 (tag: v1.0.0) feat: create `isOdd` method
```

Later, `v1.0.2` tag is created at the latest commit:

```bash
> git commit -am 'feat: create `isEven` method'
> git log --oneline
bc5e6d3 (tag: v1.0.2) feat: create `isEven` method
dd3168d (tag: v1.0.1, tag: v1) fix: add support for 2 digit number
53f0899 (tag: v1.0.0) feat: create `isOdd` method
```

And then the new commit and tag is pushed:

```bash
> git push
> git push --tags
```

The workflow will be triggered and move the `v1` to the latest `v1.x.x` tag (`v1.0.2` tag in this case)

```bash
> git log --oneline
bc5e6d3 (tag: v1.0.2, tag: v1) feat: create `isEven` method
dd3168d (tag: v1.0.1) fix: add support for 2 digit number
53f0899 (tag: v1.0.0) feat: create `isOdd` method
```
