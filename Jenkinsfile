withEnv(["KUBERNETES_HOST_NAME=hero-command-test"]) {
  stage "checkout, build, test and publish"
  node {
    git poll: true, url: "https://github.com/robertBrem/hero-frontend.git"
    def npmHome = tool 'NPM'
    env.PATH = "${npmHome}/bin:${env.PATH}"
    sh "npm run clean && npm install"
    sh "npm run test"
    sh "npm run build"
    sh "USER_NAME=robertbrem VERSION=1.0.${currentBuild.number} ./build.js"
    step([$class: 'JUnitResultArchiver', testResults: '**TESTS-*.xml'])
    step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: '**REPORTS-*.xml'])
  }

}
