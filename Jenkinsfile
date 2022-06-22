node {
stage('SCM')
{
checkout scm
}
stage('SonarQube Analysis')
{
def scannerHome = tool 'jenkinsdemo';
withSonarQubeEnv()
{
bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=jenkinsdemo"
}
}

stage("Build Result")
{
echo "Build Successful"
}
}
