# Losant Javascript REST API Client

[![Build Status](https://travis-ci.org/Losant/losant-rest-js.svg?branch=master)](https://travis-ci.org/Losant/losant-rest-js)

The [Losant](https://www.losant.com) REST API client provides a simple way to
use the comprehensive Losant API.  You can authenticate either as a Losant
device or with your user account, and have access to all the functionality
of the Losant platform.

This client works both in browsers and node.js (v0.12 and newer), and supports
both callbacks and promises. It uses [Axios](https://github.com/mzabriskie/axios)
under the covers for the actual HTTP communication.

<br/>

## Installation

The latest stable version is available in NPM and can be installed using

```bash
npm install --save losant-api-js
```

<br/>

## Example

Below is a high-level example of using the Losant Ruby REST API client to
authenticate against the Losant Platform and report state for a device.

```javascript
var api = require('losant-api-js');
var mySensor = require('./my-analog-sensor');

var client = api.createClient();

client.auth.authenticateDevice({ credentials: {
  deviceId: 'my-device-id',
  key: 'my-app-access-key',
  secret: 'my-app-access-secret'
}}).then(function (response) {
  client.setOption('accessToken', response.token);
  var appId = response.applicationId;

  var state = { data: { temperature: mySensor.read() } };
  return client.device.sendState({
    deviceId: 'my-device-id',
    applicationId: appId,
    deviceState: state
  });
})
.then(function (response) {
  console.log(response); // { success: true }
})
.catch(function (error) {
  console.error(error);
});
```

<br/>

## API Documentation

```javascript
var client = api.createClient({ accessToken: undefined, url: 'https://api.losant.com' })
```

The losant-api-js module exposes a single function named createClient which
returns a client instance.  Ite takes the following options:

*   accessToken  
The access token to be used for authentication - by default there is no
access token.  An access token can be acquired through either of the
[Auth](docs/auth.md) methods.

*   url  
The url of the Losant API - by default <https://api.losant.com>.

### Client

A client is a single api instance.  By default, it is unauthenticated, but can
be given an access token to perform authenticated requests.

#### Functions

*   setOption(name, value)  
The setOption function can be used to change any of the options currently
set on the client, such as the access token.

*   getOption(name)
The getOption function can be used to retrieve the current value of any of the
options set on the client instance.

#### Resources

Each of the following is a property on the client instance, and wraps the
actions for that particular resource.  See each resource documentation file
for more information.

*   [applicationKey](docs/applicationKey.md)  
Contains all the actions that can be performed against a single
[Application Key](https://docs.losant.com/applications/access-keys/) -
for instance, getting info on a single key or revoking a key.

*   [applicationKeys](docs/applicationKeys.md)  
Contains all of the actions that can be performed against the collection of
[Application Keys](https://docs.losant.com/applications/access-keys/) belonging
to an Application - such as listing all keys or creating a new key.

*   [application](docs/application.md)  
Contains all of the actions that can be performed against a single
[Application](https://docs.losant.com/applications/overview/),
which include things like getting info on an application or
modifying an application.

*   [applications](docs/applications.md)  
Contains all of the actions that can be performed against the set of
[Applications](https://docs.losant.com/applications/overview/) that the
currently authenticated user has access to - such as
listing the applications or creating a new application.

*   [auth](docs/auth.md)  
Contains the actions used for authenticating against the api, either as a
user or as a device.  The result of authentication calls contain the auth_token
needed for authenticated calls - see the examples for more details.

*   [dashboard](docs/dashboard.md)  
Contains all of the actions that can be performed against a single
[Dashboard](https://docs.losant.com/dashboards/overview/),
which include things like getting info on a dashboard or
modifying a dashboard.

*   [dashboards](docs/dashboards.md)  
Contains all of the actions that can be performed against the set of
[Dashboards](https://docs.losant.com/dashboards/overview/) that the
currently authenticated user has access to - such as
listing the dashboards or creating a new dashboard.

*   [data](docs/data.md)  
Contains the actions for querying against historical Device
data across an Application.

*   [device](docs/device.md)  
Contains all the actions that can be performed against a single
[Device](https://docs.losant.com/devices/overview/) -
for instance, getting info on a single device or reporting the current
state of a device.

*   [devices](docs/devices.md)  
Contains all of the actions that can be performed against the collection of
[Devices](https://docs.losant.com/devices/overview/) belonging
to an Application - such as listing all devices or sending a command to a set
of devices.

*   [deviceRecipe](docs/deviceRecipe.md)  
Contains all the actions that can be performed against a single
[Device Recipe](https://docs.losant.com/devices/device-recipes/), which
include things like removing a device recipe or creating a device
from a device recipe.

*   [deviceRecipes](docs/deviceRecipes.md)  
Contains all the actions that can be performed against the collection of
[Device Recipes](https://docs.losant.com/devices/device-recipes/) belonging
to an Application - such as listing recipes or creating a new recipe.

*   [event](docs/event.md)  
Contains all the actions that can be performed against a single
[Event](https://docs.losant.com/events/overview/), such as commenting on
or changing the state of an event.

*   [events](docs/events.md)  
Contains all the actions that can be performed against the collection of
[Events](https://docs.losant.com/events/overview/) belonging
to an Application - such as listing open events or creating a new event.

*   [flow](docs/flow.md)  
Contains all the actions that can be performed against a single
[Workflow](https://docs.losant.com/workflows/overview/), such as enabling or
disabling a workflow, or triggering a virtual button in the workflow.

*   [flows](docs/flows.md)  
Contains all the actions that can be performed against the collection of
[Workflows](https://docs.losant.com/workflows/overview/) belonging
to an Application - such as listing the workflows or creating a new workflow.

*   [me](docs/me.md)  
Contains the actions for operating against the currently authenticated
[User](https://docs.losant.com/user-accounts/overview/) such as changing
the password or linking against external services.

*   [org](docs/org.md)  
Contains all the actions that can be performed against a single
[Organization](https://docs.losant.com/organizations/overview/), things like
inviting a user to the organization, or modifying the organization.

*   [orgs](docs/orgs.md)  
Contains all of the actions that can be performed against the set of
[Organizations](https://docs.losant.com/organizations/overview/) that the
currently authenticated user has access to - such as
listing the organizations or creating a new organization.

*   [webhook](docs/webhook.md)  
Contains all the actions that can be performed against a single
[Webhook](https://docs.losant.com/applications/webhooks/), for instance
modifying the verification settings or removing the webhook.

*   [webhooks](docs/webhooks.md)  
Contains all the actions that can be performed against the collection of
[Webhooks](https://docs.losant.com/applications/webhooks/) belonging
to an Application - such as listing the webhooks or creating a new webhook.

<br/>

*****

Copyright (c) 2016 Losant IoT, Inc

<https://www.losant.com>
