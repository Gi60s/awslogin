# awslogin
Python script for CLI and SDK access to AWS via ADFS while requiring MFA access using https://duo.com/

## History and Purpose
BYU used to use the great [aws-adfs](https://github.com/venth/aws-adfs) CLI tool to login to our AWS accounts.  It worked great, especially the DUO 2FA support.  Eventually, we decided to write our own similar tool but make it BYU-specific so that we could taylor it to our needs (which basically means hard-code certain BYU-specific things) and remove some of the required parameters.  Since this tool will be used by BYU employees only we had that option.  We then morphed it a little more for our use cases.  This isn't something that you could use outside of BYU, sorry.

## Installation
* Install Python 3.x using your preferred method.
  * See https://www.python.org/downloads/ for a windows installation method.
  * In linux you may be able to use apt, rpm or https://www.python.org/downloads/.
  * In Mac you can use homebrew, macports or https://www.python.org/downloads/.
* Run `pip3 install byu-awslogin`

## Usage
awslogin defaults to the default profile in your ~/.aws/config and ~/.aws/credentials files.  **_If you already have a default profile you want to save in your ~/.aws files make sure to do that before running awslogin._**

Once you're logged in, you can execute commands using the AWS CLI or AWS SDK. Try running `aws s3 ls`.
Currently, awslogin tokens are only valid for 1 hour due to the assume_role_with_saml AWS API call has a max timeout of 1 hour.

To use it:
* Run `awslogin` and it will prompt you for the AWS account and role to use.
* Run `awslogin --account <account name> --role <role name>` to skip the prompting for account and name.  You could specify just one of the arguments as well.
* Run `awslogin --profile <profile name>` to specifiy an alternative profile
* Run `awslogin -- --help` for full help message

## Reporting bugs or requesting features
* Enter an issue on the github repo.
* Or, even better if you can, fix the issue and make a pull request.

## Deploying changes
* Update the version in the VERSION file.
* Commit the change and push.  Handel-codepipeline will run the automated tests and if they pass it will build and upload a new version to pypi.

## TODO
* gracefully handle the error case when the duo push is rejected
* Add support for profiles
* Authenticate once for 8 hours and rerun `awslogin` to relogin
* Write tests
  * roles.py
  * assume_role.py
