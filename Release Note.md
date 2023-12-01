# FIP Health API V1.0.0

## Introduction
FIUs/TSPs want to access SAANS Data during their user journeys. This allows them to manage the user expectations and Lending FIUgate the user through the AA flow depending upon the health status of the APIs. This could lead to a higher success percentage by only raising a consent request when the likelihood of the success of the consent is much higher. 

## Target Users
- FIUs
- AA Client apps
- FIP Health monitoring systems
- TSPs
- Real-time alert systems - both central and FIP specific

## How the solution works
The solution requires a system that can identify FIUs that have subscribed to the service. These FIUs will expose a endpoints that receives data from the API on a 30 min frequency. This data will be calculated based on the performance of FIP over the last 3 hours. The data will be pushed to the exposed endpoint. 

## How to access the SAANS API
1. **Create a public endpoint:**
   Set up an endpoint to receive notifications from the SAANS Health API service as per the specs mentioned below. 

2. **Whitelist IPs on your Firewall:**
   Whitelist the following IP addresses on your Firewall:
   - "20.204.209.246"
   - "13.71.48.89"

3. **Authenticate the Request:**
   To further authenticate the request from the SAANS health API:
   - The API sends an `Authorization` header in the request with a bearer token.
   - Validate the token with the Sahamati token service’s public certificate. You can find the certificate [here](#link-to-certificate).
   - Refer to [this guide](#link-to-validation-guide) for instructions on validating JWT with a public key.

4. **Fill in the Form:**
   Complete the information in the following form: [Form Link](https://forms.gle/F3fhxHzQzeEZUKBx6)

5. **Deploy on your endpoint:**
   You will start receiving notifications on your configured endpoint on a T+1 basis. 

## API Broad Specs
API Specs: [View Specs](https://github.com/Sahamati/FIP-Health-API-Specs/blob/main/Health%20API%20Specs.json)

Sample JSON: [View Sample](https://github.com/Sahamati/FIP-Health-API-Specs/blob/main/Sample%20response.json)

SLAs: [View SLAs](https://docs.google.com/spreadsheets/d/1T4qzwGPfqCxM-910HTZDkkikEezxUrU1/edit?usp=sharing&ouid=102688648237312172000&rtpof=true&sd=true)


