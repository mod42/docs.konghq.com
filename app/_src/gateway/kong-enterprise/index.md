---
title: Overview
badge: enterprise
content_type: explanation
---

Kong Enterprise is the scalable, secure, and flexible API management solution that extends {{site.base_gateway}}, the fastest, most adopted API gateway. 
It adds enterprise plugins, a developer portal, analytics, advanced security features, GUI's, and 24/7 support. 
It is the only solution that helps you accelerate your cloud journey by managing, securing, and monitoring connections between applications across hybrid and multi-cloud architectures, to help you scale faster and boost developer productivity.

## Enterprise Plugins

Kong Enterprise offers access to 400+ out-of-box enterprise and community plugins. 
It offers exclusive versions of OSS plugins like the [Rate Limiting Advanced plugin](/hub/kong-inc/rate-limiting-advanced/) with added functionality such as the use of consumer groups, and database specific strategy. It also provides Enterprise-exclusive functionality, such as authentication with 
[OpenID Connect](/hub/kong-inc/openid-connect/), which lets you standardize identity provider (IdP) integrations.

Kong Enterprise also natively supports gRPC and REST, WebSockets, and integrates with Apollo GraphQL server and Apache Kafka services. These plugins can be leveraged to provide advanced connectivity features and solutions to {{site.base_gateway}} such as:

