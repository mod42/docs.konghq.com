---
nav_title: Overview
---

The jq plugin enables arbitrary jq transformations on JSON objects included in API requests or responses.

The configuration accepts two sets of options: one for the request and another for the response.
For both the request and response, a jq program string can be included, along with some jq option flags
and a list of media types.

One of the configured media types must be included in the `Content-Type` header of
the request or response for the jq program to run. The default media type in the `Content-Type`
header is `application/json`.

In the response context, you can also specify a list of status
codes, one of which must match the response status code.
The default response status code is `200`.

{:.note}
> **Notes:**
> * In the response context the entire body must be buffered to be processed. This requirement also
implies that the `Content-Length` header will be dropped if present, and the body transferred with chunked encoding.
> * To use this plugin in Konnect,
[upgrade your runtimes](/konnect/runtime-manager/upgrade/) to at least
v2.6.0.0.

See jq's documentation on [Basic filters](https://stedolan.github.io/jq/manual/#Basicfilters) for more information on writing programs with jq.
