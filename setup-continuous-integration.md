# Setup Continuous Integration

## Goals

1. Continuous integration should run on [Travis CI](https://travis-ci.org/)
2. Tests should run for each build
3. Lint should run for each build
4. [Required status checks](https://help.github.com/articles/about-required-status-checks/) and [protected branches](https://help.github.com/articles/about-protected-branches/) should prevent merging into `master` unless the build passes continuous integration
5. A GitHub Access Token is provided to download Carthage binaries (this gets rate limited on Travis otherwise)
6. On Travis, to conserve resources we should only build pull requests, the `master` branch, and tags. The only reason we build `master` is that there is no way to build pull requests without also building `master`.

## Script Instructions

Use the `setup_xcode.sh` script at [repla-app/Scripts](https://github.com/thepotionlab/Scripts/). This performs the same steps as "Add Continuous Integration Files" in the "Manual Instructions".

## Manual Instructions

Use [XCTestTemp](https://github.com/robenkleene/XCTestTemp/tree/master) as the reference repository.

### Setup Continuous Integration

1. Add the repository in [Travis CI](https://travis-ci.org/).
2. Configure [protected branches](https://help.github.com/articles/configuring-protected-branches/) on the `master` branch, and mark the "Require status checks to pass before merging" for the Travis jobs (note that these won't appear until a Travis CI job has run).

### Add Continuous Integration Files

1. Copy over the `.travis.yml` file from the reference repository.
2. Copy over the `Makefile` from the reference repository.
	* You'll need to update the `SCHEME` in the `Makefile`.
	* If the target doesn't have tests, replace `test` with `build` in the `ci` job, like in [robenkleene/StringPlusPath](https://github.com/robenkleene/StringPlusPath/tree/master)
	* If your target has [Carthage](https://github.com/Carthage/Carthage) dependencies, add a `bootstrap` step, like in [robenkleene/BubbleUp](https://github.com/robenkleene/BubbleUp)
3. Copy over the `.swiftlint.yml` from the reference repository.

### Fix Continuous Integration

1. Checkout a new branch and commit those changes to it, after the continuous integration job runs on Travis, make the `master` branch on GitHub a protected branch that requires continuous integration to pass by copying the reference repository.
2. Add the build sticker to the `README.md` by copying from the reference repository (make sure to update the URL of the sticker).
3. Run `make lint` and fix any errors.
4. Run `make ci` and make sure it works.

### Setup Carthage Deployments

Binaries are much faster so we should use them over compiling in continuous integration steps.

#### Create Binaries for New Tags

Following [the steps](https://github.com/Carthage/Carthage#use-travis-ci-to-upload-your-tagged-prebuilt-frameworks) for setting up Carthage with Travis

#### Getting Around Rate Limiting

GitHub will prevent Travis from downloading binaries because of rate limiting. To get around this, we need to provide a `GITHUB_ACCESS_TOKEN`. Note that we should *only provide a GitHub access token to repositories that have Carthage dependencies!*

1. Make a GitHub access token under settings, developer settings, personal access tokens. You do need need to add any special access rights.
2. Add the personal access token to the `.travis.yml` file with `travis encrypt GITHUB_ACCESS_TOKEN=YOUR_ACCESS_TOKEN --add env.global`