* [OpenID Connect (OIDC)](/hub/kong-inc/openid-connect/)
* [Event gateways with Kafka](/hub/kong-inc/kafka-upstream/)
* [GraphQL](/hub/kong-inc/graphql-proxy-cache-advanced/)
* [Mocking](/hub/kong-inc/mocking/)
* [Advanced data transformation](/hub/kong-inc/jq/)
* [OPA Policy driven traffic management](/hub/kong-inc/opa/)
{% if_version lte:3.3.x %}
* [API product tiers](/gateway/{{page.kong_version}}/admin-api/consumer-groups/reference/)
{% endif_version %}
{% if_version gte:3.4.x %}
* [API product tiers](https://developer.konghq.com/spec/937dcdd7-4485-47dc-af5f-b805d562552f/be79b812-46d5-4cc1-b757-b5270bf4fa60#/consumer_groups/get-consumer_groups)
{% endif_version %}
[Get started with plugins &rarr;](/hub/)

## Dev Portal

The Dev Portal provides a single source of truth for all developers to locate, access and consume APIs, similar to a traditional API catalog. 
Dev Portal streamlines developer onboarding by offering a self-service developer experience to discover, register, and consume published services from {{site.base_gateway}}.
This customizable experience can be used to match your own unique branding and highlights the documentation and interactive API specifications of your services.
In addition, you can secure your APIs with a variety of authorization providers by enabling application registration.

[Learn more about Dev Portal &rarr;](/gateway/{{page.kong_version}}/kong-enterprise/dev-portal/)

## Monitoring and analytics

The Vitals platform provides deep insights into services, routes, and application usage data. You can view the health of your API products with custom reports and contextual dashboards, and you can enhance the native monitoring and analytics capabilities with {{site.base_gateway}} plugins that enable streaming monitoring metrics to third-party analytics providers, such as [Datadog](/hub/kong-inc/datadog/) and [Prometheus](/hub/kong-inc/prometheus/).

[Start monitoring with Vitals &rarr;](/gateway/{{page.kong_version}}/kong-enterprise/analytics/)

## Role-based access control (RBAC)

Kong Enterprise lets you configure users, roles, and permissions with built-in role-based access control (RBAC). With RBAC, you can streamline developer onboarding, and create apply fine-grained security and traffic policies using the [Admin API](/gateway/{{page.kong_version}}/admin-api/rbac/reference/), or [Kong Manager](/gateway/{{page.kong_version}}/kong-manager/auth/rbac/).

[Manage teams with RBAC &rarr;](/gateway/{{page.kong_version}}/kong-manager/auth/rbac)

## Secrets management
Kong Enterprise offers out of the box secrets management with the following backends: 

* [Amazon Web Services](/gateway/{{page.kong_version}}/kong-enterprise/secrets-management/backends/aws-sm/)
* [Google Cloud Platform](/gateway/{{page.kong_version}}/kong-enterprise/secrets-management/backends/gcp-sm/)
* [Hashicorp Vault](/gateway/{{page.kong_version}}/kong-enterprise/secrets-management/backends/hashicorp-vault/)

To configure secrets management, {{site.base_gateway}} consumes your key for the backend provider, authenticates with the backend provider, and uses the backend to centrally manage and store application secrets, sensitive data, passwords, keys, certifications, tokens, and other items.

[Secure your application secrets &rarr;](/gateway/{{page.kong_version}}/kong-enterprise/secrets-management/)


## Keyring and data encryption

Keyring and data encryption functionality provides transparent, symmetric encryption of sensitive data fields at rest. When enabled, {{site.base_gateway}} encrypts and decrypts data immediately before writing, or immediately after reading, from the database. Responses generated by the Admin API that contain sensitive fields continue to show data as plaintext, and {{site.base_gateway}} runtime elements (such as plugins) that require access to sensitive fields do so transparently, without requiring additional configuration.

{{site.base_gateway}} allows you to store sensitive data fields, such as consumer secrets, in an encrypted format within the database.
This provides encryption-at-rest security controls in a {{site.base_gateway}} cluster.

[Set up keyring and data encryption &rarr;](/gateway/{{page.kong_version}}/kong-enterprise/db-encryption/)

## Audit logging

{{site.base_gateway}} provides granular logging of the Admin API. You can keep detailed track of changes made to the
cluster configuration throughout its lifetime, for compliance efforts and for
providing valuable data points during forensic investigations. Generated audit
log trails are [workspace](/gateway/{{page.kong_version}}/admin-api/workspaces/reference/) and [RBAC](/gateway/{{page.kong_version}}/admin-api/rbac/reference/)-aware,
providing {{site.base_gateway}} operators a deep and wide look into changes happening within
the cluster.

[Get started with audit logging &rarr;](/gateway/{{page.kong_version}}/kong-enterprise/audit-log/)

## FIPS support

Kong Enterprise features a self-managed FIPS 140-2 gateway package, making it ideal for highly regulated industries with strict compliance and security considerations. 
Compliance with this standard is typically required for working with U.S. federal government agencies and their contractors.

[Learn more about FIPS support &rarr;](/gateway/{{page.kong_version}}/kong-enterprise/fips-support/)

## Workspaces

Workspaces provide a way to segment or group {{site.base_gateway}} entities. Entities in a workspace are isolated from those in other workspaces.
{{site.ce_product_name}} is limited to one workspace. With Kong Enterprise, you can leverage multiple workspaces to allow developers to easily transition between projects, and to separate services and routes belonging to different upstreams. 

[Learn more about workspaces &rarr;](/gateway/{{page.kong_version}}/kong-manager/workspaces/)

## Dynamic plugin ordering

Dynamic plugin ordering allows you to override the priority for any {{site.base_gateway}} plugin using each plugin's `ordering` field. 
This determines plugin ordering during the `access` phase
and lets you create _dynamic_ dependencies between plugins.

[Get started with dynamic plugin ordering &rarr;](/gateway/{{page.kong_version}}/kong-enterprise/plugin-ordering/)
## Event hooks

Event hooks are outbound calls from {{site.base_gateway}}. With event hooks, the {{site.base_gateway}} can communicate with target services or resources, letting the target know that an event was triggered. When an event is triggered in the {{site.base_gateway}}, it calls a URL with information about that event. Event hooks add a layer of configuration for subscribing to worker events using the admin interface. 

In {{site.base_gateway}}, these callbacks can be defined using one of the following handlers:

* webhook
* webhook-custom
* log
* lambda

You can configure event hooks through the Admin API.

[Learn more about event hooks &rarr;](/gateway/{{page.kong_version}}/admin-api/event-hooks/reference/)

## Consumer groups

You can use consumer groups to manage custom rate limiting configuration for subsets of consumers. With consumer groups, you can define any number of rate limiting tiers and
apply them to subsets of consumers, instead of managing each consumer
individually.

For example, you could define three consumer groups:
* A "gold tier" with 1000 requests per minute
* A "silver tier" with 10 requests per second
* A "bronze tier" with 6 requests per second

{% if_version lte:3.3.x %}
[Set up consumer groups &rarr;](/hub/kong-inc/rate-limiting-advanced/how-to/)
[Consumer groups API reference](/gateway/{{page.kong_version}}/admin-api/consumer-groups/reference/)
{% endif_version %}
{% if_version gte:3.4.x %}
[Set up consumer groups &rarr;](/hub/kong-inc/rate-limiting-advanced/how-to/)
[Consumer groups API documentation](https://developer.konghq.com/spec/937dcdd7-4485-47dc-af5f-b805d562552f/be79b812-46d5-4cc1-b757-b5270bf4fa60#/consumer_groups/get-consumer_groups)
{% endif_version %}

{% if_version gte:3.2.x %}
## Provisioning new data planes in the event of a control plane outage

Starting in version 3.2, {{site.base_gateway}} can be configured to support configuring new data planes in the event of a control plane outage. For more information, read the [How to Manage New Data Planes during Control Plane Outages](/gateway/latest/kong-enterprise/cp-outage-handling/) documentation, or the [Control Plane Outage Management FAQ](/gateway/latest/kong-enterprise/cp-outage-handling-faq/).

{% endif_version %}
## More information

See [Plugin Compatibility](/hub/plugins/compatibility/) for more information about Enterprise-only plugins.
