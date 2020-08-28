# Bug-Bounty-Automation
Bug Bounty/Web App Pentesting Automation with Bash


--------- One Liners ------------

Subdomain Enum : findomain-linux [Output Filename ./domain.com.txt] 
Subdomain Resolve : httpx [Output Filename ./httpx.txt]
Waybackurls : waybackurls [Output Filename ./subdomain.com-waybackurls.txt]

findomain-linux -t $target -o; httpx -l $target.txt -location -status-code -threads 100 -o httpx.txt; cat httpx.txt | sort -u | grep "200" | cut -d " " -f 1 > resolved_active_subdomains.txt; for url in $(cat resolved_active_subdomains.txt); do filename=`echo $url | cut -d "/" -f 3`; echo filename | waybackurls > $filename-waybackurls.txt; done

_____________________________________________________________________________________

Fuzzing : dirsearch
custom-wordlist.txt = common.txt + directory-list-2.3-medium.txt
Extensions Used : php,php.bak,aspx,bak,asp,jsp
Reports Saved in ./subdomain.com.txt

for url in $(cat resolved_active_subdomains.txt); do filename=`echo $url | cut -d "/" -f 3`; echo; echo "Starting Fuzzing on $url, Output Will Be Saved in $filename"; dirsearch -u $url -w /home/sujit/Wordlists/custom-wordlist.txt -e php,php.bak,aspx,bak,asp,jsp -f -t200 --plain-text-report=$filename.txt; done

---------------------------------
