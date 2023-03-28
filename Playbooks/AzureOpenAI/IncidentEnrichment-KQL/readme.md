# Azure OpenAI Sentinel Use Cases - Incident Enrichment with AI-generated KQL queries

<b>Enrich the incident with an AI generated KQL queries <br></b>
This Playbook summits incident details (Title, Description,Entities, ATT&CK details, Sentinel Availabe tables to the Azure OpenAI ChatGPT API. It writes the generated KQL queries as Incident Tasks and the results of the queries as a comment.

An Azure OpenAI Endpoint and API key are required in order to work. You can get them from Azure Cognitive services. 

You also need to assign Sentinel Responder role to the Logic App managed identity in order to add comments to the incident. 

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjguimera%2FMicrosoft-Sentinel%2Fmain%2FPlaybooks%2FAzureOpenAI%2FIncidentEnrichment-KQL%2Fdeployazure.json)