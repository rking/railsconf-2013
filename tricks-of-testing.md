# Tricks of Testing - Tests are making people unhappy; how to fix that
— Sandi Metz

Unit Tests: Goals
- Thorough
- Stable
- Fast
- Few - “Most parsimonious expression of the proof of the code”

## Messages

Message Origins
- Incoming
- Self↔Self
- Outgoing

Message Types
- Query
- Commands
(Conflating these two is considered bad)

## Covering all types of messages

Test *Incoming Query Messages* (`#gear_inches`) by
- making *assertions*
- about *what they return back*
- (Interface, not implementation)

Test *Incoming Command Messages* (`#set_cog`) by
- making *assertions*
- about *side effects*

Don't test *Self↔Self* Messages
- Is an anti-pattern
- But break the rule if it saves *$$$* during dev
- As time passes, these tests just resist change.
- “# If theses tests fail, delete them”

Don't test *Outgoing Query messages* (`Wheel#diameter`)
- Don't assert the return value, or even expect them to be sent
- “If a message has no visible side-effects, it's invisible to the rest of the app.”

Test *Outgoing Command Messages* (`observer.changed(something)`)
- Don't assert the side effect (e.g. don't verify that the `observer` changed the database) — this is an integration test
- Test that the message got sent
- Depends on the interface, betting that the interface is more stable than the side-effect
- Break rule if it's easy to do

“I am fully aware that I used ‘Mock’ and ‘Stable’ in the same sentence.” — Sandi Metz

What happens if `observer` stops implementing `#changed`? ⇒ Pain (API Drift)

Gems to automatically ensure mocks are used:
https://github.com/psyho/bogus
https://github.com/benmoss/quacky
https://github.com/xaviershay/rspec-fire
https://github.com/cfcosta/minitest-firemock

Good tests insist on simplicity.