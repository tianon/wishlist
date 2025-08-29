# [GitHub](https://github.com)

- "How do I know this person?" (contribution intersection between two users -- comments, commits, etc etc)

- ~~a way to "git clone" a commit (requires Git changes); you can pull up an "orphan" commit through the web UI, which is awesome, and you can then tag or branch it, but you can't clone it directly without doing one of those things first~~

- smarter diffs: code copies like "git diff" does (right now if someone commits an exact copy of a file that already exists in the repo, we get the full file contents all over again -- "git diff" can even be smart about a 90% or so copy, for example), diff already merged in target branch (think two people made the exact same PR at the same time and we merge one, but the other one is still open and still appears "mergeable" even though the change has already merged and the merge commit will be +0-0), etc

- ~~"docker pull github.com/tianon/..." (docker/OCI registry built-in! would unfortunately require bumping https://github.com/v2 who appears to just be squatting on a great URL)~~ ghcr.io is a good substitute, I suppose...

- force pushes that reference a PR or issue in their commit message making less comment spam on referenced ticket

- axe "+1" comments entirely (auto-convert to a ":+1:" reaction with a nice popup explaining why commenting nothing but "+1" is really poor form to help encourage better open source interaction habits); also/alternatively some way to not receive email notifications of useless "me too" comments

- expanded "partial" watching (omg love being able to watch just releases) -- only issues/PRs with a certain label, etc
  - ability to subscribe to just PRs or just issues (specific subset of "partial" subscription feature request); just PRs/issues matching a label (https://github.com/golang/go/labels/binary-size)

- ability to change issue/PR titles without breaking Gmail threads somehow (that's what prevents us from changing issue/PR titles actively now)

- auto-sync / lock a fork's "master" (rebasing is hard for many folks and sooo many contributors can't figure out how to rebase on the origin's master instead of their fork's master, which causes all sorts of haywire); it would also look better hygienically to see the latest upstream "master" content when viewing a fork if it's simply a PR vessel and not a true "fork"

- an option to not include (or to trivially purge post-fork) upstream's tags/branches during fork (I don't want or need *all* of upstream's poor repository maintenance baggage); I have scripts and one-liners to do this post-fork right now, but it's very manual and icky (and my "fork" is only a PR vessel, not really a fork!)

- "files changed" (diff view) tab/link on the new persistent PR bar

- ability to diff a file or directory between commits/tags/branches (a filtered "compare" view that's not so repo-focused, if you will); ala "git diff abc...def -- foo/ bar/"

- a way to make a team able to be @org/team mentioned by outsiders on outside repos (for official-images many groups, like Node.js, want a github org team to be the place they maintain the list of "image maintainers" but that makes it hard for us to @ them on PRs and issues /o\)

- optional expanded diffs in email notifications!  for example, GitLab's diff comment notifications include a full syntax highlighted code context display that's just great to look at (but they don't provide it for the initial PR notification, which IMO would be really nice too depending on the length of the PR diff)

- "git archive" and Git LFS working together in harmony somehow (https://github.com/git-lfs/git-lfs/issues/1322; although https://github.com/git-lfs/git-lfs/issues/1322#issuecomment-442074490 is :heart:) -- so I guess this one's already on "the list"

- a better way to report "spam" that isn't abusive (yet?); going through the full abuse process for someone sending a PR that's just adding a line of noise to a README feels like massive overkill so I've stopped reporting them (even though they are still spam)

- a way to lock a thread that only stops new comments / necro bumps (so reactions can still be added to existing comments)

- a page to list all my existing invitations (instead of having to get the URL from an email)

- ~~notification of comments on my gists (or gists I've starred)~~

- ~~commits on a repo showing a PR number from a fork as if it's in the origin (https://github.com/docker-library/official-images/commit/69c374aa980702d604a19712929f226b01984b37, for example, shows #185 which isn't accurate at all because it's from some random fork)~~

- "delete fork" is cool, but it needs to be a little smarter, like not suggest it when I have other PRs still open from the fork, and a way to tell it I never want to have that suggestion for a particular fork (a sticky fork, if you will)

- ~~notify PR author via email when CI / checks fail (otherwise they often don't come back to check after the pipeline finishes and they have a result)~~

- an ICS exporter for milestones (so they can show up in my calendar application natively)

- automatic artifact checksums (SHA256)
  - (automatic) checksums for assets in the releases API

- the ability to block https://github.com/apps/pull from ever showing up on anything in my organization (never link its PRs from commits, etc); it's like an abusive user I can't block

- ability to block unrequested/undesired outside user "approvals" (or otherwise edit/delete/dismiss them like normal comments)

- ability to auto-reset approvals on a force push

- ~~ability to review, approve, and mark as "merge when CI succeeds" (or some email notification if it doesn't) -- likely needs to either block the submitter from updating further or cancel the merge if they update~~

- ~~often curl/wget against releases artifacts will result in "403 Forbidden" (https://www.google.com/search?q=%22github-production-release-asset%22+%22403+forbidden%22)~~

- when a PR has a conflict, point to the commit/PR which created it (where possible)

- more control over what counts as a contribution (closing or commenting on issues, for example)

- actions: ability to generate "steps:" values (https://twitter.com/tianon/status/1253032501796147200, https://twitter.com/tianon/status/1253081994902134784)

- actions: something like "@weekly" or an evenly-distributed placeholder value (like Jenkins has) for scheduled crons (so they don't all run on Sunday at midnight or get manually distributed)

- actions: some way to mark builds as "authoritative" for their commit (such that if we do a build on a "push" event for a commit, we don't redo a build on a "pull_request" event for that same commit, or on another "push" event to another branch)

- repository language stats should be a graph so we can see the change in language ratios over time

- bot accounts should be a first-class citizen -- they should either be able to belong to an organization, or at least be "managed" by multiple users in some way so that they can be added to organizations/repos that require 2FA without needing to share 2FA tokens between the users who manage the bot account

- ability to restart single matrix job in github actions (instead of having to re-run all jobs for a single flaky leg)

- option to require confirmation on issue/PR closure

- if the diff of a PR against the base branch is (or becomes via force push, commits to the base branch, etc) empty, there should be a notice / notification on the PR saying so (for example, if the exact patch of a PR is committed or merged to master, that should be more obvious); see also the related dream, "smarter diffs"

- ability to archive an entire organization

- better ways to organize/manage/use saved replies (control of the order, keyboard shortcuts, replies that only show for comments within a particular organization, etc)

- contributors intersection (show me users who have comitted to both of two repositories); see also the related (but not quite the same) dream, "How do I know this person?"

- allow pushing to "refs/pull/NNN/head" if the contributor lets maintainers push to their PR (and redirect it to their branch behind the scenes); this would allow things like automated scripts to rebase someone else's PR

- a way to do a real rebase through the UI (instead of merging HEAD into the PR, which makes the commit history really tacky)

- on a failing Actions build, link me directly to the end of the log on the failing step (since otherwise I have to click in, find the failing matrix entry, click the failing step, then continue hitting "End" in the box until it gets to the bottom, then scroll back up to see the end of the log to see the actual error message)

- relatedly, when an Actions build fails, the email should list the specific jobs that failed, not just the first few jobs of the matrix whether they failed or not

- an email notification as a maintainer for "draft -> ready to review" state changes...

- multiple forks in a single user/org from the same fork base (for example, I have a fork of https://github.com/conchyliculture/acme-tiny-dns but I'd *also* like a fork of the original https://github.com/diafygi/acme-tiny, separately)

- "tianon force-pushed the xxx:yyy branch 3 times, most recently from FOO to BAR x days ago" needs some way to expand to show all three force pushes (at the very least so I can walk back to the original commit of the PR to check whether the final approach still matches the original)

- help with the creation/maintenance of a suitable `.mailmap` file (since GitHub has the full list of commit emails *and* knows which GitHub accounts they all map to, so could help combine them)

- some way to see what a person's profile said about who they are / where they work when they made a particular comment ("Why is the X of Y company commenting *that* on *this* issue??  Oh, they used to be at Z company.")

- ~~choose a name / rename a fork *during* forking (so there isn't ever even a redirect for the old name)~~

- a way to choose a PR as the target ref for a `workflow_dispatch` GHA trigger

- actions: a way for an "action" to know which commit it's building from (maybe Git being part of the platform itself instead of actions being downloaded a zip/tarballs? 🙃)

- actions: https://github.com/actions/runner/issues/1478 (blocks the ability to write "pure shell" actions -- Node.js is wild, and shouldn't be required; Docker/containers are great but limiting as an action source)
