# Setup Continuous Integration

## Goals

1. Setup continuous integration on [Travis CI](https://travis-ci.org/)
2. Tests should run for each build
3. Linting should run for each build
4. Via protected branches, merges should not be allowed on `master` unless the build passes continuous integration.

## Instructions

Use [XCTestTemp](https://github.com/robenkleene/XCTestTemp/tree/master) as the reference repository.

1. Add the repository in [Travis CI](https://travis-ci.org/).
2. Copy over the `.travis.yml` file from the reference repository.
3. Copy over the `Makefile` from the reference repository.
	* You'll need to update the `SCHEME` in the `Makefile`.
	* If the target doesn't have tests, remove `test` from the `ci` job.
4. Commit those changes, after the continuous integration job runs on Travis, make the `master` branch on GitHub a protected branch that requires continuous integration to pass by copying the reference repository.
5. Add the build sticker to the `README.md` by copying from the reference repository (make sure to update the URL of the sticker).
6. Run `make lint` and fix any errors.
7. Run `make ci` and make sure it works.


