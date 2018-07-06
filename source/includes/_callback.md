# Callbacks

``` ruby

# Sample redirect URL
redirect_url = "https://www.tapresearch.com/router/customers/fdbe1666a0146f54d85dbc90a5f12552/cps/complete?tid=53b183dd1a729fa04acd9ba2283af896"

# Generate HMAC-SHA1
api_secret = "f81324b50c807cd7118ffe32a34a6681"
digest = OpenSSL::Digest.new("sha1")
sha1 = OpenSSL::HMAC.hexdigest(digest, api_secret, redirect_url)

puts sha1 # e48ad262a413283078f5841cb3beb8d75def03a2

redirect_url += "&tr_sech=#{sha1}"

```

<aside class=info>
Your customer ID and API secret can be found via the dashboard after you log into your account on the TapResearch website.
</aside>

These are the routes you will need to use when you redirect a respondent back to TapResearch.

* Complete: https://www.tapresearch.com/router/customers/#{CUSTOMER_ID}/cps/complete?tid=#{TID}&tr_sech=#{SECURITY_HASH}
* Over Quota: https://www.tapresearch.com/router/customers/#{CUSTOMER_ID}/cps/over_quota?tid=#{TID}&tr_sech=#{SECURITY_HASH}
* Everything else: https://www.tapresearch.com/router/customers/#{CUSTOMER_ID}/cps/disqualified?tid=#{TID}&tr_sech=#{SECURITY_HASH}

Parameter | Type | Description
--------- | ---- | -----------
(customer_id) | String | The unique identifier associated with your account.
tid | String | Unique transaction identifier that is passed to you on survey entry.
tr_sech | String | HMAC-SHA1 security hash generated using the redirect URL (less the tr_sech parameter) and your API secret.






