# Angular Components Repository Overview

> Source: https://github.com/angular/components

## Repository

- **Repo:** https://github.com/angular/components
- **Docs:** https://material.angular.dev
- **Stars:** ~25,000
- **Language:** TypeScript
- **Default branch:** `main`

## Published Packages

| Package | Description |
|---|---|
| `@angular/material` | Material Design UI components for Angular |
| `@angular/cdk` | Component Dev Kit — headless interaction patterns |
| `@angular/aria` | Headless, accessible WAI-ARIA directive collection |
| `@angular/google-maps` | Angular wrapper for Google Maps JS API |
| `@angular/youtube-player` | Angular wrapper for YouTube Player API |

## Quality Bar

High-quality means:
- Internationalized and accessible (a11y first)
- Straightforward, non-confusing APIs
- Behaves correctly across wide use-cases
- Well-tested (unit + integration)
- Customizable within Material Design bounds
- Minimal performance cost
- Clean, documented code

## Browser Support

Most recent two versions of: Chrome (+ Android), Firefox, Safari (+ iOS), Edge.

### Screen Reader Support

- Windows: NVDA + JAWS with FF/Chrome
- macOS: VoiceOver with Safari/Chrome
- iOS: VoiceOver with Safari
- Android: Android Accessibility Suite with Chrome
- Chrome OS: ChromeVox with Chrome

## Support Policy

Follows Angular's release/support policy:
https://angular.dev/reference/releases

## Key Repo Files

| File | Purpose |
|---|---|
| `CODING_STANDARDS.md` | Code style + API design rules |
| `CONTRIBUTING.md` | Contribution workflow, PR guidelines, commit format |
| `DEV_ENVIRONMENT.md` | Local dev setup |
| `FAQ.md` | Frequently asked questions |
| `guides/` | User-facing guides (source for material.angular.dev/guides) |
| `src/material/` | Material component source |
| `src/cdk/` | CDK source |

## Commit Message Format

```
<type>(<package>/<scope>): <subject>

<body>

<footer>
```

Types: `feat`, `fix`, `docs`, `refactor`, `perf`, `test`, `build`, `ci`, `release`

Example:
```
fix(material/button): unable to disable button through binding

Fixes a bug where buttons cannot be disabled through a binding.

Fixes #1234
```
