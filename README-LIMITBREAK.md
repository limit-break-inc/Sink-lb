# Deployment

Merging to main / master will trigger a deployment within cloudflare

Environments
Dev / Feature environments all share one environment called link.limitinternal.com/*
Prod is link.puzzlepanic.com/*


Site Token


NUXT_HOME_URL should be set to something we control like limitbreak.com.  This is used for requests that are invalid to redirect here


Test to ensure its working and secure
1. `curl -v X GET "https://link.limitinternal.com/api/verify" -H "Authorization: Bearer NEXT_SITE_TOKEN"` This should give you a redirect to an access application which is good
1. `curl -v X GET "https://link.limitinternal.com/api" -H "Authorization: Bearer NEXT_SITE_TOKEN"` This should give you a redirect to an access application which is good
1. `https://link.limitinternal.com` should redirect you to limitbreak.com
1. `curl -X POST "https://link.limitinternal.com/api/link/create" -H "Authorization: Bearer NEXT_SITE_TOKEN" -H "Content-Type: application/json" -d '{"url": "https://github.com/miantiao-me/Sink/issues/14", "slug": "issue14"}'` This should redirect you to an access application which is good
1. Any of the above from the allowed NATs should work per the access application policies.
1. Find a KV pair within the respective KV database within cloudflare
Make a request to `curl -v X GET "https://link.limitinternal.com/287wtv"` and confirm it redirects you to adjust or something like that.

