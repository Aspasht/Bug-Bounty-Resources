# Curl Cookbook
### POST REQUESTS
   #### *Send an Empty POST Request* 
      curl -X POST https://{TargetUrl}
   #### *Send a POST Request with Form Data*
      curl -d 'login=user/email&password=password' -X POST https://{TargetUrl}
   #### *Send a POST Request and Follow a Redirect*
       curl -L -d 'Key=Value' https://{TargetUrl}
   #### *Send a POST Request with JSON Data*
       curl -d '{"Key":"Value","Key":"Value"}' -H 'Content-Type: application/json' https://{TargetUrl}
   #### *Send a POST Request with XML Data*
       curl -d '<user><login>username</login><password>test232</password></user>' -H 'Content-Type: text/xml' https://{TargetUrl}
   #### *Send a POST Request with Plain Text Data*
       curl -d 'Your Text Here' -H 'Content-Type: text/plain' https://{TargetUrl}
   #### *Send a POST Request with Data from a File*
       curl -d '@data.txt' https://{TargetUrl} 
              Note: Remember to put @ {Symbol}                   
   #### *POST a Binary File*
        curl -F 'file=@test.png' https://{TargetUrl}
   #### *POST a Binary File and change Its Filename*
        curl -F 'file=@test.png,filename=newname.png' https://{TargetUrl} # Change Filename
        curl -F 'file=@test.png,type=test.newformat' https://{TargetUrl}  # Change File Format
 ### OTHER USEFUL COMMANDS
    curl -u 'user:password' https://{TargetUrl} # Basic Authentication
    curl -i  https://{TargetUrl}  # Print Response Headers
    curl -A 'Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:60.0) Gecko/20100101 Firefox/60.0' https://{TargetUrl} # Change User Agent Header
    curl -A '' https://{TargetUrl} # Remove User Agent Header
    curl -1 https://{TargetUrl} # Use SSL Version
    
#### Resources
  - https://cheatsheet.dennyzhang.com/cheatsheet-curl-a4
  - https://catonmat.net/cookbooks/curl
  - https://medium.com/@webcrat.tech/curl-cheat-sheet-9487e628968f
