<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/how-do-I-check-port-80-and-443-usage-before-installing-mdss-on-w -->

# How do I Check Port 80 and 443 Usage Before Installing MDSS on Windows and Linux?

## **Introduction**

Before installing MDSS, it is crucial to check the availability of ports 80 and 443. If these ports are in use by another application, the MDSS service will not start. This document provides step-by-step instructions to check port 80 and 443 usage on both Windows and Linux systems.

---

## **Windows**

### **1. Checking Port 80 and 443 Using PowerShell**

#### **Steps:**

1. Open PowerShell as an Administrator.
2. Copy and paste the following command:

![](https://uploads.developerhub.io/prod/k8zL/n6xwhywictmnl9b7rqcltw6aboud5czhhi2qvurn2t3pejrgmj5dfsqhvgpw4wob.png)

3. Interpret the Output:

- If no application is using the ports, you will see an error message like this:

![](https://uploads.developerhub.io/prod/k8zL/6zsj80k10ibewra8zdq4dj4qu8uj9b4zcd16u8aexhf3xr22cnrgg65v1njkvq0r.png)

This indicates that port 80 and 443 are available, and you can proceed with the MDSS installation.

- If another application is using the ports, the output will look like this:

![](https://uploads.developerhub.io/prod/k8zL/qqpq4q0l5ipkpdegs89sqvco0a83wpqq8cvzx0u3900iziwsqau8d3t82720w86v.png)

This means that httpd.exe is currently using port 80 and 443.

---

### **2. Checking Port 80 and 443 Using Netstat**

#### Steps:

1. Open Command Prompt (CMD) as an Administrator.
2. Run the following commands:

![](https://uploads.developerhub.io/prod/k8zL/01qqqsyhpwe5j0wqu5qnnl5rev32w0jjyzmwbu9nfj68rxmzk2w1a16bvanqutoh.png)

3. Interpret the Output:

- If the ports are in use, you will see an output like this:

![](https://uploads.developerhub.io/prod/k8zL/egbvkqtrkgsmv7to72kc7d9jgsd500qj7legj1h60vstytdmvcohzxlz5ypyklmy.png)

- The last column (47752) is the Process ID (PID) of the application using the ports.

4. To identify the application using the PID, run:

![](https://uploads.developerhub.io/prod/k8zL/vb773wrc9vv76ns2zan97tni4k8fhvwktjudbof08370sjtuc1dmfpi6j2djmqpj.png)

Example Output:

![](https://uploads.developerhub.io/prod/k8zL/r99674vhe5pxbod2k24s9xgtcphlf28erxpl46w4yhd4quei3c4qunh9moj9wm0j.png)

This confirms that httpd.exe is using port 80 and 443.

---

## **Linux**

### **Checking Port 80 and 443 Using Netstat**

#### Steps:

1. Open a Terminal.
2. Run the following command:

![](https://uploads.developerhub.io/prod/k8zL/y1v93rurv1opjzg7hk3iotvwc3j4lg0q40r8nq93qavta2zf52f0kcepbsrdi3qz.png)

3. Interpret the Output:

- If ports 80 and 443 are in use, you will see an output like this:

![](https://uploads.developerhub.io/prod/k8zL/8pvvbm6dhnfg7xmnt7zk0cnpl5pjg7eq2j3lu2pjc7xfa3of0yq2nrwdcr1d40ms.png)

** Netstat Command Options Explained: **

- `-t` **→** Show TCP connections
- `-u` **→** Show UDP connections
- `-l` **→** Show Listening ports
- `-p` **→** Show the process name
- `-n` **→** Show numeric addresses instead of resolving hostnames

---

## **Conclusion**

- If ports 80 and 443 are available, you can proceed with the MDSS installation.
- If ports 80 and 443 are in use, you need to stop or reconfigure the conflicting application before installing MDSS.
- Use the provided commands on Windows and Linux to check and troubleshoot port usage effectively.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
