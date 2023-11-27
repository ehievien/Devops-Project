Either you can create your own files using the Github repositry : https://github.com/kushaggarwal/Webapp/blob/main/Jenkinsfile or else you can just fork this into your own github account

1. Go to dockerhub registary to create a new repository for storing the docker image.
2. Make sure to install Jenkins and git using the steps mentioned in Installation.md file
3. Go to Jenkins console and then to manage jenkins option to create the credentials for dockerhub and github
4. Click on Global credentials to add dockerhub credentials (username and password) with identifier "dockerhub"
5. Similarly add credentials for github reepository having the Dockerfile and Jenkins file if the reepository is private
6. Update the Jenkins file to update for the repositry name created in you Dockerhub account under the Build and Push stage. Refer to the Jenkinsfile in the same Project folder.
7. Create new item on Jenkins dashboard and choose pipeline as the type
8. Select the option Github and add the link to github repository
9. Choose SCM and give the link to the github repositry herea nd choose the credentials as "github"
10. Scroll down and select the option Pipeline from SCM option in dropdown to use the Jenkins file
