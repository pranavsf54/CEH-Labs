# Lab 8: Perform Footprinting using Various Footprinting Tools

## Lab Scenario

The information gathered in the previous steps may not be sufficient to reveal the potential vulnerabilities of the target. There could be more information available that could help in finding loopholes in the target. As an ethical hacker, you should look for as much information as possible about the target using various tools. This lab activity will demonstrate what other information you can extract from the target using various footprinting tools.

## Lab Objectives

- Footprinting a target using Recon-ng

## Overview of Footprinting Tools

Footprinting tools are used to collect basic information about the target systems in order to exploit them. Information collected by the footprinting tools contains:

- Target's IP location information
- Routing information
- Business information
- Address, phone number and social security number
- Details about the source of an email and a file
- DNS information
- Domain information

## Task 1: Footprinting a Target using Recon-ng

Recon-ng is a web reconnaissance framework with independent modules and database interaction that provides an environment in which open-source web-based reconnaissance can be conducted. In this task, we will use Recon-ng to:

- Perform network reconnaissance
- Gather personnel information
- Gather target information from social networking sites

### Part 1: Initial Setup

1. In the Parrot Security machine, open a Terminal and run as root:

   ```
   sudo su
   ```

   Enter password: `toor`

2. Navigate to root directory and launch Recon-ng:

   ```
   cd
   recon-ng
   ```

   ![Recon-ng Launch](./screenshots/recon-ng-launch.png)

3. View available commands:

   ```
   help
   ```

   ![Help Command](./screenshots/help-command.png)

4. Install all available modules:

   ```
   marketplace install all
   ```

   Note: Ignore any errors during installation

   ![Module Installation](./screenshots/module-install.png)

5. View all available modules:

   ```
   modules search
   ```

   ![Available Modules](./screenshots/modules-list.png)

### Part 2: Workspace Setup

1. View workspace commands:

   ```
   workspaces
   ```

   ![Workspace Commands](./screenshots/workspace-commands.png)

2. Create new workspace:

   ```
   workspaces create CEH
   ```

   ![Create Workspace](./screenshots/create-workspace.png)

3. List workspaces:

   ```
   workspaces list
   ```

   ![List Workspaces](./screenshots/list-workspaces.png)

### Part 3: Domain Reconnaissance

1. Add target domain:

   ```
   db insert domains
   ```

   Enter domain: `certifiedhacker.com`
   Press Enter for notes

   Verify with:

   ```
   show domains
   ```

   ![Add Domain](./screenshots/add-domain.png)

2. Harvest hosts using brute_hosts module:

   ```
   modules load recon/domains-hosts/brute_hosts
   run
   ```

   ![Brute Hosts](./screenshots/brute-hosts.png)
   ![Brute Results](./screenshots/brute-results.png)

3. Use Bing module for additional host discovery:

   ```
   back
   modules load recon/domains-hosts/bing_domain_web
   run
   ```

4. Perform reverse lookup:

   ```
   modules load recon/hosts-hosts/reverse_resolve
   run
   ```

   ![Reverse Lookup](./screenshots/reverse-lookup.png)

5. View all harvested hosts:

   ```
   show hosts
   ```

   ![Show Hosts](./screenshots/show-hosts.png)

### Part 4: Generating Reports

1. Load HTML reporting module:

   ```
   modules load reporting/html
   ```

2. Configure report options:

   ```
   options set FILENAME /home/attacker/Desktop/results.html
   options set CREATOR [Your Name]
   options set CUSTOMER Certifiedhacker Networks
   run
   ```

   ![Report Generation](./screenshots/report-generation.png)

3. View generated report:
   Navigate to Desktop > results.html > Open with Firefox ESR

   ![Report Preview](./screenshots/report-preview.png)
   ![Hosts List](./screenshots/hosts-list.png)

### Part 5: Gathering Personnel Information

1. Create new workspace:

   ```
   workspaces create reconnaissance
   ```

   ![Reconnaissance Workspace](./screenshots/recon-workspace.png)

2. Load WHOIS module and gather contacts:

   ```
   modules load recon/domains-contacts/whois_pocs
   info
   options set SOURCE facebook.com
   run
   ```

   ![WHOIS Module](./screenshots/whois-module.png)
   ![Contact Results](./screenshots/contact-results.png)

### Part 6: Subdomain Enumeration

1. Use HackerTarget module:

   ```
   modules load recon/domains-hosts/hackertarget
   options set SOURCE certifiedhacker.com
   run
   ```

   ![Subdomain Enumeration](./screenshots/subdomain-enum.png)

## Lab Questions

### Question 2.8.1.1

Q: Use the Recon-ng tool to gather personnel information. Enter the Recon-ng module name that extracts the contacts associated with the domain and displays them.

A: `recon/domains-contacts/whois_pocs`
