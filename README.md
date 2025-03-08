🚀 OSINT Tool (Name, Location, Phone, Email, IP Search) for Termux

यह Python OSINT Tool आपको किसी भी व्यक्ति की बेसिक जानकारी खोजने में मदद करेगा:

✅ नाम से लोकेशन, सोशल मीडिया, कॉलेज, स्कूल खोजें
✅ फोन नंबर से देश और वैधता जांचें
✅ ईमेल से डेटा लीक की जानकारी पाएं
✅ IP एड्रेस से लोकेशन और सिक्योरिटी स्कैन करें
✅ Google, Shodan और Dark Web से जानकारी निकालें


---

📌 Step 1: Termux में Required Packages Install करें

pkg update && pkg upgrade -y
pkg install python git curl -y
pip install requests beautifulsoup4 whois phonenumbers google shodan pyfiglet termcolor




📌 Step 2: Python OSINT Tool Script बनाएं

1️⃣ Script File बनाएं:

nano osint_advanced.py

2️⃣ अब नीचे दिया गया Code कॉपी-पेस्ट करें:


---

🎯 Advanced OSINT Python Script

import requests
import whois
import phonenumbers
import json
import os
from bs4 import BeautifulSoup
from googlesearch import search
import shodan
import pyfiglet
from termcolor import colored

# 🔹 Heading Banner
def banner():
    print(colored(pyfiglet.figlet_format("OSINT Tool"), "cyan"))

# 🔹 Name Lookup (Google & Social Media Search)
def name_lookup(name):
    print("\n[+] Searching for:", name)
    search_queries = [
        f'"{name}" site:facebook.com',
        f'"{name}" site:linkedin.com',
        f'"{name}" site:instagram.com',
        f'"{name}" site:twitter.com',
        f'"{name}" site:github.com',
        f'"{name}" site:zoominfo.com',
    ]
    for query in search_queries:
        print(f"\n[🔍] Searching: {query}")
        try:
            for j in search(query, num=5, stop=5, pause=5):
                print(f"  - {j}")
        except Exception as e:
            print(f"[!] Google Search Blocked: {str(e)}")

# 🔹 Phone Number Lookup
def phone_lookup(number):
    try:
        parsed_number = phonenumbers.parse(number, None)
        print("\n[+] Phone Number Information:")
        print(f"  - Country: {phonenumbers.region_code_for_number(parsed_number)}")
        print(f"  - Valid: {phonenumbers.is_valid_number(parsed_number)}")
    except Exception as e:
        print(f"[!] Error in phone lookup: {str(e)}")

# 🔹 Website WHOIS & Security Scan
def website_lookup(domain):
    try:
        domain_info = whois.whois(domain)
        print("\n[+] Website Information:")
        print(f"  - Domain Name: {domain_info.domain_name}")
        print(f"  - Registrar: {domain_info.registrar}")
        print(f"  - Expiry Date: {domain_info.expiration_date}")
        print(f"  - Name Servers: {domain_info.name_servers}")
    except Exception as e:
        print(f"[!] Error in website lookup: {str(e)}")

# 🔹 IP Address Geolocation
def ip_lookup(ip):
    try:
        response = requests.get(f"http://ip-api.com/json/{ip}")
        data = response.json()
        print("\n[+] IP Address Information:")
        print(f"  - Country: {data['country']}")
        print(f"  - City: {data['city']}")
        print(f"  - ISP: {data['isp']}")
        print(f"  - Latitude: {data['lat']}, Longitude: {data['lon']}")
    except Exception as e:
        print(f"[!] Error in IP lookup: {str(e)}")

# 🔹 Shodan API Lookup (Vulnerability Check)
def shodan_lookup(ip):
    SHODAN_API_KEY = "YOUR_SHODAN_API_KEY"  # Get API Key from Shodan.io
    api = shodan.Shodan(SHODAN_API_KEY)
    try:
        host = api.host(ip)
        print("\n[+] Shodan IP Information:")
        print(f"  - Organization: {host.get('org', 'N/A')}")
        print(f"  - Open Ports: {host.get('ports', [])}")
    except Exception as e:
        print(f"[!] Error in Shodan lookup: {str(e)}")

# 🔹 Dark Web Search (Leaks Check)
def dark_web_search(query):
    print("\n[+] Searching Dark Web:")
    try:
        search_results = search(f"site:pastebin.com {query}", num=5, stop=5, pause=5)
        for url in search_results:
            print(f"  - {url}")
    except Exception as e:
        print(f"[!] Google Search Blocked: {str(e)}")

# 🔹 Main Menu
def main():
    banner()
    print("1. Name Lookup (Google & Social Media)")
    print("2. Phone Number Lookup")
    print("3. Website WHOIS & Security Scan")
    print("4. IP Address Lookup")
    print("5. Dark Web Search")
    print("6. Shodan Vulnerability Check")

    choice = input("\nSelect an option (1-6): ").strip()

    if choice == "1":
        name = input("Enter Name: ").strip()
        name_lookup(name)

    elif choice == "2":
        number = input("Enter Phone Number: ").strip()
        phone_lookup(number)

    elif choice == "3":
        domain = input("Enter Website Domain: ").strip()
        website_lookup(domain)

    elif choice == "4":
        ip = input("Enter IP Address: ").strip()
        ip_lookup(ip)

    elif choice == "5":
        query = input("Enter Search Query for Dark Web: ").strip()
        dark_web_search(query)

    elif choice == "6":
        ip = input("Enter IP Address for Shodan Scan: ").strip()
        shodan_lookup(ip)

    else:
        print("Invalid choice!")

if __name__ == "__main__":
    main()


---

📌 Step 3: स्क्रिप्ट को रन करें

1️⃣ स्क्रिप्ट को सेव करें:

CTRL + X, फिर Y, फिर ENTER दबाएं।
2️⃣ स्क्रिप्ट को Executable बनाएं:


chmod +x osint_advanced.py

3️⃣ स्क्रिप्ट को रन करें:

python osint_advanced.py


---

✅ अब आप क्या कर सकते हैं?

✅ नाम से पूरी जानकारी निकाल सकते हैं (सोशल मीडिया, वेबसाइट्स, स्कूल, कॉलेज)
✅ फोन नंबर से देश, वैधता, और डेटा लीक खोज सकते हैं
✅ IP Address से लोकेशन और सिक्योरिटी चेक कर सकते हैं
✅ डार्क वेब पर डेटा लीक खोज सकते हैं
✅ शोडान API से Vulnerability Scan कर सकते हैं

