---
layout: default
title: Comments
parent: Search
nav_order: 2
---

# Get Comments

This API endpoint is designed to retrieve the comments associated with a specific entity.

**EndPoint:** https://intelligence.threatwinds.com/api/search/v1/comments/{id}

### Parameters
  
<dl>
  <dt><b>Autentication</b></dt>
  <dd>Authentication can be via Authorization header or Key-Pair. See the See <a href="../QUICKSTART#auth">Quick Start Auth</a> for a short explanation.<dl>
  <dt><b>Authorization</b> (<i>string</i>)</dt>
  <dd>The authorization header of the session if it is your authentication method.<br>
      <code>e.g.: Bearer fq6JoEFTsxiXAl1cVxPDnK4emIQCwaUBfq6JoEFTsxiXAl1cVxPDnK4emIQCwaUB</code></dd>
  <dt><b>api-key</b> (<i>string</i>)</dt>
  <dd>It needs to be combined with the api-secret. You can get it from the <a href="../auth/KeyPair">Key Pair Endpoints</a>.</dd>
  <dt><b>api-secret</b> (<i>string</i>)</dt>
  <dd>It needs to be combined with the api-key. You can get it from the <a href="../auth/KeyPair">Key Pair Endpoints</a>.</dd>
  </dl>
  </dd>
  <dt><b>limit</b> (<i>int</i>)</dt>
  <dd>This parameter specifies the maximum number of results you wish to retrieve per page. (Default is 10)</dd>
  <dt><b>page</b> (<i>int</i>)</dt>
  <dd>This parameter specifies the page of results you want to retrieve, where each page contains a specified number of objects based on the value of the "limit" parameter. (Default is 0)</dd>
  <dt><b>sort</b> (<i>string</i>)</dt>
  <dd>The sort parameter is a query parameter that allows you to sort the results of your search based on a specific field.<br>
      <code>e.g.: reputation</code></dd>
  <dt><b>order</b> ("asc" or "desc")</dt>
  <dd>The order parameter specifies the order in which the results should be sorted based on the specified "sort" parameter. It can take two values: "asc" for ascending order and "desc" for descending order. (Default is asc)</dd>
  <dt><b>id</b> (<i>string</i>)</dt>
  <dd>The "id" parameter is used to specify the ID of the entity for which you want to retrieve comments through this API endpoint.</dd>
</dl>

To get a comment, use a <b class="label label-blue">GET</b> request, for example:

```bash
curl -X 'GET' \
  'https://intelligence.threatwinds.com/api/search/v1/comments/malware-a208c4b33a1763284ce9a4584efa296372082ba82ee174597092f972767de163' \
  -H 'accept: application/json'
}'
```

### Returns
<h3> <b class="label label-green">Code 202</b> Accepted</h3>

**Return a list of comments as Response**

This API endpoint returns a list of comments that are associated with the specified entity.

### Fields of the response:

* **pages** (_string_):  The total number of pages in the result set.<br>
* **items** (_string_) The total number of comments in the result set.
* **result** (_entity list_):  A list of hits that correspond to the comments that are associated with the specified entity.

_e.g.:_
```json
{
  "pages": 1,
  "items": 1,
  "results": [
    {
    "commentID": "NEED A REAL EXAMPLE"
    "comment": "Test",
    "entityID": "malware-a208c4b33a1763284ce9a4584efa296372082ba82ee174597092f972767de163"
}
  ]
}
```

### Errors

### Fields of the response

<dl>
  <dt><b> uuid </b> (<i>string</i>)</dt>
  <dd>
    The id of the error. <i>e.g.: 6070686d-917d-44bb-ad11-02345a7f1939</i>
  </dd>
  <dt><b> error </b> (<i>string</i>)</dt>
  <dd>
    The description of the error. <i>e.g.: "duplicated key not allowed"</i>
  </dd>
</dl>
<h3><b class="label label-red">Code 400</b>Bad request</h3>

The HTTP status code 400, also known as a "Bad Request" error, is typically returned when the server is unable to process the client's request due to issues with the request parameters.

For example:

```json
{
  "uuid": "cf096e86-347f-4ddf-af1c-0c673a004211",
  "error": "value cannot be empty"
}
```
<h3><b class="label label-red">Code 401</b>Authentication required</h3>

The 401 error code indicates that you need authentication to do this request. See <a> Authentication API Page</a> for more details.

For example:

```json
{
  "uuid": "4b2561eb-2b4b-43ee-a272-643df36e2c5b",
  "error": "authentication required"
}
```

<h3><b class="label label-red">Code 403</b>Forbidden</h3>
A 403 error code, also known as a Forbidden error, indicates that the server understood the client's request, but it is refusing to fulfill it. The server can return a 403 error if you do not have enough permissions to make this operation, it suspects that the client is making too many requests, or if the client is using an IP address that is banned or blocked by the server. If the error persists you should contact support for further assistance.

For example:
```json
{
  "uuid": "75827622-bb05-46b5-80a9-344a6df0e001",
  "error": "unauthorized"
}
```

<h3><b class="label label-red">Code 404</b>Not found</h3>

The HTTP status code 404, also known as a "Not Found" error, occurs when the search could not find a match for the given parameters.

For example:

```json
{
  "uuid": "e23611e9-2974-4cd7-a08b-47fe7d35fa9a",
  "error": "entity not found"
}
```
<h3><b class="label label-yellow">Code 500</b>Internal server error</h3>
We get this code when an internal server error occurs. This is not session related.