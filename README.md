1)Run 'docker-compose up -d" from compose directory
2)Login to Jenkins via http://localhost:8082/ (find admin password in Jenkins logs)
3)Install CloudBees Docker Build and Publish Jenkins plugin
4)Create new pipline for SCM (this repo), set up build brunch (main), set up path to Jenkinsfile (root)
5)Run the build