# PathX
PathX takes a URL and a string as input, and returns a list of modified URLs with the string appended to the URL path in different ways.

This tool can help you to Identify **Path XSS** and other stuffs.
## Installation
```console
git clone https://github.com/Q0120S/pathx.git
cd pathx
python3 pathx.py -h
```
You can add this tool to your bashrc for ease of use:
```bash
pathx() {                  
python3 /path/to/your/tool/pathx.py "$@"
}
```
## Usage
```bash
python3 pathx.py -h
```
This will display help for the tool. Here are all the switches it supports.
```console
usage: pathx.py [-h] [-u URL] [-l LIST] [-s STRING] [-ne]

Appending string in different ways to a URL path.

options:
  -h, --help            show this help message and exit
  -u URL, --url URL     single target URL.
  -l LIST, --list LIST  target URL file.
  -s STRING, --string STRING
                        string to append to the URL path.
  -ne, --no-ending-slash
                        omit ending slash from URLs
```
## Running PathX
```bash
cat urls.txt | python3 pathx.py -s %22pathx
```
```bash
echo https://google.com/api/XSS/services/test | python3 pathx.py -s %22pathx
```
```bash
python3 pathx.py -l urls.txt -s %22pathx
```
```bash
python3 pathx.py -u https://google.com/api/XSS/services/test -s %22pathx
```
### Output:
```console
https://google.com/api/XSS/services%22pathx/test/
https://google.com/api%22pathx/XSS/services/test/
https://google.com/api/XSS/services/test/%22pathx
https://google.com/api/XSS/services/test%22pathx/
https://google.com/%22pathx/api/XSS/services/test/
https://google.com/api/XSS/%22pathx/services/test/
https://google.com/api/XSS/services/%22pathx/test/
https://google.com/api/XSS%22pathx/services/test/
https://google.com/api/XSS/services/test/%22pathx/
https://google.com/api/%22pathx/XSS/services/test/
```
## Running PathX with no ending slash
```bash
python3 pathx.py -u https://google.com/api/XSS/services/test -s %22pathx -ne
```
### Output:
```console
https://google.com/api/%22pathx/XSS/services/test
https://google.com/api%22pathx/XSS/services/test
https://google.com/api/XSS/services/test/%22pathx
https://google.com/api/XSS/%22pathx/services/test
https://google.com/api/XSS/services%22pathx/test
https://google.com/api/XSS/services/%22pathx/test
https://google.com/api/XSS/services/test%22pathx
https://google.com/api/XSS%22pathx/services/test
https://google.com/%22pathx/api/XSS/services/test
```
