An Intervention for ActiveRecord
Ernie Miller
@erniemiller
http://erniemiller.org/

There is a contrast between Martin Fowler's ‘Active Record’ (purported to simplify) and ActiveRecord (maybe you ♥ it at first, but then its complexity shows up).

Referenced

Magic requires conventions
Conventions require opinions
Opinions are not created equal

Compares ActiveRecord to the kind of magic from http://youtu.be/wTqsV3q7rRU

---

ActiveRecord hooks into `#after_initialize`

Persisted / save triggers are inconsistent

Major respect points to Ernie for advertising his Pull Request that blew things up and required a security patch.

tl;dr, `#inverse_of` is handy.

`#validates_uniqueness_of` lies.

“`#default_scope` must die.”

`lib/active_record/callbacks.rb`

    # That's a total of twelve callbacks, which gives you immense power to react and prepare for each state in the
    # Active Record life cycle.

# Prescriptions

Instead of using callbacks, just override methods + use `super`

Write AR docs, tests, issues, get informed.