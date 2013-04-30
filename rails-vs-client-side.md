Noel Rappin - Comparing "Basecamp" vs "Discourse"
@noelrap, Master Space and Time with JavaScript

DHH's opening talk pretty much advertised for Rails/server-side apps, then wycats's was Ember.js/client-side. This talk compared the two approaches.

[rails::api](https://github.com/rails-api/rails-api) - Rails with the Views stripped out

- “Simplicity is being able to deal with components separately.”
- “Simplicity is using sipmle structures.”
- “Simplicity is consistency.”

- It's not clear that one side or the other requires less code.
- Both climes claim speed
  * Server-side: The number of times you access the server is (basically) the number of times the user interacts.
  * Client-side: Proportianal to the new data requirements (e.g. update on the client, then notify the server). Speed advantage when the link to the server is slow (e.g. conference wifi, mobile).

Turbolinks + cache_key approach ⇒ Pretty much to disrupt Rails the least
 
http://tablexi.com
http://tablexi.com/blog/category/xi-to-eye/ # weekly video thing?


---

rking's opinion: You have to master both before you can make a good decision.