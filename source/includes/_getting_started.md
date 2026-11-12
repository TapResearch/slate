# Getting Started

Before you can begin consuming our API, you will need to contact **api_support@tapresearch.com** for an API token. This token will be used
 for authentication purposes described in the section below. The API only accepts tokens for active users of active customer accounts.

Use `https://www.tapresearch.com` as the base URL for all routes. There is no separate staging server: you build and test your
integration in production with the same token, as described in [Testing your integration](#testing-your-integration).

When you are ready to go live:

1. Make sure your campaign has at least one quota with `num_respondents` greater than 0.
2. Update the campaign's `status` to 2 (Active). From this point real respondents will start to enter your survey.
