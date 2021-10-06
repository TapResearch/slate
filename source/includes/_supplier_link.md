# Supplier Links

**Transaction ID**

Specify where you want this ID to appear using {ID}:
https://api.samplecompany.com/surveys/23423?id={ID}

Here is an example upon survey entry: 
https://api.samplecompany.com/surveys/23423?&id=46f8bb49ad688570abb84eafae38733d

This value must be passed back in the [status callback URLs](#callbacks).

**Respondent ID**

https://api.samplecompany.com/surveys/23423?respondent_id={RESPONDENT_ID}&id={ID}

This is the unique alphanumeric ID for this respondent.

**Retarget Identifier**

https://api.samplecompany.com/surveys/23423?retarget_id={RETARGET_IDENTIFIER}&id={ID}

{RETARGET_IDENTIFIER} will be replaced with the retargeting_id as provided in [Campaign Retargeting](#campaign-retargeting).

If a replacement_id is specified in [Campaign Retargeting](#campaign-retargeting), that value will be used instead.

**Respondent Demographics**

https://api.samplecompany.com/surveys/23423?id={ID}&age={AGE}&gender={GENDER}&zip={ZIP_CODE}&education={633}

{AGE} will be an integer.

{GENDER} will be either M (male) or F (female).

{ZIP_CODE} will be an alphanumeric string. 

Any {QUESTION_ID} from the [/qualifications](#get-a-specific-qualification) route may now be used as a substitution value. Any invalid values will be safely ignored. The URL example above has been updated with an example using the Education Level question_id.

For the above example upon survey entry the URL will look like this: https://api.samplecompany.com/surveys/23423?id=46f8bb49ad688570abb84eafae38733d&age=23&gender=M&zip=90210&education=10

**Security (optional)**

<aside class=info>
Your API secret can be found via the dashboard after you log into your account on the TapResearch website.
</aside>

We now support the creation of an HMAC-SHA1 security hash to be appended to the end of a Supplier Link using the substitution value {LINK_HASH} used in conjunction with a new parameter called security_hash.

The HMAC-SHA1 security hash should be generated using the fully constructed Supplier Link less the {LINK_HASH} substitution value and the customer’s API secret.

The {LINK_HASH} should always be the final value appended to a supplier link.

***Example***

Use the customer API secret and Fully Constructed Supplier link sans the {LINK_HASH} substitution value to generate the HMAC-SHA1 security hash. See [Callbacks](#callbacks) for an additional example.

* Supplier Link Format Example: https://api.samplecompany.com/surveys/23423?id={ID}&age={AGE}&gender={GENDER}&zip={ZIP_CODE}&education={633}&security_hash={LINK_HASH}
* Fully Constructed Supplier Link: https://api.samplecompany.com/surveys/23423?id=46f8bb49ad688570abb84eafae38733d&age=24&gender=M&zip=72758&education=4&security_hash={LINK_HASH}
* Fully Constructed Supplier Link with Security Hash: https://api.samplecompany.com/surveys/23423?id=46f8bb49ad288570abb84eafae38733d&age=24&gender=M&zip=72758&education=4&security_hash=3d2d...

Parameter | Type | Description
--------- | ---- | -----------
security_hash | String | HMAC-SHA1 security hash generated using the fully constructed Supplier Link less the {LINK_HASH} substitution value.


