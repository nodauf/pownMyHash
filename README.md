# PownMyHash
A simple script that automates password cracking with hashcat


# Install
```bash
mkdir -p /opt/hashcat/
mkdir -p /opt/dico/
mkdir -p /opt/pmh/stats/
touch /opt/pmh/.pownMyHash.dico
touch /opt/pmh/.training_ntlm.txt
wget https://raw.githubusercontent.com/1mm0rt41PC/pownMyHash/main/pownMyHash.sh -O /opt/pmh/pownMyHash.sh
chmod +x /opt/pmh/pownMyHash.sh
wget https://download.weakpass.com/wordlists/1947/weakpass_3.7z -O /opt/dico/weakpass_3.7z
7x x /opt/dico/weakpass_3.7z
rm /opt/dico/weakpass_3.7z
mv /opt/dico/weakpass* /opt/dico/weakpass.dico
curl https://hashcat.net/hashcat/ 2>/dev/null | grep -E '<a href="([^"]+.7z)' |head -n1 | sed -E 's/[^"]+"([^"]+)"[^\r\n]+/\1/g' | xargs -I '{}'  -t curl 'https://hashcat.net{}' --output /opt/hashcat.7z 2>/dev/null
7z x /opt/hashcat.7z
mv /opt/hashcat* /opt/hashcat/
rm /opt/hashcat.7z
wget https://github.com/NotSoSecure/password_cracking_rules/raw/master/OneRuleToRuleThemAll.rule -O /opt/hashcat/rules/OneRuleToRuleThemAll.rule
wget https://github.com/praetorian-inc/Hob0Rules/raw/master/hob064.rule -O /opt/hashcat/rules/hob064.rule
wget https://github.com/praetorian-inc/Hob0Rules/raw/master/d3adhob0.rule -O /opt/hashcat/rules/d3adhob0.rule
```

# Usage
```
Usage:
  /opt/pmh/pownMyHash.sh <hash-type> <hash-file>
  /opt/pmh/pownMyHash.sh test <dico-to-test> (will be tested against /opt/pmh/.training_ntlm.txt in NTLM)
  TEST_DICO=<dico-to-test> /opt/pmh/pownMyHash.sh <hash-type> <hash-file>

With:
  <hash-type>: The type of the hash (ex:1000 for NTLM, 5500 for NetNTLMv1, 5600 for NetNTLMv2). See hashcat --help
  <hash-file>: The file that contains the hashed passwords

Example:
  /opt/pmh/pownMyHash.sh ntlm myNtlmFile.txt
  /opt/pmh/pownMyHash.sh 1000 myNtlmFile.txt
```
