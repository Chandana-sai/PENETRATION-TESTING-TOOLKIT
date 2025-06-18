# PENETRATION-TESTING-TOOLKIT

COMPANY : CODTECH IT SOLUTIONS

NAME : PURLLA CHANDANA SAI PRIYANKA

INTERN ID :CT06DM729

DOMAIN :CYBER SECURITY AND ETHICAL HACKING

DURATION :6 WEEKS

MENTOR : NEELA SANTOSH

OUTPUT:
![Screenshot (4)](https://github.com/user-attachments/assets/45eeec66-9530-4082-a348-bb8127e8e41c)

DESCRIPTION:

🛡️ Penetration Testing Toolkit – PyCharm Code Overview
This Penetration Testing Toolkit is a modular Python project, developed and maintained in PyCharm, aimed at automating the detection of common web vulnerabilities such as SQL Injection (SQLi) and Cross-site Scripting (XSS). The toolkit uses Python’s standard libraries along with requests and BeautifulSoup to simulate attack scenarios and analyze responses for vulnerabilities.

🔧 Development Environment: PyCharm
IDE: PyCharm Community or Professional Edition

Language: Python 3.x

Project Type: Standalone Python application

Dependencies: Managed via requirements.txt

txt
Copy
Edit
requests
beautifulsoup4
📁 Directory and File Structure
graphql
Copy
Edit
penetration-testing-toolkit/
│
├── scanner.py           # 🔍 Main vulnerability scanning logic
├── utils.py             # 🔧 Helper functions (optional, e.g., payloads, HTML parsing)
├── payloads.py          # 💣 Predefined SQLi and XSS payloads
├── requirements.txt     # 📦 Project dependencies
├── README.md            # 📄 Documentation
└── logs/                # 📂 Output logs of scans (optional)
🔍 Core Components (Code Description)
✅ scanner.py
Purpose: This is the main entry point for the vulnerability scanner.

Main Functions:

scan_url(url): Orchestrates the full scanning process.

get_forms(url): Fetches and parses all forms using BeautifulSoup.

get_form_details(form): Extracts action, method, and input fields.

submit_form(form_details, url, payload): Submits payloads into form fields using either GET or POST.

analyze_response(response, payload): Checks if the payload appears in the response (for XSS) or causes errors/logical anomalies (for SQLi).

✅ payloads.py
Purpose: Stores lists of payloads for injection.

python
Copy
Edit
SQLI_PAYLOADS = [
    "' OR '1'='1",
    "'; DROP TABLE users; --",
    '" OR "1"="1'
]

XSS_PAYLOADS = [
    "<script>alert('XSS')</script>",
    '"><img src=x onerror=alert(1)>'
]
✅ utils.py (Optional)
Purpose: Utility functions for reusability.

Examples:

Logging

URL normalization

Input sanitization

Response differencing

🧪 How It Works (Code Workflow)
URL Input: A list of target URLs is provided (hardcoded or via command-line).

Form Discovery: HTML content is parsed to extract all <form> tags.

Payload Injection: All text-type input fields are tested using SQLi and XSS payloads.

Form Submission: Payloads are submitted via the appropriate HTTP method.

Vulnerability Detection: Responses are inspected for signs of reflection, unfiltered input, or anomalies.

Reporting: Results are printed in the terminal and optionally saved in a log file.

🛡️ Sample Code Snippet – Form Submission Logic
python
Copy
Edit
def submit_form(form_details, url, payload):
    target_url = urljoin(url, form_details["action"])
    data = {}
    
    for input in form_details["inputs"]:
        if input["type"] == "text":
            data[input["name"]] = payload
        else:
            data[input["name"]] = input.get("value", "")

    if form_details["method"] == "post":
        return requests.post(target_url, data=data)
    else:
        return requests.get(target_url, params=data)
📤 Output Example
bash
Copy
Edit
[+] Scanning http://testphp.vulnweb.com for vulnerabilities...
[!!] SQL Injection vulnerability detected with payload: ' OR '1'='1
[!!] XSS vulnerability detected with payload: <script>alert('XSS')</script>
[✓] Scan complete.
🧰 How to Run in PyCharm
Clone or open the project in PyCharm.

Create a virtual environment (PyCharm will suggest this).

Install dependencies using the PyCharm terminal:

bash
Copy
Edit
pip install -r requirements.txt
Run scanner.py using the green play button or right-click → Run.

Observe results in the run terminal pane.

🔐 Disclaimer
This tool is intended for educational and ethical testing only. Only use it against systems you own or have explicit permission to test.

