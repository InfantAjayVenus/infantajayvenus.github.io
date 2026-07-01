**Tags**: #web-dev #git

---

#### Feature Branching
1. Create a feature branch from `main`.
2. Work independently on the main branch.
3. Create PR to main from feature and merge into main branch.

#### Git Flow
1. Dev, Feature, Release, Hotfix branches are standardized.
2. When starting a feature, branch off of `develop` branch.
3. Upon completion, merge back into `develop`
4. When preparing a release, branch off feature from `develop`.
5. After testing and bug fixing, merge into both `main` & `develop`.
6. When creating hotfixes, branch off of `main`.
7. Upon fixing and testing, merge into both `main` & `develop`.

#### Gitlab flow
1. `main` branch with production code.
2. Other environment branches based on requirements like `stageing`, `production` etc.,
3. Create a feature branch off of `main`. 
4. Merge back to `main` upon completion.
5. Deploy to other environments from `main`.

#### Github flow
1. Branch from `main`.
2. Work locally, commit as frequently as possible.
3. Open a PR to `main`.
4. Merge to `main` and deploy

#### Trunk-based Development
1. Make minor changes to `main` and commit.
2. If feature branches are created they are merged back to `main` within a day.
3. CI setup to run tests on every commit.

#### Stacked Diffs
1. Start working on a feature.
2. Upon completing a small part, create a PR.
3. Continue with the Develoment.
4. Repeat steps 2 and 3 until the development is done.

#### Merge vs Rebase
Merge merges the history together by ordering the source branch and target branch commits in chronological order.

Rebase, moves all the commits of the source branch from the point of deflection on top of the target branch.

---
Ref: https://newsletter.techworld-with-milan.com/p/git-branching-strategies?ref=dailydev