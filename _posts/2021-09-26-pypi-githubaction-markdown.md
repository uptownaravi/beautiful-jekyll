---
layout: post
title: pypi packages with GitHub actions
subtitle: using github actions to build a python package and publish to pypi
gh-repo: uptownaravi/encoder
gh-badge: [star, fork, follow]
tags: [devops, github, python]
comments: false
---

GitHub actions are a great way to get your ci/cd done.

In this post we will see how we can run ci flow with lint, package, test and publish a python package. Using the sample repo 
```
https://github.com/uptownaravi/encoder
```
This will help you get started on a simple GitHub action for a pypi package.

Refer to [GitHub Workflow Syntax](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions) for documentation.

Workflows have jobs and steps under that, our workflow is defined in the file 
```
https://github.com/uptownaravi/encoder/blob/main/.github/workflows/pythonaction.yml
```

This is configured to run when a commit happens on the main branch.

The steps in the workflow include 
* checkout (using predefined action actions/checkout@v2 )
* Install dependencies required in the workflow
* run pylint for linting
* build the pypi package
* get version from version file in the repository ( this will be used with the test step )
* install the package from dist/*
* run unit test
* publish package to pypi ( using pypa/gh-action-pypi-publish )
* install package from pypi URL to verify

Version is read from the version file both on the setup.py and in the workflow during install/test

Once we make a commit on the main branch, we can see the workflow run on the actions tab of the repository

![GitHub action tab](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/okjot2qx6jjsovv72es5.png)

After the job run we can see our package in pypi webpage. 
![pypi webpage](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nvf78mqlan7iyfupklu7.png)


### Note
{: .box-note} if you notice the workflow file we can see a secret being used with in package upload. Add a GitHub secret called  PYPI_TOKEN which has the token from pypi account. Check https://pypi.org/help/#apitoken for steps to generate the token
