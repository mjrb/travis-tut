# ci and automated testing tutorial
automated testing allows us to make scripts to automatically test our code
this makes it easy to find bugs we may reintroduce to old code with future changes.

Continous Integration (CI) is when you set up a testing enviroment that can
automatically run tests once builds are pushed to github. you can then use
a github feature to potentially require a pull request passes all the tests before
it merges into master. this way you know master allways passes all the tests.

## setup
- make sure you have node installed (alteast v10)
- run `npm install`

## jest specifics
this tutorial uses the jest testing library, which automatically finds tests by looking
though the \_\_tests\_\_ folder. you can run the included test by executing `npm test`.
see `__tests__/sumtest.spec.js` for more details. also here is a good [reference](https://www.valentinog.com/blog/jest/) for more info

## travis specifics
once the travis integration is setup, travis will look at the travis.yml in your repo
for the steps to take in order to run your tests. travis also has the option `os: osx`
for runing tests in a macos enviroment https://docs.travis-ci.com/user/tutorial/

## setting up travis for your fork
- go to [https://travis-ci.com](https://travis-ci.com)
- login with github
- add a new repository
- activate github app
- click on the travis-tut fork
- click on setings
- the default settings should be fine but you can also add enviroment variables to
  provide secrets that shouldn't be public that you need for testing. like api keys
- try pushing a change and watch it build

## more interesting things
- you can also setup enviroment variables in the travis settings.
  - this allows you to add secret config variables that you can use during testing
    without having them publicly in the repo
  - the default setting is to not show them in the log, so even if you do accidently
    print them in the public log it will display `[redacted]` instead of your secret
	api key
- branch protection/merge requests
  - you can configure github to force people to push code to a branch and then merge
    it into master. it's highly suggested to do this and also require code review
	which will improve code quality
  - in the branch protection settings you can also require that the travis tests pass
    so that you don't merge in broken code
- travis also allows you to have sidecar services like databases that the application can use
  while its undergoing tests
- it's also not limited to testing, you can also have travis
  - run a linter on your code
  - calulcate code coverage
  - deploy your code to your server
