<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w -->

# How do I Check Port 80 and 443 Usage Before Installing MDSS on Windows and Linux?

## [**Introduction**](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#introduction)

Before installing MDSS, it is crucial to check the availability of ports 80 and 443. If these ports are in use by another application, the MDSS service will not start. This document provides step-by-step instructions to check port 80 and 443 usage on both Windows and Linux systems.

---

## [**Windows**](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#windows)

### [**1. Checking Port 80 and 443 Using PowerShell**](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#1-checking-port-80-and-443-using-powershell)

#### [**Steps:**](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#steps)

1. Open PowerShell as an Administrator.
2. Copy and paste the following command:

3. Interpret the Output:

- If no application is using the ports, you will see an error message like this:

This indicates that port 80 and 443 are available, and you can proceed with the MDSS installation.

- If another application is using the ports, the output will look like this:

This means that httpd.exe is currently using port 80 and 443.

---

### [**2. Checking Port 80 and 443 Using Netstat**](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#2-checking-port-80-and-443-using-netstat)

#### [Steps:](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#steps)

1. Open Command Prompt (CMD) as an Administrator.
2. Run the following commands:

3. Interpret the Output:

- If the ports are in use, you will see an output like this:

- The last column (47752) is the Process ID (PID) of the application using the ports.

4. To identify the application using the PID, run:

Example Output:

This confirms that httpd.exe is using port 80 and 443.

---

## [**Linux**](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#linux)

### [**Checking Port 80 and 443 Using Netstat**](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#checking-port-80-and-443-using-netstat)

#### [Steps:](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#steps)

1. Open a Terminal.
2. Run the following command:

3. Interpret the Output:

- If ports 80 and 443 are in use, you will see an output like this:

** Netstat Command Options Explained: **

- `-t` **→** Show TCP connections
- `-u` **→** Show UDP connections
- `-l` **→** Show Listening ports
- `-p` **→** Show the process name
- `-n` **→** Show numeric addresses instead of resolving hostnames

---

## [**Conclusion**](/docs/mdss/4.4.2/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w#conclusion)

- If ports 80 and 443 are available, you can proceed with the MDSS installation.
- If ports 80 and 443 are in use, you need to stop or reconfigure the conflicting application before installing MDSS.
- Use the provided commands on Windows and Linux to check and troubleshoot port usage effectively.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
