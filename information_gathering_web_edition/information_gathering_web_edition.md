# Information gathering web edition

## WHOIS

| Command                                 | Description                                  |
|-----------------------------------------|----------------------------------------------|
| `export TARGET="domain.tld"`            | Assign target to an environment variable.   |
| `whois $TARGET`                         | WHOIS lookup for the target.                 |

## DNS Enumeration

| Command                                 | Description                                  |
|-----------------------------------------|----------------------------------------------|
| `nslookup $TARGET`                      | Identify the A record for the target domain. |
| `nslookup -query=A $TARGET`             | Identify the A record for the target domain. |
| `dig $TARGET @<nameserver/IP>`          | Identify the A record for the target domain. |
| `dig a $TARGET @<nameserver/IP>`        | Identify the A record for the target domain. |
| `nslookup -query=PTR <IP>`              | Identify the PTR record for the target IP address. |
| `dig -x <IP> @<nameserver/IP>`          | Identify the PTR record for the target IP address. |
| `nslookup -query=ANY $TARGET`           | Identify ANY records for the target domain. |
| `dig any $TARGET @<nameserver/IP>`      | Identify ANY records for the target domain. |
| `nslookup -query=TXT $TARGET`           | Identify the TXT records for the target domain. |
| `dig txt $TARGET @<nameserver/IP>`      | Identify the TXT records for the target domain. |
| `nslookup -query=MX $TARGET`            | Identify the MX records for the target domain. |
| `dig mx $TARGET @<nameserver/IP>`       | Identify the MX records for the target domain. |

## Passive Subdomain Enumeration

| Resource/Command                                                                  | Description                                          |
|-----------------------------------------------------------------------------------|------------------------------------------------------|
| [VirusTotal](https://www.virustotal.com/gui/home/url)                             | VirusTotal                                           |
| [Censys](https://censys.io/)                                                      | Censys                                               |
| [Crt.sh](https://crt.sh/)                                                          | Crt.sh                                               |
| `curl -s https://sonar.omnisint.io/subdomains/{domain} | jq -r '.[]' | sort -u`      | All subdomains for a given domain.                  |
| `curl -s https://sonar.omnisint.io/tlds/{domain} | jq -r '.[]' | sort -u`               | All TLDs found for a given domain.                  |
| `curl -s https://sonar.omnisint.io/all/{domain} | jq -r '.[]' | sort -u`                | All results across all TLDs for a given domain.     |
| `curl -s https://sonar.omnisint.io/reverse/{ip} | jq -r '.[]' | sort -u`               | Reverse DNS lookup on IP address.                   |
| `curl -s https://sonar.omnisint.io/reverse/{ip}/{mask} | jq -r '.[]' | sort -u`        | Reverse DNS lookup of a CIDR range.                 |
| `curl -s "https://crt.sh/?q=${TARGET}&output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u` | Certificate Transparency.                           |
| `cat sources.txt | while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}-${TARGET}";done` | Searching for subdomains and other information on the sources provided in the source.txt list. |

### Sources.txt
```txt
baidu
bufferoverun
crtsh
hackertarget
otx
projecdiscovery
rapiddns
sublist3r
threatcrowd
trello
urlscan
vhost
virustotal
zoomeye
```

# Passive Infrastructure Identification

| Resource/Command                          | Description                                        |
|-------------------------------------------|----------------------------------------------------|
| Netcraft                                  | Netcraft                                           |
| WayBackMachine                            | WayBackMachine                                     |
| WayBackURLs                               | WayBackURLs                                        |
| `waybackurls -dates https://$TARGET > waybackurls.txt` | Crawling URLs from a domain with the date it was obtained. |

# Active Infrastructure Identification

| Resource/Command                          | Description                                    |
|-------------------------------------------|------------------------------------------------|
| `curl -I "http://${TARGET}"`             | Display HTTP headers of the target webserver. |
| `whatweb -a https://www.facebook.com -v` | Technology identification.                     |
| Wappalyzer                                | Wappalyzer                                     |
| `wafw00f -v https://$TARGET`              | WAF Fingerprinting.                            |
| Aquatone                                  | Aquatone                                       |
| `cat subdomain.list aquatone -out ./aquatone -screenshot-timeout 1000` |                                                   |

# Active Subdomain Enumeration

| Resource/Command                                          | Description                                              |
|-----------------------------------------------------------|----------------------------------------------------------|
| HackerTarget                                              | HackerTarget                                             |
| SecLists                                                  | SecLists                                                 |
| `nslookup -type=any -query=AXFR $TARGET nameserver.target.domain` | Zone Transfer using Nslookup against the target domain and its nameserver. |
| `gobuster dns -q -r "${NS}" -d "${TARGET}" -w "${WORDLIST}" -p ./patterns.txt -o "gobuster_${TARGET}.txt"` | Bruteforcing subdomains. |

# Virtual Hosts

| Resource/Command                                         | Description                                              |
|----------------------------------------------------------|----------------------------------------------------------|
| `curl -s http://192.168.10.10 -H "Host: randomtarget.com"` | Changing the HOST HTTP header to request a specific domain. |
| `cat ./vhosts.list while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://<IP address> -H "HOST: ${vhost}.target.domain"` | Bruteforcing for possible virtual hosts on the target domain. |
| `ffuf -w ./vhosts -u http://<IP address> -H "HOST: FUZZ.target.domain" -fs 612` | Bruteforcing for possible virtual hosts on the target domain using ffuf. |

# Crawling

| Resource/Command                          | Description                                              |
|-------------------------------------------|----------------------------------------------------------|
| ZAP                                       | ZAP                                                      |
| `ffuf -recursion -recursion-depth 1 -u http://192.168.10.10/FUZZ -w /opt/useful/SecLists/Discovery/Web-Content/` | Discovering files and folders that cannot be spotted by browsing the website. |
