# EHPT
Labs 

Disable Windows, firewall for public and private network both.
winget install “openssh preview”


Lab 1: Enumeration{
nmap -A -T4 192.168.1.20
host google.com
nslookup google.com
dig google.com
dig axfr @ns1.google.com google.com
dnsenum google.com
dnsrecon -d google.com
fierce --domain google.com
sublist3r -d google.com
}


Lab 2 — (Online Password Cracking)
Hydra{
hydra -l your_windows_username -P passwords.txt 192.168.1.20 ssh
}

Medusa{
medusa -h 192.168.1.20 -u your_windows_username -P passwords.txt -M ssh
}

John the Ripper{
# Combine passwd and shadow files into a crackable format
sudo unshadow /etc/passwd /etc/shadow > myhashes.txt ✅

# Ensure the rockyou wordlist is unzipped and ready to use
sudo gunzip /usr/share/wordlists/rockyou.txt.gz

# Basic attack (Let John auto-detect the format)
john --wordlist=/usr/share/wordlists/rockyou.txt myhashes.txt

# Forced format attack (Use this if John says "No hashes loaded")
john --format=crypt --wordlist=/usr/share/wordlists/rockyou.txt myhashes.txt ✅

# Specific file attack (Targeting just the natsu_hash.txt we created)
john --wordlist=/usr/share/wordlists/rockyou.txt natsu_hash.txt

echo 'natsu:$y$j9T$z01QHLvy19.CaUpX7yvWR0$rbOd131OmRvphUxVmZNRkyMFwJ6dF2boFpRcSAvgLp0' > natsu_hash.txt ✅

john --show myhashes.txt ✅
}

Hash CAT{
Search for MD5 has generator and create a hash for our pass and save it to 
nano target_hash.txt 
hashcat -m 0 -a 0 target_hash.txt /usr/share/wordlists/rockyou.txt
}

OSINT
whoislookup{ 
whois [target_domain.com]
}

Google Dorking {
Open your browser and try these queries to find sensitive files:

site:target.com filetype:pdf (Finds all PDFs)

site:target.com intitle:index.of (Finds exposed directories)

site:target.com "confidential" (Finds documents with specific keywords)
}

The Harvestor{
theHarvester -d dypiu.ac.in -b yahoo
}

Shodan{
Open Shodan and goomi ghoomi
}

ReconNG{
recon-ng
db insert domains
tesla.com
show domains
modules load recon/domains-hosts/google_site_web
options list
run
modules load recon/domains-hosts/brute_hosts
run
show hosts
dashboard
}

ARP Spoofing{
sudo -E ettercap -G
Step-by-Step GUI Lab Guide (Once it opens)
Once the window appears, follow these steps to perform the ARP Spoofing lab:
1. Start Sniffing: Click the Checkmark (top left) to accept the default interface (eth0).
2. Scan for Hosts: Click the Magnifying Glass icon. Wait for the blue bar at the bottom to finish.
3. Open Host List: Click the icon that looks like a list/three lines (next to the magnifying glass).
4. Assign Targets:
    * Find your Router/Gateway IP -> Right-click -> Add to Target 1.
    * Find your Windows IP (192.168.1.20) -> Right-click -> Add to Target 2.
5. Start the Attack:
    * Click the Globe Icon (MITM Menu) at the top.
    * Select ARP Poisoning.
    * Check the box for Sniff remote connections and click OK.


On windows 
arp -a
}






















