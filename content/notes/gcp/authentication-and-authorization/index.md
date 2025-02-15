---
title: Authentication and Authorization
menu:
  notes:
    name: Authentication and Authorization
    identifier: Authentication-and-Authorization
    parent: notes-gcp
    weight: 202
---

{{< note title="Authentication and Authorization" >}}

# Authentication and Authorization

{{< alert type="info" >}}
IAM, Identity Platform, Identity-Aware Proxy (IAP)<br>
Federated identity with Firebase SDK (Identity Platform similar?)
{{< /alert >}}
{{< /note >}}

{{< note title="Application Default Credential" >}}

ADC checks for credential in the following orders

1. GOOGLE\_APPLICATION\_CREDENTIALS environment variable
2. Default service account (Compute Engine, Google Kubernetes Engine, App Engine, Cloud Functions, Cloud Run)

{{< /note >}}

{{< note title="OAuth 2.0 (user consent screen)" >}}

https://support.google.com/cloud/answer/6158849?hl=en

{{< /note >}}

{{< note title="Identity-Aware Proxy (IAP)" >}}
IAP allows you to establish a central accessed by HTTPS

IAP lets you adopt an application-level access control model instead of relying on network-level firewalls

Work with Google Sign-in only

##### Some IAP usage model

- User → IAP → GAE
- User → Load Balancer → GKE / GCE

##### Follow the precautions when using IAP

- Configure your firewall and load balancer to protect against traffic that doesn’t come from the serving infrastructure
- Use signed headers or the App Engine standard environment Users API
{{< /note >}}

{{< note title="Identity Platform" >}}
(Authentication as a service, developers access via a set of SDKs)

Provide federate login that integrates with many common providers

- SAML, OpenID Connect, Google, Twitter, Facebook, Microsoft, LinkedIn
- Email and Password
- Phone

{{< /note >}}

{{< note title="Identity Platform vs Firebase Authentication" >}}
Common feature: Easily sign users into your apps
* Provide backend services, SDKs, UI libraries
* SDKs occasionally used Firebase branding and naming conventions for backward compatibility

**Identity Platform** only-features:
* Offers additional capabilities for enterprise customers: OpenID Connect, SAML authentication, multi-tenancy support, IAP integration, 99.95% uptime SLA.
    - **Daily:** 43s
    - **Weekly:** 5m 2.4s
    - **Monthly:** 21m 44s
    - **Quarterly:** 1h 5m 12s
    - **Yearly:** 4h 20m 49s
* Upgrading to Identity will continue to work with existing Firebase services
{{< /note >}}

{{< note title="Lab - Adding user authentication to your application" >}}
* Use Identity Platform
* Login with username and password
{{< /note >}}