node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    if (env.BRANCH_NAME == 'dev') {
        stage('Build image') {
            app = docker.build("emsnikac/kiii-jenkins")
        }

        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'Docker_hub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        }
    } else {
        echo "Not on 'dev' branch. Skipping Docker build & push."
    }
}
