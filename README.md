# jenkins-test

##Set Webhooks configuration

Click `Add Webhooks`
![Webhooks & services](https://github.com/elviswxy/jenkins-test/blob/master/pics/snapshot1.png)

Set the `Payload URL` to your own jenkins url, and select the `Content type`.
![pic2](https://github.com/elviswxy/jenkins-test/blob/master/pics/snapshot2.png)

After these cofig, you need to select the individual envent for the project.

![pic3](https://github.com/elviswxy/jenkins-test/blob/master/pics/snapshot4.png)

When you finished the configuration, the system will send a test request to your jenkins server.

![pic4](https://github.com/elviswxy/jenkins-test/blob/master/pics/snapshot3.png)
During the project, you could modify the webhook configuration anytime.

##Set jenkins

Firstly, you need install jenkins into your own computer and modify the end port(8080) to your own end port.

Secondly, you could go to the jenkins page, and create a new jenkins service.

1, Create a jenkins project name. For example, we call it `OpenBidder` in our project.
2, Select the first option and create the button, you will get more details for project config.
3, In project url, type in the url address for you own project. For example, `https://github.com/WebSciences/OpenBidder`
4, In `源码管理`, select `git` then you will get the `git config file`, then set the config, when you connect to private repository, you need to add the credential certification.
In `Advance setting`,
