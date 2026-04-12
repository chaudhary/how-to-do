---
layout: post
title: "Regex Cheat Sheet: 20 Patterns You'll Use Constantly"
date: 2026-04-11
category: Tech / Dev
description: "A practical regex reference with 20 patterns for emails, URLs, numbers, dates, and common text processing tasks."
reading_time: 6
related_tool: /tools/regex-tester
related_tool_name: Regex Tester
---

Regular expressions are one of those tools that feel impossible until they click, then become indispensable. Here are 20 patterns that cover the vast majority of real-world use cases.

## The Basics First

| Pattern | Matches |
|---------|---------|
| `.` | Any single character |
| `\d` | Any digit (0-9) |
| `\w` | Any word character (a-z, A-Z, 0-9, _) |
| `\s` | Any whitespace (space, tab, newline) |
| `^` | Start of string |
| `$` | End of string |
| `*` | Zero or more of previous |
| `+` | One or more of previous |
| `?` | Zero or one of previous |
| `{n,m}` | Between n and m of previous |
| `[abc]` | Any character in the set |
| `[^abc]` | Any character NOT in the set |
| `(...)` | Capture group |
| `\|` | OR operator |

## The 20 Patterns

### 1. Email address (simple)
```
[\w.+-]+@[\w-]+\.[\w.]+
```
Not RFC-compliant (nothing is, practically), but catches 99% of real emails.

### 2. URL
```
https?://[\w\-.]+(:\d+)?(/[\w\-./?%&=]*)?
```

### 3. Phone number (Indian)
```
(\+91[\s-]?)?[6-9]\d{9}
```

### 4. Phone number (US)
```
(\+?1[\s-]?)?\(?\d{3}\)?[\s-]?\d{3}[\s-]?\d{4}
```

### 5. IP address (IPv4)
```
\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b
```

### 6. Date (YYYY-MM-DD)
```
\d{4}-(?:0[1-9]|1[0-2])-(?:0[1-9]|[12]\d|3[01])
```

### 7. Date (DD/MM/YYYY)
```
(?:0[1-9]|[12]\d|3[01])/(?:0[1-9]|1[0-2])/\d{4}
```

### 8. Time (24-hour)
```
(?:[01]\d|2[0-3]):[0-5]\d(:[0-5]\d)?
```

### 9. Integer
```
-?\d+
```

### 10. Decimal number
```
-?\d+\.?\d*
```

### 11. Hex color code
```
#([0-9a-fA-F]{3}|[0-9a-fA-F]{6})\b
```

### 12. HTML tag
```
</?[\w]+[^>]*>
```

### 13. Whitespace trimming
```
^\s+|\s+$
```
Use with replace to trim leading/trailing whitespace.

### 14. Duplicate words
```
\b(\w+)\s+\1\b
```
Finds "the the", "is is", etc.

### 15. PAN card (India)
```
[A-Z]{5}\d{4}[A-Z]
```

### 16. PIN code (India)
```
\b[1-9]\d{5}\b
```

### 17. ZIP code (US)
```
\b\d{5}(-\d{4})?\b
```

### 18. Password strength (minimum 8 chars, 1 upper, 1 lower, 1 digit)
```
^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$
```

### 19. Extract domain from URL
```
https?://([^/]+)
```
Capture group 1 gives you the domain.

### 20. CSV value parsing
```
(?:^|,)("(?:[^"]*"")*[^"]*"|[^,]*)
```

## Tips for Writing Regex

1. **Start simple, add complexity.** Get a basic pattern working, then handle edge cases.
2. **Use non-capturing groups** `(?:...)` when you don't need to extract the match.
3. **Be specific.** `\d{4}` is better than `\d+` when you know exactly 4 digits are expected.
4. **Test with real data.** Regex that works on examples can fail on production data. Test with messy, real-world input.
5. **Don't parse HTML with regex.** For anything beyond simple tag matching, use a proper HTML parser.
6. **Comment complex patterns.** Most regex engines support verbose mode where you can add comments.

## When NOT to Use Regex

- Parsing nested structures (HTML, JSON, XML). Use a parser.
- Complex validation that would be clearer as procedural code.
- When a simple `string.contains()` or `string.startsWith()` would do.

Regex is a scalpel. Use it when you need precision. Don't use it when a butter knife works fine.
