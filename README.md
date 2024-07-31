# jQuery Version Checker

This repository contains a Python script to check if a website is using an up-to-date version of jQuery. The script scans the provided URL for jQuery scripts and verifies if the version used is either 2.1.1 or 1.12.1.

## Description

The script fetches the HTML content of a given URL, parses it to find all `<script>` tags, and checks if any of them are jQuery scripts. It then fetches the script content and identifies the jQuery version being used. If the version is either 2.1.1 or 1.12.1, it prints "Up to date". Otherwise, it prints "Out of date" along with the detected version.

## Features

- Parses HTML to find jQuery script tags.
- Checks if the jQuery version is up-to-date (2.1.1 or 1.12.1).
- Provides feedback on the jQuery version used.

## Requirements

- Python 3.x
- `requests` library
- `beautifulsoup4` library

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/arifbinekram/Jquery-Checker.git
    cd Jquery-Checker
    ```

2. Install the required libraries:

    ```bash
    pip install requests beautifulsoup4
    ```

## Usage

Run the script with the target URL as an argument:

```bash
python check_jquery_version.py <url>
```

Replace `<url>` with the actual URL you want to check. For example:

```bash
python check_jquery_version.py http://example.com
```

## Example

```sh
python check_jquery_version.py http://example.com
```

This will output whether the jQuery version is up-to-date or not, and print the detected version if it is out-of-date.

## Script Explanation

```python
import requests
import re
from bs4 import BeautifulSoup
import sys

scripts = []

if len(sys.argv) != 2:
    print("Usage: {} url".format(sys.argv[0]))
    sys.exit(0)

tarurl = sys.argv[1]
url = requests.get(tarurl)
soup = BeautifulSoup(url.text, 'html.parser')

for line in soup.find_all('script'):
    newline = line.get('src')
    scripts.append(newline)

for script in scripts:
    if script and "jquery.min" in str(script).lower():
        url = requests.get(script)
        versions = re.findall(r'\d[0-9a-zA-Z._:-]+', url.text)
        if versions:
            if versions[0] == "2.1.1" or versions[0] == "1.12.1":
                print("Up to date")
            else:
                print("Out of date")
                print("Version detected: " + versions[0])
```

### Details

- **Imports**: Imports the necessary libraries for HTTP requests, regular expressions, HTML parsing, and command-line argument handling.
- **Argument Check**: Ensures the script is run with the correct number of arguments.
- **Fetch URL**: Retrieves the HTML content of the target URL.
- **Parse HTML**: Finds all `<script>` tags and extracts their `src` attributes.
- **Check jQuery Version**: Fetches the content of jQuery scripts and checks if the version is up-to-date.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.


Feel free to customize this README further based on your specific requirements or preferences.
