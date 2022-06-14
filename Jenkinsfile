node {
stage('SCM')
{
checkout scm
}
stage('SonarQube Analysis')
{
def scannerHome = tool 'sonarqube';
withSonarQubeEnv()
{
bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=TESTAPP2"
}
}
stage("Build Result")
{
echo "Build Successful"
}
}
