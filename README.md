# BugBounty Commands

## Introduction


I always have to search for commands everytime I start to hunt for bugs.Therefore, I created this repository to list all useful commands of different useful tools. My intention is to make a repo containing all the important commands used for Bug Bounty. 

If you think any important commands were not listed in this repository, feel free contribute. 

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


#### Refrences:
  - https://github.com/dwisiswant0/awesome-oneliner-bugbounty
  - https://github.com/XalfiE/Bug-Bounty-Oneliners
  
