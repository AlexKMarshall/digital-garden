# Backend Integration Testing using Jest and Supertest

We want to do some integration tests to have confidence in all the pieces of our app working together. Particularly "plumbing" code that isn't easily unit tested.
In addition, with integration tests we can cover a large part of the code base in a single test making them good value for money. We are (fairly) free to refactor the middle of our app, so long as the endpoints don't change. This makes our tests a bit more useful and not so annoying to have to keep re-writing.

To do this for a Node web backend we should spin up a server and hit it over http. If we have a database hen we should probably hit that too. We at least want to hit our ORM.

Integration tests are slow so we idealy want to run them in parallel. But we don't want our tests to conflict. So this means using a separate server per test and a separate database per test.

Jest gives us an environment variable `process.env.JEST_WORKER_ID` that is a unique number per test file. So if we use that to append to our database name and server port we'll avoid collisions.

If we use supertest we can avoid providing a server port completely and supertest will just take care of all that for us.

It may be unnecessary to hit a real database, maybe we can instead use an in-memory DB so long as we still hit our real ORM models (as they have critical validation and logic in them). Haven't explored this yet. At hte moment it's easier to just use the real database. But if tests get big/slow, it may be worth looking into

#testing #jest #integration-tests #backend #database
