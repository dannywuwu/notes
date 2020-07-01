# [Regex 101](https://regex101.com/)

# Find

```
/cool/
```

- looks for the first instance of `cool`

## Flags

```
/cool/gi
```

### Global `/g`

- looks for all matches

### Insensitive `/i`

- case insensitive

# Character sets `[]`

```
/[cp]ool/
```

- matches `cool` and `pool`

## Exclude ^

```
/[^1]000/
```

- Match everything except for `1` in the first position
- `2000`, `3000` . . . 

## Ranges

```
/[a-g]/
```

- instead of writing [abcdefg] we can specify a range

```
/[a-zA-Z0-9]/
```

- lowercase, uppercase, and numbers

## Repeating Characters

```
/[0-9]+/
```

- match unlimited times, but at least 1

```
/[0-9]{10}/
```

- match 10 times

```
/[0-9]{8,11}/
```

- match between 8 to 11 times

```
/[0-9]{8,}/
```

- match at least 8 times

# Metacharacters

### `\d`

- match any digit character `[0-9]`

### `\w`

- match any word character `[a-zA-Z0-9_]`

### `\s`

- match any whitespace character (spaces, tabs)

### `\t`

- match tab character only

# Special Characters

### `+` one or more

### `\` escape

### `[]` character set

### `[^]` negate in set

### `?` zero or one (optional)

```
/hey?/
```

- he is a match
- hey is a match

### `.` any character (except newline)

```
.+
```

- matches all characters

### `*` zero or more 

# Start/End patterns

```
/^[a-z]{5}$/
```

- Only find a 5 letter word
- ^ ensures front
- $ ensures back - line end

# Alternate Characters

```
/cool|pool/
/(c|p)ool/
```

## `()` groups up Regex

# JavaScript

```js
let reg = /[a-z]/ig
let reg = new RegExp(/[a-z]/, 'ig');
```

# HTML

```html
<input pattern="[a-z]">
```
