node {
    def registryProjet = 'rania144/'
    def IMAGE = "${registryProjet}mon-nginx-personnalise:version-${env.BUILD_ID}"
    def img

    stage('Clone') {
        checkout scm
    }

    stage('Build') {
        img = docker.build(IMAGE, '.')
    }

    stage('Run') {
        img.withRun("-p 8000:80 --name run-${env.BUILD_ID}") { c ->
            echo "Container is running"
        }
    }

    stage('Push') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker_id') {
            img.push('latest')
            img.push()
        }
    }
}


