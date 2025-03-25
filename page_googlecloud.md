---
layout: default
title: Google Cloud Platform
permalink: /GoogleCloud/
toc: True
---

# Google Cloud Platform

## Authentication

```
gcloud config set project PROJECT_ID
```

```bash
gcloud projecs list
```

```bash
gcloud auth login
```

```bash
gcloud auth list
```

```bash
gcloud auth application-default login [--impersonate-service-account=SERVICE_ACCOUNT]
```

```bash
gcloud auth application-default revoke
```

```bash
gcloud auth activate-service-account ACCOUNT --key-file=credentials.json
```

```bash
gcloud auth revoke --all
```

```bash
gcloud auth revoke ACCOUNT
```

```bash
export GOOGLE_APPLICATION_CREDENTIALS=/path/to/credentials.json
```

```bash
gcloud auth print-identity-token
```

```bash
gcloud auth print-access-token
```

```bash
SERVICE_ACCOUNT@PROJECT_ID.iam.gserviceaccount.com
```

## Default Credentials

```python
credentials, project_id = google.auth.default()
```

## Validate JWT python version

A partian content of a JWT:


```json
{
  "alg": "RS256",
  "kid": "abcdef",
  "typ": "JWT"
}

{
  "aud": "aaaa",
  "exp": 0000,
  "iat": 000,
  "iss": "example@abc.gserviceaccount.com"
}
```

```
pip install oauth2client
pip install google-auth
pip install google-api-python-client
```

```python
import oauth2client

issuer = 'example@abc.gserviceaccount.com'
cert = 'https://www.googleapis.com/service_accounts/v1/metadata/x509/'

try:
    res = oauth2client.client.verify_id_token(
        token, 
        project_number, 
        cert_uri=cert + issuer
    )
    return res['aud'] != issuer

except Exception as e:
    logging.exception("not a valid bearer token")
    return False
```

Audience and issues are not always needed

## Retrieve 

``` python
import oauth2client
import google.oauth2.id_token
import googleapiclient.discovery
from google.auth.transport.requests import AuthorizedSession, Request

def get_token_default() -> str:
    credentials, _ = google.auth.default()

    credentials.refresh(Request(AuthorizedSession(credentials)))
    if hasattr(credentials, "token"):
        return credentials.token

    credentials.refresh(Request())
    if hasattr(credentials, "token"):
        return credentials.token


def get_token_for(endpoint: str) -> str:
    url = urllib.parse.urlparse(endpoint)
    audience = f'{url.scheme}://{url.netloc}'
    try:
        return google.oauth2.id_token.fetch_id_token(Request(), audience)
    except:
        return get_token_default()
    
```

## Docker

```bash
gcloud auth configure-docker
```

```bash
gcloud auth configure-docker gcr.io
```

---

# Predefined Roles and Permissions

Often google refers to the role name instead of the actual role name needed
by gcloud or terraform-like frameworks, the following link provides the human 
readable role name, the actual role and the permissions predefined for 
that specific role, e.g.:

- BigQuery Admin > (roles/bigquery.admin) > bigquery.bireservations.*

Link: https://cloud.google.com/iam/docs/understanding-roles

---

# API Discovery

## Python

``` bash
pip install oauth2client
pip install google-auth
pip install google-api-python-client
```

Refer to https://developers.google.com/apis-explorer/ to get the list of supported
services.

For this example, refer to https://cloud.google.com/resource-manager/reference/rest/v1/projects/get

```python
import googleapiclient.discovery

discovery = googleapiclient.discovery.build('cloudresourcemanager', 'v1')
request = (
    discovery
        .projects()
        .get(projectId=project_id)
)
response = request.execute()
```

---

# Resources

- https://cloud.google.com/sdk/gcloud/reference/auth/activate-service-account
- https://cloud.google.com/sdk/gcloud/reference/auth/print-access-token
- https://cloud.google.com/sdk/gcloud/reference/auth/print-identity-token
- https://cloud.google.com/sdk/gcloud/reference/config/set
- https://cloud.google.com/sdk/gcloud/reference/auth/configure-docker
- https://developers.google.com/chat/api/guides/message-formats
- https://cloud.google.com/iam/docs/understanding-roles
- https://developers.google.com/discovery
- https://developers.google.com/apis-explorer/
- https://developers.google.com/api-client-library
