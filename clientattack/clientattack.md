# Client side attack
## Target Reconnaissance
* Gather information
* leverge client fingerprints
  
### Information gathering
1. Goal of Passive Reconnaissance:
   * To enumerate a target's installed software without alerting their monitoring systems or leaving forensic evidence.
   * Suited for situations with no direct access to the target.
2. Methodology:
   * Metadata Analysis: Inspect the metadata tags of public documents from the target organization.
     * Metadata can include the software and version used to create the document, the author, creation date, operating system, etc.
     * Tags can be manually sanitized but often are not, providing potentially useful information.
3. Sources of Information:
    * Publicly available documents associated with the target can reveal software metadata.
4. Limitations:
   * Information may be outdated.
   * Variations in software use across different branches of the organization.
5. Techniques for Information Gathering:
   * Google Dorking: Use specific search queries such as site:example.com filetype:pdf to find PDFs on a target's website.
   * Directory Enumeration Tools: Tools like gobuster with -x parameter to find files with specific extensions. This method is more intrusive and can create noise in the target's logs.
  
6. Practical Example:

   * Scenario: You're gathering information about the Mountain Vegetables company.
   * Action: Use a browser to navigate to the   company's website (e.g., http://192.168.50.197) and search for documents to analyze.
   * Example Google Dork: To find PDF documents on the Mountain Vegetables website, you would use site:mountainvegetables.com filetype:pdf in a Google search.

**To display the metadata of any supported file,4 we can use exiftool.5**
> The reason use this tool.
>>1. more comprehensive metadata information (history, modification history, specific software version, operating system
>>2. Automation and efficiency
>>3. display hidden attributes and security
>>4. Comparibility and Standardization
```shell
cd Downloads
exiftool -a -u brochure.pdf
```
This generated a lot of output. For us, the most important information includes the **file creation date, last modified date, the author's name, the operating system, and the application used to create the file.**

The Create Date and Modify Date sections reveal the relative age of the document. Given that these dates are relatively recent (at the time of this writing) we have a high level of trust that this is a good source of metadata.(**meaning that the information or data is up-to-date which should be crucial for ensuring the accuracy and relevance of the information**)

The Author section reveals the name of an internal employee. **We could use our knowledge of this person to better establish a trust relationship by dropping their name casually into a targeted email or phone conversation**. This is especially helpful if the author maintains a relatively small public profile.

The output further reveals that the PDF was created with Microsoft PowerPoint for Microsoft 365. **This is crucial information for us to plan our client-side attack since we now know that the target uses Microsoft Office and since there is no mention of "macOS" or "for Mac" in any of the metadata tags**, it's very probable that Windows was used to create this document.

We can now leverage client-side attack vectors ranging from Windows system components to malicious Office documents.

## Labs1:
>Download old.pdf from the Mountain Vegetables website on VM #1 by clicking on the OLD button. Use exiftool to review the file's metadata. Enter the value of the Author tag.
* search for the pdf and download it
![This is for process](2024-01-26%2014_35_53-.png)

* use esiftool -a -u command to find the detailed information inside the document
![This is for process](2024-01-26%2014_30_16-.png)
![This is for process](2024-01-26%2014_30_28-clientattack.md%20-%20pen%20-%20Visual%20Studio%20Code.png)

## Labs2:
>Start VM #2 and use gobuster to bruteforce the contents of the web server. Specify "pdf" as the filetype and find a document other than old.pdf and brochure.pdf. After you identify the file, download it and extract the flag in the metadata.
* gobuster
   ```shell
   gobuster dir -u http://targetwebsite.com -w /usr/share/wordlists/dirb/common.txt
   ```
* **hint: we can use kali linux's wordlist(normaly it is inside of /usr/share/wordlist)**
   1. dirb: web hidden dir or file
   2. dirbuster: same but other
   3. nmap.lst: nmap weak password
   4. rockyou.txt: weak password
      ```shell 
      john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
      ```
      ```shell
      hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt```
* use gobuster to find pdf
   ![this is for process](2024-01-26%2018_43_36-.png)
* use firefow find the pdf and use exiftool to find the detailed information
   ![this is for process](2024-01-26%2018_43_54-.png)