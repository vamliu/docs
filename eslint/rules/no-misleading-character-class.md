---
规则名: no-misleading-character-class
规则类型: problem
---





Unicode includes the characters which are made with multiple code points.
RegExp character class syntax (`/[abc]/`) cannot handle characters which are made by multiple code points as a character; those characters will be dissolved to each code point. For example, `❇️` is made by `❇` (`U+2747`) and VARIATION SELECTOR-16 (`U+FE0F`). If this character is in RegExp character class, it will match to either `❇` (`U+2747`) or VARIATION SELECTOR-16 (`U+FE0F`) rather than `❇️`.

This rule reports the regular expressions which include multiple code point characters in character class syntax. This rule considers the following characters as multiple code point characters.

**A character with combining characters:**

The combining characters are characters which belong to one of `Mc`, `Me`, and `Mn` [Unicode general categories](http://www.unicode.org/L2/L1999/UnicodeData.html#General%20Category).

```js
/^[Á]$/u.test("Á") //→ false
/^[❇️]$/u.test("❇️") //→ false
```

**A character with Emoji modifiers:**

```js
/^[👶🏻]$/u.test("👶🏻") //→ false
/^[👶🏽]$/u.test("👶🏽") //→ false
```

**A pair of regional indicator symbols:**

```js
/^[🇯🇵]$/u.test("🇯🇵") //→ false
```

**Characters that ZWJ joins:**

```js
/^[👨‍👩‍👦]$/u.test("👨‍👩‍👦") //→ false
```

**A surrogate pair without Unicode flag:**

```js
/^[👍]$/.test("👍") //→ false

// Surrogate pair is OK if with u flag.
/^[👍]$/u.test("👍") //→ true
```

## 规则详解

This rule reports the regular expressions which include multiple code point characters in character class syntax.

此规则的 **错误** 代码实例：



```js
/*eslint no-misleading-character-class: error */

/^[Á]$/u
/^[❇️]$/u
/^[👶🏻]$/u
/^[🇯🇵]$/u
/^[👨‍👩‍👦]$/u
/^[👍]$/
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-misleading-character-class: error */

/^[abc]$/
/^[👍]$/u
```

## 禁用建议

You can turn this rule off if you don't want to check RegExp character class syntax for multiple code point characters.
