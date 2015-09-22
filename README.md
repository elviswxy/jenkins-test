# Jenkins Test Project

We live and breathe Test Driven Development, so a CI server continuously running our tests and building our apps is vital. This project introduces the setting process for a Jenkins project which used to manage your own project. You can use Jenkins test your code and depoly your project.

##[Jenkins Installation](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)

On Debian-based distributions, such as Ubuntu, you can install Jenkins through apt-get. 

Recent versions are available in an apt repository. Older but stable LTS versions are in this apt repository.

You need to have a JDK and JRE installed. openjdk-7-jre and openjdk-7-jdk are suggested.

Please make sure to back up any current Hudson or Jenkins files you may have.

### Installation

```
wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

### Upgrade

Once installed like this, you can update to the later version of Jenkins (when it comes out) by running the following commands:

```
sudo apt-get update
sudo apt-get install jenkins
```

## GitHub Pull Request Builder Plugin Installation

In an effort to strengthen our codebase, Rent the Runway has implemented test execution against all pull requests. We used the GitHub Pull Request Builder Plugin to trigger Jenkins jobs on every pull request.

To do this go to `Jenkins` → `Manage Jenkins` → Manage Plugins and click on the `Available` tab. Search for `GitHub Pull Request Builder` and install it.

After installing the plugin and rebooting your Jenkins it’s time to configure the plugin. Go to `Jenkins` → `Manage Jenkins` → `Configure System` and scroll down to the `GitHub Pull Requests Builder` section.

To get going you only need to enter a GitHub access token for the GitHub user you would like to access your GitHub repositories from Jenkins. It’s probably a good idea to use a dedicated user for this purpose.

Beware that the user Jenkins will be using to connect to GitHub must be either the repo owner or have “Push, Pull & Administrative” permissions.

Note: if you don’t have an access token yet you can fill in your GitHub username and password under “Advanced…” and have Jenkins create the access token.

## Jenkins Project Configure

Now to actually allow Jenkins to build your projects pull requests we’ll need to setup a new Jenkins Project and configure it as follows:

1. Create a new Jenkins service.
![pic5](https://github.com/elviswxy/jenkins-test/blob/test/pics/snapshot5.png)
Create a jenkins project name. For example, we call it `OpenBidder` in our project. Select the first option and create the button, you will get more details for project config.

2. Jenkins project config
In the GitHub project field fill in the URL to your GitHub project `https://github.com/<username>/<project>/`, for example, `https://github.com/WebSciences/OpenBidder`
Under `Source Code Management` select `Git` and enter the fields as follows:
![pic6](https://github.com/elviswxy/jenkins-test/blob/test/pics/snapshot6.png)
You could find more options in `Advance setting`, when you connect to private repository, you need to add the credential certification.

3. Under `Build Triggers` make sure to check the following settings and white list some users:
![pic7](https://github.com/elviswxy/jenkins-test/blob/test/pics/snapshot7.png)

4. Now perform your regular setup of what Jenkins should actually do, such as run a script test. A script under version control running the entire testsuite. The final step to get things going is to enable the `Set build status on GitHub commit` post-build action.
![pic8](https://github.com/elviswxy/jenkins-test/blob/test/pics/snapshot8.png)

##Set Webhooks configuration

In Github repo you also need to change the setting for the project which used to tracing your every pull request. During the project, you could modify the webhook configuration anytime.

1. Click `Add Webhooks`
![Webhooks & services](https://github.com/elviswxy/jenkins-test/blob/master/pics/snapshot1.png)

2. Set the `Payload URL` to your own jenkins url, and select the `Content type`.
![pic2](https://github.com/elviswxy/jenkins-test/blob/master/pics/snapshot2.png)

3. After these cofig, you need to select the individual envent for the project.
![pic3](https://github.com/elviswxy/jenkins-test/blob/master/pics/snapshot4.png)
4. When you finished the configuration, the system will send a test request to your jenkins server.

![pic4](https://github.com/elviswxy/jenkins-test/blob/master/pics/snapshot3.png)

## Conclution
With all of the steps above, this job should be triggered every time that a pull request is created against the monitored GitHub repo. Now whenever you open a new pull request or add some commits to an existing pull request Jenkins will try to perform a merge build and report the result to GitHub. Add your tests under the Build steps, and when the tests finish running, the status will be updated on the Pull Request. Now all your pull requests should look like this:
![pic9](https://github.com/elviswxy/jenkins-test/blob/test/pics/snapshot9.png)
