withEnv(["KUBERNETES_HOST_NAME=hero-command-test"]) {
  stage "checkout, build, test and publish"
  node {
    git poll: true, url: "https://github.com/robertBrem/hero-frontend.git"
    def npmHome = tool 'NPM'
    sh "${npmHome}/bin/npm run build"
    sh "USER_NAME=robertbrem VERSION=1.0.${currentBuild.number} ./build.js"
  }

}
