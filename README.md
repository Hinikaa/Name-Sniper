# Roblox Username Checker

A small Python script that checks a list of Roblox usernames against Roblox's official username validation endpoint and tells you whether each one is available, taken, or censored.

## Features

- Bulk-checks usernames from a text file
- Color-coded terminal output via `colorama`
- Saves available usernames to `valid.txt`
- Handles request errors gracefully

## Requirements

- Python 3.7+
- [`requests`](https://pypi.org/project/requests/)
- [`colorama`](https://pypi.org/project/colorama/)

Install dependencies:

```bash
pip install requests colorama
```

## Usage

1. Create a file named `usernames.txt` in the same directory as the script, with one username per line:

   ```
   coolguy123
   xX_Shadow_Xx
   robloxfan99
   ```

2. Run the script:

   ```bash
   python checker.py
   ```

3. Watch the output in your terminal:

   | Color | Meaning |
   |-------|---------|
   | 🟢 Green | Username is **valid**/available |
   | ⚫ Gray | Username is **taken** |
   | 🔴 Red | Username is **censored**/not allowed |
   | 🟡 Yellow | Unexpected response code or request error |

4. Any valid (available) usernames are automatically appended to `valid.txt`.

## How It Works

The script sends a request to Roblox's public username validation API:

```
https://auth.roblox.com/v1/usernames/validate?Username={username}&Birthday=2000-01-01
```

and interprets the returned `code` field:

| Code | Status |
|------|--------|
| `0`  | Valid / available |
| `1`  | Taken |
| `2`  | Censored / moderated |
| other | Unknown — printed as-is |

## Notes & Disclaimer

- This script relies on an **unofficial, undocumented Roblox endpoint**. Roblox can change or remove it at any time without notice, which may break this script.
- Sending a very high volume of requests in a short time may trigger rate limiting or get your IP temporarily blocked. Adjust the delay in the `time.sleep()` call if you run into issues.
- This project is not affiliated with or endorsed by Roblox Corporation. Use at your own risk and in accordance with [Roblox's Terms of Use](https://en.help.roblox.com/hc/en-us/articles/115004647846).

## License

MIT — feel free to use, modify, and share.
