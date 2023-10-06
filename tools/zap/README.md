# ZAP - SDL Automation Scan

Run ZAP website security scan for the following SDL Control Testing
- Prevent OS Command Injection
- Perform Input Validation
- Do Not Mix Code and Unvalidated Data 
- Secure Headers or HTTP Security Headers

## Prerequisites

- Docker installed on your machine.
- The ZAP Proxy Docker image You can pull it using 

    `docker pull ghcr.io/zaproxy/zaproxy:stable`.

## Steps to Run

1. **Choose Open API Specifications File:**  
   You need to have an Open API specifications file for the scan stored in same directory as the config

2. **Add Authorization token to the Configuration file**  
   You need to replace the `BEARER_TOKEN` in the `config-auth.prop` file with the required authorization token

3. **Select Configuration Based on SDL Control:**  
   There are different configurations available based on the SDL control:

    - **Prevent OS Command Injection:** Use `configuration-prevent-os-command-injection.conf`
    - **Perform Input Validation:** Use `configuration-perform-input-validation.conf`
    - **Do Not Mix Code and Unvalidated Data:** Use `configuration-do-not-mix-code-and-unvalidated-data.conf`

   Choose the appropriate configuration file for the SDL Control.

4. **Run the Docker Command:**  
   With all the above in place, run the following command, replacing placeholders with your actual values:

   ```bash
   docker run -v [PATH_TO_CONFIG_AND_REPORT]:/zap/wrk/:rw -t ghcr.io/zaproxy/zaproxy:stable zap-api-scan.py -t [OPEN_API_SPEC_FILE] -f openapi -r zap-report.html -z "-c config-auth.prop -addoninstall ascanrulesAlpha -addoninstall sqliplugin -addoninstall ascanrulesBeta -addoninstall pscanrulesAlpha -addoninstall pscanrulesBeta" --hook=zap_custom_hooks.py -c [CONFIGURATION_FILE]

Once the scan is complete, you will find the zap-report.html in the specified configuration and report directory