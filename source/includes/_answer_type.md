# Answer Types

When you make a request to our qualifications route, there will be an answer_type field returned with every object.
The answer_type value will determine how the campaign_qualifications pre_codes array is constructed.

### When answer_type is a 0 or 1
Pass in every pre code that qualifies a respondent. For example, the gender qualification has two accept answers,
male and female, with pre codes of 1 and 2, respectively.

If you passed in:

* 1: target only males
* 2: target only females
* 1 and 2: target both males and females

### When answer_type is equal to 5
Qualifications with answer_type 5 will return with an empty qualification_answers array. You will need to construct
an array of customer values.

* Age: Pass in an array of ages. `I.E. Pass in [ 18, 19, 20, 21, 22, 23, 24 ] if you are looking to target respondents that are between the ages of 18 and 24.`
* Zip: Pass in an array of zip codes. `I.E. [ "95120", "94089" ]`
