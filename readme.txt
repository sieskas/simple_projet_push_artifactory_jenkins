docker pull jenkins/jenkins

docker run -p 7070:7070 -e JENKINS_OPTS="--httpPort=7070" jenkins/jenkins