# Order Notification & IoT Automation

This project provides a Node.js-based service for processing orders and sending notifications based on order value.

## Features
- Processes orders and verifies required parameters (`order` and `manager`).
- Sends an email notification for high-value orders using SendGrid.
- Provides an email sending functionality using SendGrid API.
- Logs order processing and email notification details to the console.
- Provides a cURL command for invoking the service via OpenWhisk.
- Supports IBM Watson IoT Platform for event-based automation.

## Installation
1. Clone this repository:
   ```sh
   git clone <REPO_URL>
   ```
2. Navigate to the project directory:
   ```sh
   cd <PROJECT_FOLDER>
   ```
3. Install dependencies:
   ```sh
   npm install
   ```

## Usage
Call the `main` function with parameters:
```javascript
const params = { from: "FROM_EMAIL", to: "TO_EMAIL", subject: "Test Subject", content: "Email content here" };
main(params)
  .then(response => console.log(response))
  .catch(error => console.error(error));
```

## Environment Variables
Replace `<SENDGRID_API_KEY>`, `<FROM_EMAIL>`, and `<TO_EMAIL>` in the code with actual values.

## OpenWhisk Integration
Export required environment variables and invoke the service using cURL:
```sh
export TYPE='Content-Type: application/json'
export AUTH='Authorization: Basic '`bx wsk property get --auth | awk '{printf("%s", $3)}' | base64 `
export NAMESPACE=<OW_NAMESPACE>
export API_ENDPOINT=<API_ENDPOINT>
curl -k -s -X POST -d '{"from": "FROM_EMAIL_ID", "to": "TO_EMAIL_ID","subject":"OpenWhisk Alert","content":"Hello from Serverless"}' -H "$TYPE" -H "$AUTH" https://$API_ENDPOINT/api/v1/namespaces/$NAMESPACE/actions/sendMail?blocking=true
```

## IBM Watson IoT Platform Integration
### Button to Bulb Communication
1. The button sends an event to Watson IoT Platform.
2. The subscribed application processes the event and triggers an action.
3. The action sends a command to turn the bulb on/off.

## Dependencies
- Node.js
- SendGrid API
- OpenWhisk CLI
- UUID package (v3.0.1)
- IBM Watson IoT Platform
- Paho MQTT Library
- GrovePi Sensor Library

## Package.json Configuration
Below is the package.json configuration for the project:
```json
{
  "name": "sendgrid",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {
    "sendgrid": "file:",
    "uuid": "3.0.1"
  },
  "author": "",
  "license": "ISC"
}
```

## License
This project is licensed under the MIT License.
