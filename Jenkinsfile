@Library( "digibridge-library@master" ) _

GIT_REPO = "https://github.com/PIPIRAN/simple-java-maven-app.git"
TARGET_JAR = "herschel-backend.jar"
TARGET_DIR = "D:\\workspace\\simple-java-maven-app"

node {
  cleanWs()
  deleteDir()

  stage("Checkout") {
    def branches = git.lsRemote(repo: GIT_REPO)
    def branch

    timeout(time: 3, unit: 'MINUTES') {
      def userChoices = input(
          message: 'Please select !',
          parameters: [choice(choices: branches, name: "branchToBuild", description: "Which branch to build?")]
      )
      branch = userChoices
    }

    git.checkoutRepo(repo: GIT_REPO, branch: branch, targetDir: "project")
  }

  stage("Build") {
    sh "ls -lat project"
    dockerRun.maven(command: "mvn clean install -DskipTests")
  }

}
