# @ornikar/neverthrow/must-use-result

> Not handling neverthrow result is a possible error because errors could remain unhandleds.
> ⭐️ This rule is included in `plugin:@ornikar/neverthrow/recommended` preset.

## Rule Details

This rule aimed at disallowing `Results` without handling.

Examples of **incorrect** code:

```js
/*eslint @ornikar/neverthrow/must-use-result: error */

// result without unwrapOr, match or any error handler
const result = getResult();
result.map(() => {});

// result used just as parameter
const v = getResult();
externaFunction(v);
```

Examples of **correct** code:

```js
/*eslint @ornikar/neverthrow/must-use-result: error */

const result = getResult();

result.unwrapOr();

// after call a map
const result = getResult();

result.map(() => {}).unwrapOr('');

// handled manually
const result = getResult();

if (result.isErr()) {
  console.error('failure', result.error);
}

if (result.isOk()) {
  console.log('success', result.value);
}
```

## Options

Nothing.

## Implementation

- [Rule source](../../src/rules/must-use-result.ts)
- [Test source](../../tests/rules/must-use-result.ts)
