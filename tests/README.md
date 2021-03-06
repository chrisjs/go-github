go-github tests
===============

This directory contains additional test suites beyond the unit tests already in
[../github](../github).  Whereas the unit tests run very quickly (since they
don't make any network calls) and are run by Travis on every commit, the tests
in this directory are only run manually.

The test packages are:

integration
-----------

This will exercise the entire go-github library (or at least as much as is
practical) against the live GitHub API.  These tests will verify that the
library is properly coded against the actual behavior of the API, and will
(hopefully) fail upon any incompatible change in the API.

Because these tests are running using live data, there is a much higher
probability of false positives in test failures due to network issues, test
data having been changed, etc.

These tests send real network traffic to the GitHub API and will exhaust the
default unregistered rate limit (60 requests per hour) very quickly.
Additionally, in order to test the methods that modify data, a real OAuth token
will need to be present.  While the tests will try to be well-behaved in terms
of what data they modify, it is **strongly** recommended that these tests only
be run using a dedicated test account.

Run tests using:

    GITHUB_AUTH_TOKEN=XXX go test -v ./integration
