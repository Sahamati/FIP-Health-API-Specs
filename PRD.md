# FIP Health API V1.0.0

## Introduction
FIUs want to access SAANS Data during their user journeys. This allows them to reduce the number of new consent requests raised and better navigate users to different modes of the journeys, ensuring that the overall data flow success percentage is improved.

## Target Users
- FIUs
- AA Client apps
- FIP Health monitoring systems
- Real-time alert systems - both central and FIP specific

## Design
The solution requires a system that can identify FIUs that have subscribed to the service. These FIUs will expose a URL or an internal database that receives data from the API on a 3-hour frequency. This data will have the performance of the last 3 hours.

This API must have the following items:
- A database/registry in which the following information is stored:
  - User ID
  - User Type
  - User Callback URL
  - User Token
  - Frequency (increments of 30 mins)
- A mechanism to authenticate connections with the FIUs
- A mechanism to push the response body onto the callback URL provided by the FIU.
- A retry mechanism in case the push fails.
- A mechanism to track successes and failures and logs.

## API Broad Specs
API Specs: [View Specs](https://github.com/Sahamati/FIP-Health-API-Specs/blob/main/Push%20API%20Specifications.json)

Sample JSON: [View Sample](https://github.com/Sahamati/FIP-Health-API-Specs/blob/main/Sample%20response.json)

SLAs: [View SLAs](https://docs.google.com/spreadsheets/d/1T4qzwGPfqCxM-910HTZDkkikEezxUrU1/edit?usp=sharing&ouid=102688648237312172000&rtpof=true&sd=true)

## How it impacts the customer journey
- Ramesh is a customer applying for a loan with Navi(FIU). Navi has received data from the push API in their systems. Ramesh selects his banks(FIPs) as SBI and Axis. Navi calls the data stored in their system from the health API to check the status of the FIPs. Their internal API queries the data from the Health API and returns the healths of SBI and Axis bank. Finding that the health of Axis bank is poor in data flow, Ramesh is recommended sharing his SBI bank statements through AA and Axis Bank statement through pdf upload.
- Ramesh is also using the Fold Money(FIU) Application for tracking his investments.Fold money has received the data from the health API and Using the health API data, Fold money checks the health of SBI and Axis Bank. Fold money realizes that the discovery and linking health of SBI is currently bad hence Fold prompts Ramesh to check if his accounts are already linked with the AA(preferred by Fold or any AA that Fold is integrated with). Upon receiving a No, Fold currently only raises a consent request for Axis. Fold also periodically checks the health of SBI and once the health is improved, it also raises a request for SBI. Upon receiving a Yes, Fold processes the consent for both FIPs knowing that discovery and linking performance is not relevant for Ramesh.

## User Scenarios
- Navi(FIU) wants to use the health API as an input while designing their customer journeys.
- TSPs want to use the Health API to track how each FIP is performing in discovery and linking aspects. They may also want to resell the API to their FIU customers as a value-added service.
- SBI FIP wants to use the API to create a real-time health monitoring and alerts system for their FIP and design an in-house alert system that can help them cater to their individual designed needs.

## SRS
- API Type: PUSH API
- Architecture: [View Architecture](https://drive.google.com/file/d/1Yw0Ha3Jri0Bq6XH_MrIJtTm3sfE6atAD/view?usp=sharing)
- Registry: New realm on Keycloak
- 2 callback URLs - UAT and Production
- New Azure Function that runs on a time trigger (Infra)
- Blob Storage-1
- Azure Queue trigger
- Azure function that runs on Queue trigger

## Discussion
- Source is AAs, if AAs want to offer a more real-time service, AAs should be able to provide.
- TSPs can offer this as a premium real-time service.
- Funds to be pooled into a common fund, revenue sharing to AAs, Sahamati, and a dedicated portion to SAANS development fund.
