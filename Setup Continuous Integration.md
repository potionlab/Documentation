# Setup Continuous Integration

## Goals

1. Setup continuous integration on [Travis CI](https://travis-ci.org/)
2. Tests should run for each build
3. Linting should run for each build
4. Via protected branches, merges should not be allowed on `master` unless the build passes continuous integration.

## Script Instructions

Use the `setup_xcode.sh` script at [thepotionlab/Scripts](https://github.com/thepotionlab/Scripts/). This performs the same steps as "Add Continuous Integration Files" in the "Manual Instructions".

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


