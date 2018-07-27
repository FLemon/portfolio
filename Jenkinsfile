def label = "test-docker-compose"
podTemplate(label: label, containers: [
    containerTemplate(name: 'compose', image: 'docker/compose:1.22.0', command: 'cat', ttyEnabled: true),
],
volumes: [
  hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
  node(label) {
    def myRepo = checkout scm
    def gitCommit = myRepo.GIT_COMMIT
    def gitBranch = myRepo.GIT_BRANCH
    def shortGitCommit = "${gitCommit[0..10]}"
    def previousGitCommit = sh(script: "git rev-parse ${gitCommit}~", returnStdout: true)

    stage('test') {
      container('compose') {
        sh "ls"
        sh "docker-compose --version"
      }
    }
  }
}
