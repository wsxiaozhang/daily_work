
# Deploy Gitlab on ICp


###prepare the helm sever:

execute below commands:

```
root@hchenk8s2:~# helm init -c
Creating /root/.helm/repository/repositories.yaml
```

Then copy the gitlab packages in /root/.helm/repository/local and start the helm serve(the package can be download from [github](https://github.ibm.com/qiujian/cfc-charts/blob/icbc/gitlab-ce-0.1.7.tgz))

```
root@hchenk8s2:~/.helm/repository/local# helm serve --address 9.111.254.208:8879
Regenerating index. This may take a moment.
Now serving you on 9.111.254.208:8879
```

Note: replace 

Add the URL in ICp repositories in System -> Reposistories

![expose form others](img/repositories.png)

Install the Gitlab package from AppCenter

![expose from others](img/gitlab_appcenter.png)
![expose from others](img/gitlab_install.png)

Check if the gitlab application was ready.

![expose from others](img/gitlab_application.png)


access the gitlab by click the link.

![expose from others](img/gitlab_detail.png)

gitlab will ask for new password set.

![expose from others](img/gitlab_access.png)

the we can login gitlab.

![expose from others](img/gitlab_login.png)



Then start to deploy the jenkins.

Click the appcenter and select the jenkins.

![expose from others](img/jenkins.png)

after the application deployed, in workloads -> application page, select the jenkins application and click the link of name to view the details.

![expose from others](img/jenkins_detail.png)
Click the endpoint link to open the jenkins UI

![expose from others](img/jenkins_ui.png)
Then start to config the gitlab plugins


first install the gitlab plugins and the plugins can be download from [URL](https://wiki.jenkins.io/display/JENKINS/GitLab+Plugin)

create the api token on gitlab

![expose from others](img/api_token.png)
Add api token in jenkins

![expose from others](img/jenkins_apitoken_setting.png)
Then test the gitlab connection by click the button

![expose from others](img/test_jenkins_connection.png)

Create a sprintboot reposistory from [IBM Liberty](https://liberty-app-accelerator.wasdev.developer.ibm.com/start/) and clone the SprintBoot project


Add the Git project in jenkins

![expose from others](img/general.png)
![expose from others](img/general2.png)
![expose from others](img/general3.png)

and save the project

Then we can start the build by trigger a jenkins job

![expose from others](img/build.png)




#How to prepare the maven repository locally.

prepare the settings.xml file and upload to your gitlab, the file like this:

```
hchenxa@hchen-mac:~/Documents/hchenxa/src/hchen/sprintBoot$ cat settings.xml

<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <mirrors>
    <mirror>
      <id>nexus</id>
      <name>nexus</name>
      <url>http://130.211.130.194:8081/repository/maven-public</url>
      <mirrorOf>*</mirrorOf>
    </mirror>
  </mirrors>
</settings>

```

and place the file in your gitlab root path

```
hchenxa@hchen-mac:~/Documents/hchenxa/src/hchen/sprintBoot$ ll -rt
total 8352
drwxr-xr-x  7 hchenxa staff     238 Jul 21 13:26 ../
drwxr-xr-x  4 hchenxa staff     136 Jul 21 13:26 src/
-rw-r--r--  1 hchenxa staff     454 Jul 21 13:26 settings.xml
-rw-r--r--  1 hchenxa staff    2955 Jul 21 13:26 pom.xml
-rw-r--r--  1 hchenxa staff    1041 Jul 21 13:26 icp-deployment.yml
-rw-r--r--  1 hchenxa staff 8534562 Jul 21 13:26 apache-maven-3.5.0-bin.tar.gz
-rw-r--r--  1 hchenxa staff     402 Jul 21 13:26 Dockerfile
drwxr-xr-x  9 hchenxa staff     306 Jul 21 13:26 ./
drwxr-xr-x 12 hchenxa staff     408 Jul 21 13:27 .git/
```

then config the maven repository use local repository:


![expose from others](img/local_repository.png)


