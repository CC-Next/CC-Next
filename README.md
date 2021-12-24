# CC:Next

<!-- TODO: workflows

badges ![status](https://github.com/CC-Next/CC_Next/actions/workflows/<WORKFLOW_FILE>/badge.svg)


Each branch needs to
	Pull (rebase?) from upstream
	Pull (rebase?) from its PR (if it has one)
    Fetch custom Cobalt jar (if required)
        lua 5.2 - https://github.com/CC-Next/Cobalt/releases/download/0.5.4%2B859205c%2B484ae62%2B(PR50)/Cobalt-0.5.4+859205c+484ae62+.PR50.jar
	Build
	Test?
	Upload build artifact (and test log?)

Might not be a bad idea to add the commit ids to the artifact names, the builds to take a while and if people are too quick they might grab a build while things are in progress.
    Might want to just upload the mod jar too (skipping the other bits)

* auto delete old builds?

* find a way to trigger builds that isn't just nightly

* automatically make new branches when CC:T has a new PR

* auto build docs and host them somewhere (need to edit these files, look for "tweaked")
    * ./illuaminate.sexp
    * ./package-lock.json
    * ./package.json
    * ./doc/index.md
    * ./

* upload to curseforge and stuff? copycat support? (will need to edit, look for "tweaked")
    * ./build.gradle
    * ./rollup.config.js

TODO: the following files reference CC:T and I'm reluctant to change them
    * ./src/main/resources/data/computercraft/lua/rom/motd.txt
    * ./src/main/java/dan200/computercraft/core/apis/http/request/HttpResponseHandle.java
    * ./src/main/java/dan200/computercraft/api/lua/GenericSource.java
    * ./doc/stub/os.lua
    * ./src/main/resources/data/computercraft/lua/rom/programs/http/wget.lua
    * ./src/main/resources/data/computercraft/lua/rom/programs/http/pastebin.lua
    * ./src/main/resources/data/computercraft/lua/rom/help/whatsnew.md
    * ./

-->



## About

Our intent here is to provide bleeding edge builds of [CC:T](https://github.com/cc-tweaked/CC-Tweaked) with some extra features from pull requests thrown in. We expect to have bugs and issues and that's the point, we also are not holding to ourselves to the same version migration requirements that CC:T has.

## Link To Builds
![GitHub last commit (branch)](https://img.shields.io/github/last-commit/CC-Next/CC-Next/mc-1.18.x?label=updated)  ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/CC-Next/CC-Next/update-and-build)  [![download](https://img.shields.io/badge/download-latest%20jars-brightgreen)](https://nightly.link/CC-Next/CC-Next/workflows/update-and-build/CCN%2Fmain)

If your download's commit ID doesn't match the repo's then wait a while and download again, the builds can take a little while (> 7 mins for some).

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
<!-- TODO: from @Merith-TK : `cc-tweaked_<version>_<commit>-mc<version>-ccn_<commit>-<extras>` -->

## Branch Naming System

Our branches have a similar naming system as our versioning and is simply `CCN/<MC version>+<extras>`, so the above example version would be tracked on the `CCN/1.16.5+Cobalt.PR50` branch. With Cobalt branches being `CCN/<extras>` where extras just refers to Cobalt PRs, sometimes with a note on what that PR implements. *All branches should start with `CCN/`* this helps us spot them amongst the branches that we inherit from upstream, the exception to this are the basic MC version branches that track the upstream. Another exception is `CCN/main` which exists just for the README, workflows and other bits for GitHub.

All CC:N branches will do nightly builds (once it's set up, for now all is manual<!-- TODO: don't forget to edit this -->), pulling the latest from their PRs and from their upstream branch on the CC:T repo.
