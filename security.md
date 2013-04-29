# Security, by Andre 
https://twitter.com/indirect

Rails and Ruby have each had flurries of security releases.
- This snowballs, because security problems draw further scrutiny
- Issues are in fundamental gems, active\*/rack/etc, even rdoc

https://cve.mitre.org
https://nvd.nist.gov

Security's business value is comparable to physical insurance, where the worst case is catastrophic, but the normal cost is not so bad.

Much of it is not about outrunning the bear, but about being able to out run the other guy.

## Responsible disclosure

Reasons why companies don't do it:
- Hard for companies to bite the bullet on, because if they can keep a security problem quiet, no tangible negatives come back to that company
- Gives attackers an indirect reward

Turning this momentum around is a problem to be solved. One way is companies that offer rewards for finding security holes.
- Facebook offers minimum $500 reward, with no cap
- GitHub offers a minimum t-shirt
- Engine Yard: minimum nothing

## Publicizing Found Issues

Ask yourself two questions:
- Can I access something I shouldn't?
- Can I disable something for other poeple? (breaking your own data isn't as bad as breaking others')

If so, contact the author directly, first. This means a patch can be released concurrent with the announcement. Look for:
- a security policy
- an email in the `.gemspec` (TODO: figure out how to query this from the CLI)
- Email address from GitHub
- …when this fails: fix it yourself

## Your Own Gems