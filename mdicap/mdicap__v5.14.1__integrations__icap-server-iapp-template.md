<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template -->

# ICAP Server iApp template

## [iApps in a nutshell](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#iapps-in-a-nutshell)

iApps is a user-customizable framework for deploying applications that enables templatizing sets of functionality on an F5 gear. Automate the process of adding virtual servers or build a custom iApp to manage your iRules inventory. [[F5-1](https://devcentral.f5.com/iapps)]

Info

The iApps technology was released in F5’s v11.

For cases when iApps can not be used please see the generic integration guide: [F5 BIG IP LTM](/docs/mdicap/v5.14.1/integrations/f5-big-ip-ltm).

iApps are powerful tools. Used by roughly one third of all F5 customers, they perform input validation and apply complex business logic for configuring a wide variety of applications. They hide complexity, sometimes driving hundreds of configuration parameters with just a handful of input values. They also provide deployment guidance, reducing the need for documentation and training. It is helpful to understand the difference between an iApp and a wizard. A wizard is usually a script with a GUI. It is a tool that accepts a set of user inputs and performs a one-time procedure. When run twice, a wizard performs exactly the same steps during its second run as it did during its first. Although an iApp is also a script with a GUI, it behaves differently on re-entry. Unlike a wizard, an iApp maintains a relationship to the configuration that it generates. [[F5-2](https://devcentral.f5.com/articles/understanding-iapps-18224)]

**iApps have 5 critical properties**: [[F5-2](https://devcentral.f5.com/articles/understanding-iapps-18224)]

- iApps always act atomically. The result of deployment is always either the entire intended configuration or none at all.
- iApp-driven configuration objects are marked so the iApp can track them throughout its lifecycle. A visualization of these configuration objects is presented in the popular TMUI “Component View.”
- iApps protect the configuration from accidental changes. iApp-driven elements may not be changed via the UI or CLI except through the iApp.
- iApps support re-entry. Since the iApp framework tracks the configuration objects that it manages, it can be intelligent about which elements are touched during reconfiguration.
- iApps automatically perform cleanup on deletion. The housekeeping is automatic, and the iApp author does not need to (and is not allowed to) write any delete-time code.

There is an analogy between iApps and iRules that help understanding iApps better. F5 products support a scripting language based on TCL. This language allows an administrator to tell their BIG-IP to intercept, inspect, transform, direct and track inbound or outbound application traffic. An iRule is the bit of code that contains the set of instructions the system uses to process data flowing through it, either in the header or payload of a packet. This technology allows our customers to solve real-time application issues, security vulnerabilities, etc that are unique to their environment or are time sensitive. [[F5-3](https://devcentral.f5.com/articles/iapp-ndash-what-is-it)]

[[F5-3](https://devcentral.f5.com/articles/iapp-ndash-what-is-it)]

An iApp is like iRules, but for the management plane. Again, there is a scripting language that administrators can build instructions the system will use. But instead of describing how to process traffic, in the case of iApp, it is used to describe the user interface and how the system will act on information gathered from the user. The bit of code that contains these instructions is referred to as an iApp or iApp template. A system administrator can use F5-provided iApp templates installed on their BIG-IP to configure a service for a new application. They will be presented with the text and input fields defined by the iApp author. Once complete, their answers are submitted, and the template implements the configuration. First an application service object (ASO) is created that ties together all the configuration objects which are created, like virtual servers and profiles. Each object created by the iApp is then marked with the ASO to identify their membership in the application for future management and reporting. [[F5-3](https://devcentral.f5.com/articles/iapp-ndash-what-is-it)]

## [Benefits for ICAP Server](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#benefits-for-icap-server)

From MetaDefender ICAP Server's perspective iApps is an exceptionally powerful tool to perform integration to F5 BIG IP in a quick and easy way, with no deeper knowledge about both BIG IP and ICAP Server.

## [ICAP Server iApp template](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#icap-server-iapp-template)

### [Getting the template](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#getting-the-template)

The *opswat_metadefender_icap* iApp template can be downloaded from <https://github.com/OPSWAT/F5-iApp>.

## [Importing the template into F5 BIG IP](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#importing-the-template-into-f5-big-ip)

1. Login to F5 using an account with administrative privileges.

2. From the left side menu select *Main* > *iApps* > *Templates* and click the *Import...* button on the top of the *Template List*.

3. Click the Choose file button and select the file containing the MetaDefender ICAP Server iApp template.

4. Click the *Upload* button and wait for the file being uploaded.

5. Once the file gets uploaded the *opswat_metadefender_icap* template appears in the list (in a position defined by the current ordering of the list).

## [Creating an ICAP Server application service](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#creating-an-icap-server-application-service)

Once the *opswat_metadefender_icap* iApp template is imported, it can be used to create new *application services*.

1. From the left side menu select Main > iApps > Applicaton Services and click the Create... button (or click the icon next to Application Services).

2. From the *Template* list select *opswat_metadefender_icap.*

3. The fields of the *New Application Service...* window are populated according to the selected template.

### [Basic configuration](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#basic-configuration)

Note

In this section we will create a basic configuration, but may not be adequate in a specific production environment.

Warning

Do NOT select HTTP monitor for the ICAP pool

When selecting an HTTP monitor for the ICAP pool there will be a lot of "GET /" HTTP requests towards ICAP which will be displayed as a Bad Request in the ICAP hstory.

#### [ICAP On-Prem](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#icap-on-prem)

1.Provide the *Name* for this application service.

2.Choose the option for ICAP On-Prem deployment

3.Provide the IP address (and Port) of the MetaDefender ICAP Server. If an ICAP server node has previously been created, then it can also be selected here. If there are multiple ICAP servers, then any lot (at least one) can be added here.

4.Click the Finished button

5.The configuration is created and displayed in the next screen. Please note the *Metadefender_ICAP_Request* and *Metadefender_ICAP_Response* profiles created. These profiles are needed to be assigned to a virtual server (see in the next section) so that content adaptation can work.

#### [Metadefender ICAP Cloud](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#metadefender-icap-cloud)

Info

The ICAP Cloud is deployed at host **icap.metadefender.com** with port **11344**

1.Provide the *Name* for this application service

2.Choose the option for ICAP

3.Input the MDCloud APIKey

4.Create a new pool for the MD ICAP Server on Cloud

5.Click the *Finished* button

6.The configuration is created and displayed in the next screen. Please note the *Metadefender_ICAP_Request* and *Metadefender_ICAP_Response* profiles created. These profiles are needed to be assigned to a virtual server (see in the next section) so that content adaptation can work

## [Assigning request and response adapt profiles](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#assigning-request-and-response-adapt-profiles)

Note

As a final step the request and response adapt profiles –created in the previous section– are needed to be assigned to a virtual server so that content adaptation can work.

Creating virtual servers –besides creating ICAP virtual servers automatically by the ICAP Server iApp– is, however, not in the scope of this document.

1. From the left side menu select *Main* > *Local Traffic* > *Virtual Servers*. The list of virtual servers is displayed.

2. From the list select the virtual server to which content adaptation needs to be configured. The properties of the virtual server are displayed. Select *Advanced* for *Configuration*.

3. Scroll down and look for Request Adapt Profile and Response Adapt Profile. Select the Metadefender_ICAP_ Request and Metadefender_ICAP_Response profiles based on whether both requests and responses, only one, or none of them needs to be sent to the ICAP Server.

4. Scroll further down and click the *Update* button to commit the changes.

## [Testing the configuration](/docs/mdicap/v5.14.1/integrations/icap-server-iapp-template#testing-the-configuration)

To test the configuration point a browser to the IP or DNS address of the virtual server and observe how the traffic is handled by the ICAP Server.

1. Obtain the IP address of the virtual server from the configuration.

2. Point a browser to the web pages of the virtual server and generate traffic.

3. Observe the traffic in MetaDefender ICAP Server.
