NewRelic was on Rails2, and wanted to upgrade.

- Did it in 2 months
- Amidst 2,000 commits, lines changed: +110k -25k
- Avoided regression

- Dual Boot of Rails2 + Rails3 is possible

```ruby
platforms :ruby_18 do
  gem 'debugger'
end
platforms :ruby_19 do
  gem 'ruby-debug'
end
```
…but then you have 2 `Gemfile.lock`s. So they [wrote a thing to switch between them](https://github.com/newrelic/rails3_upgrade/blob/master/lib/bundler/lockfile_dsl.rb)

Needed some additional conditionality/monkeypatching of Bundler directly in the Gemfile (which can't happen in a gem, because Bundler load predates the gem load).

Gated everything off an env var, `USE_RAILS_3=1`

```ruby
is_rails3 = ENV.include? 'USE_RAILS_3' # later, this default switched to checking `not USE_RAILS_2`)
```

Got it working far enough that the Rails 2 world was unaffected, and Rails 3 would try to boot (but didn't fully work), at that point integrated into `master`.

Got into the messy work of `config/{environment,application}.rb` …etc., having both modes, with `if is_rails3 / else` pairs.

Depended on tests, with both versions running in CI.

Upgrading gems:
- If possible, just upgrade gems for both versions (== one less thing changes when released)
- Monkeypatched/shimmed other gems and Rails ways (e.g. check `defined? super`)
  - Is gross, but is lesser of two evils (and is OK as long as you really are going to get rid of it)

"Branch by abstraction"

ActiveSupport::Deprectation silence

Just worked:
- Routes
- ActionMailer
Mostly worked:
- Models (had to flip STI settings for some)
- Views
Trouble with:
- `html_safe` bugs.
- Sessions
- Audit trail issue; due to a gem that needed a fix (and not having an automated verification of its effects)
- ActiveScaffold
- BackgroundJob instrumentation (they switched to Resque)

After all the work, almost everything was deployed except the actual Rails2→3 switch

Rollout:
- Spun up a staging server, with dual deployments
- Deployed a "canary", didn't have many errors (did have a small spike, but assumed to be a fluke), chose to ship it
- Normally deploy 1–5x/day, but on that day they paused other deployments
- Turned out the canary did find a real issue, debugged it by directly contacting a customer who triggered the exception (who was impressed by the apparently very-high level of support)

After:
- Expect apologies to devops
- Schedule time for firefighting
- Cleanup of code: 191 commits, +10k -30k

http://newrelic.com/rails3_upgrade
