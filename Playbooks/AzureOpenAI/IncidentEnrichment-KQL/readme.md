# Azure OpenAI Sentinel Use Cases - Incident Enrichment with AI-generated KQL queries

<b>Enrich the incident with an AI generated KQL queries <br></b>
This Playbook summits incident details (Title, Description,Entities, ATT&CK details, Sentinel Availabe tables to the Azure OpenAI ChatGPT API. It writes the generated KQL queries as Incident Tasks and the results of the queries as a comment.<br><br>
Generated KQL queries might contain Schema errors. These errors will prevent the query from being executed. However this failure won't stop the rest of the queries from being executed. 
### Requirements:
* An Azure OpenAI Endpoint and API key are required in order to work. You can get them from Azure Cognitive services. 
* Assign Sentinel Responder role to the Logic App managed identity in order to add comments to the incident. 
* Authorize Azure Monitor API Connection to retrieve data from Log Analytics. 
### Playbook steps:
* Retrieve Available Tables in Sentinel using a KQL query.
* Ask ChatGPT for three KQL queries to investigate this incident:
  * Inputs: Incident Details (Title,Description,Severity,Entities,MITRE ATT&CK) and Available Sentinel Tables. 
  * Model: gpt-35-turbo (version 0301), Temperature:0.7 , Top_p:0.95
  * Query Language: ChatML
  * Prompt: Return three tasks with KQL queries to triage this incident using the available Microsoft Sentinel tables. Make sure you only use correct column names for each table. Respond only with the list of KQL queries in JSON Format (without any other text) using the following schema and escaping double quotes:{....}
* Parse the three KQL queries in the response.
* For each KQL query:
   * Create an incident task with the query code
   * Run the query and add the results as an incident comment. If a query fails keep executing the rest. 

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjguimera%2FMicrosoft-Sentinel%2Fmain%2FPlaybooks%2FAzureOpenAI%2FIncidentEnrichment-KQL%2Fdeployazure.json)

Playbook Screenshot:<br>
![Alt text](https://github.com/jguimera/Microsoft-Sentinel/blob/main/Playbooks/AzureOpenAI/IncidentEnrichment-KQL/AzureOpenAI-IncidentEnrichment.png?raw=true "Playbook flow")
