# GitHub Actions workflow template for LaTeX package testing and building setup using the l3build framework (minimal)

This is a template for package maintainers to add automated workflows to a l3build based repository.

This work was presented in a workshop at [TUG 2024](https://www.tug.org/tug2024/) and a corresponding article was published in [TUGboat 140](https://tug.org/l/peischl-cicd2024).
The linked repository includes a list of all variants of CI templates provided like this one.

## Usage

To use this repository create your own one using this template and replace/modify package and l3build script.

Alternatively you can copy the workflow configuration (`.github/`) to your repository and adapt the files according to your needs.

## Contents

- The minimal TeX Live setup is done with two different actions
  -[`zauguin/setup-texlive-action`](https://github.com/zauguin/install-texlive) - up to date TeX Live including recent updates
  -[`teatimeguest/setup-texlive-action`](https://github.com/teatimeguest/setup-texlive-action) - historic TeX Live versions for testing
- Minimal example LaTeX package `mypackage` providing the command `\TheAnswer`. Check `mypackage.dtx`.
- A test case for the package. Check `testfiles/verify-answer.*`.
- Upload of the package documentation. The latest version of the main branch, can be found at [mypackage.pdf on branch pdf-output](../pdf-output/mypackage.pdf)
- This version also includes a deployment workflow: [`deploy.yaml`](.github//workflows/deploy.yaml).
  It only will run if a tag was specified and uses [zauguin/ctan-upload](https://github.com/zauguin/ctan-upload).

  The workflow contains 3 jobs:

  1. Build in the same way as the main workflow does. Extended by a dry-run for the CTAN upload to validate.
     This requires a ctan.ann file and the package name to be configured, see variables configured in the workflow file.
  2. Create a GitHub release. This job requires write access to the repository.
  3. CTAN upload (dry-run by default)
      To enable you have to adjust your data within [`deploy.yaml`](.github//workflows/deploy.yaml)
      For a successful workflow run you have to add:
        -[ ] email, defaults to `${{ secrets.CTAN_EMAIL }}`
        -[ ] uploader, defaults to `${{ secrets.CTAN_NAME }}`
     For productive use additional variables need to be configured. See comments in [deploy.yaml](.github//workflows/deploy.yaml) for details.

## LICENSE

We want this to be used. You can find all this within the documentation. But in case you care, this work is licensed under MIT License.
