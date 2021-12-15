# CC:Next

## About

Our intent here is to provide bleeding edge builds of [CC:T](https://github.com/cc-tweaked/CC-Tweaked) with some extra features from pull requests thrown in. We expect to have bugs and issues and that's the point, we also are not holding to ourselves to the same version migration requirements that CC:T has.

## Quality

Being bleeding edge there will be a bit less quality on newer features, translations come to mind but balance and other things are also considerations. This is somewhat the point of CC:N, to find what parts of a PR needs to change from a gameplay point of view (with the traditional PR code review process doing code quality and such).

## Version Numbering System

Since we expect to have multiple diverging concurrent releases we need a bit of a different versioning system, here's a breakdown:
`cc-tweaked-<MC version>-<CC:T version>+<CC:T repo commit>+<CC:N repo commit>+(<extras>)`
<!-- TODO: change cc-tweaked to cc-next just to be extra clear for not being mainline CC:T -->

* `MC version`: the version of MC that the mod is made for
* `CC:T version`: the version of CC:T that this build descended is from, added purely for human readability
* `CC:T repo commit`: the latest short commit id that this build has in common with the main CC:T repo
* `CC:N repo commit`: the commit id that this build was made from on our repo
* `extras`: the extra feature/s and PRs that are in this build, we prefer PR numbers but sometimes have to break this rule. Some examples:
  * `PR5`: this means that Pull Request 5 on the CC:T repo has be merged into this build
  * `Cobalt.PR5`: this means that Pull Request 5 on the Cobalt repo has be merged into this build ([Cobalt](https://github.com/SquidDev/Cobalt) is the lua engine that CC uses, some language features of CC:T come from here)
  * `PR5,PR6,PR7`: this is how we will represent multiple PRs being merged into the CC:N build, but most of the time we will just have one

So a complete example will look like this `cc-tweaked-1.16.5-1.99.0+c4024a4+2044ac4+(Cobalt.PR50)`. <!-- TODO: replace the second commit with a real one -->
<!-- TODO: build server will need to be able to fill in these, the CC:N commit will be difficult -->

## Branch Naming System

Our branches have a similar naming system as our versioning and is simply `CCN/<MC version>+<extras>`, so the above example version would be tracked on the `CCN/1.16.5+Cobalt.PR50` branch. With Cobalt branches being `CCN/<extras>` where extras just refers to Cobalt PRs, sometimes with a note on what that PR implements. *All branches should start with `CCN/`* this helps us spot them amongst the branches that we inherit from upstream, the exception to this are the basic MC version branches that track the upstream. Another exception is `CCN/main` which exists just for the README, workflows and other bits for GitHub.

All CC:N branches will do nightly builds (once it's set up, for now all is manual<!-- TODO: don't forget to edit this -->), pulling the latest from their PRs and from their upstream branch on the CC:T repo.

<!-- 
TODO:
* set up automatic nightly builds of CC:T
  * GH actions and action artifacts
    * https://nightly.link/ already installed on repo

* auto delete old builds?

* what if the PR updates without CC:T itself getting a new commit, we would have to detect that and would want a way to identify the new build

* set up automatic merges of PRs made against CC:T
 -->
