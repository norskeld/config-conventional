# @nrsk/config-conventional

> Customised and relaxed [@commitlint/config-conventional].

## Getting started

```sh
npm i -D @commitlint/cli @nrsk/config-conventional
```

## Rules

> Note: The following rules are considered problems and will yield a non-zero exit code when not met.

### type-enum

- **condition**: `type` is in `value`
- **rule**: `always`
- **level**: `error`
- **value**: `[build, chore, ci, docs, feat, fix, perf, refactor, revert, style, test]`

```sh
echo "foo: some message"  # fails
echo "fix: some message"  # passes
```

### type-case

- **condition**: `type` is in case `value`
- **rule**: `always`
- **level**: `error`
- **value**: `'lowerCase'`

```sh
echo "FIX: some message"  # fails
echo "fix: some message"  # passes
```

### type-empty

- **condition**: `type` is empty
- **rule**: `never`
- **level**: `error`

```sh
echo ": some message".    # fails
echo "fix: some message"  # passes
```

### scope-case

- **condition**: `scope` is in case `value`
- **rule**: `always`
- **level**: `error`
- **value**: `'lowerCase'`

```sh
echo "fix(SCOPE): some message"  # fails
echo "fix(scope): some message"  # passes
```

### subject-case

- **condition**: `subject` is one of `[sentence-case, start-case, pascal-case, upper-case]`
- **rule**: `never`
- **level**: `error`

```sh
echo "fix(SCOPE): Some message"  # fails
echo "fix(SCOPE): Some Message"  # fails
echo "fix(SCOPE): SomeMessage"   # fails
echo "fix(SCOPE): SOMEMESSAGE"   # fails
echo "fix(scope): some message"  # passes
echo "fix(scope): some Message"  # passes
```

### subject-empty

- **condition**: `subject` is empty
- **rule**: `never`
- **level**: `error`

```sh
echo "fix:"               # fails
echo "fix: some message"  # passes
```

### subject-full-stop

- **condition**: `subject` ends with `value`
- **rule**: `never`
- **level**: `error`
- **value**: `'.'`

```sh
echo "fix: some message."  # fails
echo "fix: some message"   # passes
```

### header-max-length

- **condition**: `header` has `value` or less characters
- **rule**: `always`
- **level**: `error`
- **value**: `100`

```sh
echo "fix: some message that is way too long..."  # fails
echo "fix: some message"                          # passes
```

### footer-leading-blank

- **condition**: `footer` should have a leading blank line
- **rule**: `always`
- **level**: `warning`

```sh
# fails
echo "fix: some message
BREAKING CHANGE: It will be significant"

# passes
echo "fix: some message

BREAKING CHANGE: It will be significant"
```

### footer-max-line-length

> `512` characters is actually way more than you would usually need, but in my case
> smaller value was breaking my semantic-release workflow, because release notes generated
> by semantic-release were way too long, so my workflow kept failing.

- **condition**: each line in `footer` has `value` or less characters
- **rule**: `always`
- **level**: `error`
- **value**: `512`

```sh
# fails
echo "fix: some message

BREAKING CHANGE: footer with multiple lines
has a message that is way too long and will break the line rule 'line-max-length' by several characters"

# passes
echo "fix: some message

BREAKING CHANGE: footer with multiple lines
but still no line is too long"
```

### body-leading-blank

- **condition**: `body` should have a leading blank line
- **rule**: `always`
- **level**: `warning`

```sh
# warning
echo "fix: some message
body"

# passes
echo "fix: some message

body"
```

### body-max-line-length

- **condition**: `body` each line has `value` or less characters
- **rule**: `always`
- **level**: `error`
- **value**: `512`

```sh
# fails
echo "fix: some message

body with multiple lines
has a message that is way too long and will break the line rule 'line-max-length' by several characters"

# passes
echo "fix: some message

body with multiple lines
but still no line is too long"
```

## License

[Unlicense](LICENSE). Do whatever you want!

[@commitlint/config-conventional]: https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional
