# all  
## close to the flag?  
When you are close to the flag:   
try 0 and O  
translate to the language of the organization country  
encode it in base64  
check pastebin  
if it looks small, bruteforce it  
## encoding  
encode format flag in base64 to know what it looks like if you cross it somewhere...  
base64 decoding output is binary? It could be the flag in image format.  
only decimal ? Think to convert it in hexa!  
Look on https://gchq.github.io/CyberChef  
## obviously  
look the title/hints  
check on a search engine unusual strings  
look (again) the source code comments  
check if there is no similar challenge in a previous CTF, specially in a previous event of the current CTF  
## time  
think about time variable  
if a rand is initialized with time, it's not truly random!  
  
  
# cracking/reverse engineering  
cipher (brute force, be careful, output could be present only in debug) https://github.com/p4-team/ctf/tree/master/2017-09-17-ekoparty/warmup_re  
Ghidra/IDA/snowman/https://binary.ninja/dotPeek  
XOR on weird strings  
strings  
xxd  
pintool fadec0d3.blogspot.fr/2017/04/plaidctf-2017-nomoflo-125.html (or if it's char by char https://github.com/Inshallhack/Write-ups/tree/master/BackdoorCTF-2017/No-Calm)  
search flag format in memory during program execution  
solver angr neolex-security.fr/writeup/stem-ctf-2018-binary-400-re/ or AngryIDA https://github.com/Brandon-Everhart/CTF-Writeups/tree/master/2018/Codegate/Reversing/RedVelvet  
  
# crypto  
XOR  
Caesar  
substitution (with SCBSolver ?)  
Vigenere  
check if uncipher function is not already available  
Is it coordinates?  
cipher = cipher[::-1]  
https://www.lenntech.com/periodic/number/atomic-number.htm  

# exploit/pwn/privesc  
hex rays IDA analysis // test with Hex-Rays Decompiler  
return code of the executable is useful  
understand why we don't have the value we thought  
## blacklist
try unattended char: # $ '  
## buffer overflow  
buffer overflow with big inputs to crash the program  
info functions  
if it's heap overflow, do it on $rsp  
off-by-one  
think to write in an allowed place, like an address in .got (objdump -D)  
ROPgadget or ropper  
with canary, it could be Stack Smashing Protector  
## file  
io file relative path  
execve with a file descriptor still open  
## format  
put negative integers  
printf bug format https://github.com/ShellCollectingClub/backdoor2017/tree/master/Baby_0x41414141  
inject \x00, specially if there is a strncmp !  
inject empty string  
  
# forensics  
binwalk  
compare to a same kind of file  
foremost  
extundelete  
historic (commands, browser)  
strings  
TestDisk to retrieve partition table  
volatility // vol.py -f /cases/Win7SP1x64_emule.img image info and don't hesitate to create a profile  
Wireshark // with build-in export objects or use the TCP follow, check USB device type  
execute VM or disk image  
search tool to read this kind of file  
  
# network  
think about anonymous connection  
wireshark to check if the target doesn't send to me packet that I ignore  
  
# OSINT  
shodan  
virustotal.com  
  
# stega  
## image
gmask.awardspace.info // if image contains a weird rectangle  
steganography -d /tmp/image/output.jpg // not on pgm  
steghide extract -sf low-sodium-bagel.jpeg -p "" // not on gif,pgm,png  
zsteg route.png  // not on gif,jpg,pgm  
stegsolve  
steganabara  
https://29a.ch/photo-forensics/#forensic-magnifier // not on pgm  
tineye.com  
stegcracker the_doge.jpg /root/Desktop/rockyou.txt  
## audio
spek for audio/video // or SonicVisualizer?  
SSTV for audio  
steghide extract -sf toto.wav -p ""  
  
# web  
wrong certificate  
understand what is the goal of the website, use a real mail address to check if that send really an e-mail  
exploit db // try default creds  
Check for files that expose content, such as robots.txt, sitemap.xml, .DS_Store, .git  
extension // main.py, .file.ext.swp, file.ext.swp, file.ext~, #file.ext#, ~file.ext, file.ext.bak, file.ext.tmp, file.ext.old, file.bak, file.tmp, file.old, file.save  
register // try to use an account from another team which registered with a weak password  
source code // read all source code created for the challenge (including HTML, JS and CSS) specially the comments!!  
play with parameters and/or session token //including by adding %00 or %0A  
send a date that doesn't exist like 2018-01-32  
nikto    
XXE  
bypass filter with double encoding  
SSRF  
gobuster  
## htaccess  
method toto or GeT  
display .htaccess or .htpasswd file with a PHP include or CGI or SQL injection load_file   
## OS command injection  
ls;#  
ls;;  
## PHP  
$$variable  
put variable in array var[]  
PATH Windows << becomes *  
think to upload/unzip our webshell in a directory where executable right exist  
PHP filter // php://filter/read=convert.base64-encode/resource=../delete  
use urlencode to bypass  
## SQL  
sqlmap // with burp if tamper doesn't work  
'or 1 --- ou '\n#  // with a sleep if we don't have a visual feedback  
'NoneType' object is not iterable, could be bypass with: OR 1=1 --
## upload
double extension
type MIME
NULL bytes
extension forgotten by blacklist  
