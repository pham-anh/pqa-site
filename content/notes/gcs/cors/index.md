---
title: Enable CORS on Cloud Storage
menu:
  notes:
    name: Enable CORS on Cloud Storage
    identifier: notes-gcs-cors
    parent: notes-gcs
    weight: 401
---
{{< note title="Enable CORS on Cloud Storage">}}

# Enable CORS on Cloud Storage

The architecture

![](./attachments/Enable%20CORS%20on%20Cloud%20Storage.png)

Make a bucket public

```bash
gsutil -m acl set -R -a public-read gs://<bucket name>
```

Node.js code to get a file via HTTP

```javascript
http.get('https://storage.googleapis.com/<bucket name>/<path to file name>').then(function(response){
  data = response.data
})...
```

Enable CORS for a Cloud Storage bucket

```json
// sample json config file 1
[
  {
    "origin": ["*"],
    "responseHeader": ["*"],
    "method": ["*"],
    "maxAgeSeconds": 3600
  }
]

// sample json config file 2
[
  {
    "origin": ["http://35.202.103.76"],
    "responseHeader": ["*"],
    "method": ["*"],
    "maxAgeSeconds": 1
  }
]
```

Use gsutil to set CORS configuration

```bash
gsutil cors set <json config file> gs://<bucket name>
```

{{< /note >}}