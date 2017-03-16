# Authentication

```shell

Example Request

$ curl -D- -X GET -H "Authorization: Basic dGVzdEB0YXByZXNlYXJjaC5jb206NGMzMTg2Mjg4YWUyM2ZkOTY2MWNiNWRmY2NlMTkzMGU="
-H "Content-Type: application/json" http://staging.tapresearch.com/api/v1/campaigns

```

```ruby

Example Request

# Attach this to your Authorization header.
auth = "Basic" + Base64::strict_encode64("test@tapresearch.com:4c3186288ae23fd9661cb5dfcce1930e")


```

We use HTTP basic authentication combined with HTTPS to enforce access controls to secure resources. This means that we will check
the value passed in the 'Authorization' header to make sure you have access to the resource you are requesting.

The 'Authorization' header needs to be submitted in the following form:

`Authorization: Basic dGVzdEB0YXByZXNlYXJjaC5jb206NGMzMTg2Mjg4YWUyM2ZkOTY2MWNiNWRmY2NlMTkzMGU=`

The header can be constructed by following the steps below:

1. EMAIL_ADDRESS_YOU_PROVIDED:API_TOKEN
`Example: test@tapresearch.com:4c3186288ae23fd9661cb5dfcce1930e`

2. Base64 encode the string generated in step 1.
`Example: dGVzdEB0YXByZXNlYXJjaC5jb206NGMzMTg2Mjg4YWUyM2ZkOTY2MWNiNWRmY2NlMTkzMGU=`

3. Append Basic to the string generated in step 2.
`Example: Basic dGVzdEB0YXByZXNlYXJjaC5jb206NGMzMTg2Mjg4YWUyM2ZkOTY2MWNiNWRmY2NlMTkzMGU=`

<aside class="info">
The authorization header is **required** for every request.
</aside>