# 📘 SolveItSmart Redirects

This simple HTML-based redirector enables deep linking from Apple Books to the Solve It Smart app.

## ❓ Why This Exists

Apple Books does not support direct deep linking using custom URL schemes (e.g., `solveitsmart://`). To work around this, we host an intermediate redirector page on GitHub Pages. When a user taps a link inside the iBook, it redirects through this page and then launches the Solve It Smart app via Safari.

## 🔧 How It Works

The redirector reads a query parameter (`id`) from the URL and constructs a deep link.

### Example

```url
https://yourusername.github.io/solveitsmart-redirects/?id=ABC123
```

Redirects to:

```text
solveitsmart://problem/ABC123
```

If the `id` is missing, the page will display a message.

## 🧪 Local Testing

If you're building Solve It Smart in Xcode, you can use this redirect page to test deep links manually.

### Example Deep Link URLs

You can simulate launching specific problems by visiting URLs like:

```
https://yourusername.github.io/solveitsmart-redirects/?id=001
https://yourusername.github.io/solveitsmart-redirects/?id=002
https://yourusername.github.io/solveitsmart-redirects/?id=003
```

These will trigger the app (if installed) with the corresponding problem ID.

---
