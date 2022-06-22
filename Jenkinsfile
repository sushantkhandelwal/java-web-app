node {
stage('SCM') {
checkout scm
}
stage('SonarQube Analysis')
{
def scannerHome = tool 'sonarqubedemo';
withSonarQubeEnv()
{
bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=sonarqubedemo"
}
}
stage("UPLOAD TO JFROG")
{
def server = Artifactory.server "java-web-app"
def buildInfo = Artifactory.newBuildInfo()
buildInfo.env.capture = true
buildInfo.env.collect()
def uploadSpec = """{
"files": [
{
"pattern": "**/target/*.jar",
"target": "libs-snapshot-local"
}, {
"pattern": "**/target/*.pom",
"target": "libs-snapshot-local"
}, {
"pattern": "**/target/*.war",
"target": "libs-snapshot-local"
}
]
}"""
// Upload to Artifactory.
server.upload spec: uploadSpec, buildInfo: buildInfo
buildInfo.retention maxBuilds: 10, maxDays: 7, deleteBuildArtifacts: true
// Publish build info.
server.publishBuildInfo buildInfo
}
}
