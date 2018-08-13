# File Actions

Details on the various actions that can be performed on the
File resource, including the expected
parameters and the potential responses.

##### Contents

*   [Delete](#delete)
*   [Get](#get)
*   [Move](#move)
*   [Patch](#patch)

<br/>

## Delete

Deletes a file or directory, if directory all the contents that directory will also be removed.

```javascript
var params = {
  applicationId: myApplicationId,
  fileId: myFileId
};

// with callbacks
client.file.delete(params, function (err, result) {
  if (err) { return console.error(err); }
  console.log(result);
});

// with promises
client.file.delete(params)
  .then(console.log)
  .catch(console.error);
```

#### Authentication
The client must be configured with a valid api access token to call this
action. The token must include at least one of the following scopes:
all.Application, all.Organization, all.User, file.*, or file.delete.

#### Available Parameters

| Name | Type | Required | Description | Default | Example |
| ---- | ---- | -------- | ----------- | ------- | ------- |
| applicationId | string | Y | ID associated with the application |  | 575ec8687ae143cd83dc4a97 |
| fileId | string | Y | ID associated with the file |  | 575ec76c7ae143cd83dc4a96 |

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [Success](_schemas.md#success) | If file was successfully deleted |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](_schemas.md#error) | Error if malformed request |
| 404 | [Error](_schemas.md#error) | Error if event was not found |

<br/>

## Get

Retrieves information on a file

```javascript
var params = {
  applicationId: myApplicationId,
  fileId: myFileId
};

// with callbacks
client.file.get(params, function (err, result) {
  if (err) { return console.error(err); }
  console.log(result);
});

// with promises
client.file.get(params)
  .then(console.log)
  .catch(console.error);
```

#### Authentication
The client must be configured with a valid api access token to call this
action. The token must include at least one of the following scopes:
all.Application, all.Application.read, all.Organization, all.Organization.read, all.User, all.User.read, file.*, or file.get.

#### Available Parameters

| Name | Type | Required | Description | Default | Example |
| ---- | ---- | -------- | ----------- | ------- | ------- |
| applicationId | string | Y | ID associated with the application |  | 575ec8687ae143cd83dc4a97 |
| fileId | string | Y | ID associated with the file |  | 575ec76c7ae143cd83dc4a96 |

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [File Schema](_schemas.md#file-schema) | file information |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](_schemas.md#error) | Error if malformed request |
| 404 | [Error](_schemas.md#error) | Error if file was not found |

<br/>

## Move

Move a file or the entire contents of a directory

```javascript
var params = {
  applicationId: myApplicationId,
  fileId: myFileId
};

// with callbacks
client.file.move(params, function (err, result) {
  if (err) { return console.error(err); }
  console.log(result);
});

// with promises
client.file.move(params)
  .then(console.log)
  .catch(console.error);
```

#### Authentication
The client must be configured with a valid api access token to call this
action. The token must include at least one of the following scopes:
all.Application, all.Organization, all.User, file.*, or file.move.

#### Available Parameters

| Name | Type | Required | Description | Default | Example |
| ---- | ---- | -------- | ----------- | ------- | ------- |
| applicationId | string | Y | ID associated with the application |  | 575ec8687ae143cd83dc4a97 |
| fileId | string | Y | ID associated with the file |  | 575ec76c7ae143cd83dc4a96 |
| name | undefined | N | The new name of the file or directory |  | fileA |
| parentDirectory | undefined | N | The new parent directory for the file or directory to move into. |  | /new/location/here |

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 201 | [File Schema](_schemas.md#file-schema) | Returns a new file or directory that was created by the move, if a directory a job will kick off to move all the directories children. |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](_schemas.md#error) | Error if malformed request |
| 404 | [Error](_schemas.md#error) | Error if application was not found |

<br/>

## Patch

Reupload a file

```javascript
var params = {
  applicationId: myApplicationId,
  fileId: myFileId,
  updates: myUpdates
};

// with callbacks
client.file.patch(params, function (err, result) {
  if (err) { return console.error(err); }
  console.log(result);
});

// with promises
client.file.patch(params)
  .then(console.log)
  .catch(console.error);
```

#### Authentication
The client must be configured with a valid api access token to call this
action. The token must include at least one of the following scopes:
all.Application, all.Organization, all.User, file.*, or file.patch.

#### Available Parameters

| Name | Type | Required | Description | Default | Example |
| ---- | ---- | -------- | ----------- | ------- | ------- |
| applicationId | string | Y | ID associated with the application |  | 575ec8687ae143cd83dc4a97 |
| fileId | string | Y | ID associated with the file |  | 575ec76c7ae143cd83dc4a96 |
| updates | [File Patch](_schemas.md#file-patch) | Y | Reupload a file |  | [File Patch Example](_schemas.md#file-patch-example) |

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 201 | [File Post Response](_schemas.md#file-post-response) | Successfully updated file and returned a post url to respond with |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](_schemas.md#error) | Error if malformed request |
| 404 | [Error](_schemas.md#error) | Error if application was not found |