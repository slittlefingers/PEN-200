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


