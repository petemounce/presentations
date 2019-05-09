# Levelling up your continuous integration

Continuous integration (CI) can be more than just a thing that compiles and runs tests. It can teach your engineers many more things.

In this talk I'll describe how CI was improved from "runs-my-jobs-mostly" so that:

* environment drift is minimised, so that CI fails far less often for something that's not "engineer wrote code that failed a test".
* engineers can trivially see which CI jobs are on the critical path, to avoid wasting time speeding up the wrong test.
* engineers can query build logs to see when a test started failing (think git bisect but built into CI).
* engineers are able to assert that their workstation matches their CI environment, eliminating "works in CI, why not here?"
* engineers are able to visualise the health of their CI trivially.
* customers can now be better supported historically because builds can be reproduced years into the past.

I'll also talk to how this reduces the onboarding time and effort for fresh engineers into on-call rotas operating software in production.
