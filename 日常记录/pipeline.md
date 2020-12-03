```yaml
podTemplate(containers: [
    containerTemplate(name: 'jnlp', image: '192.168.80.54:8081/library/jenkins/agent_maven:v1.0.5_alpha', ttyEnabled: true)
  ]{
    node(POD_LABEL) {
        stage('Get a Maven project') {
            container('jnlp') {
                stage('Build a Maven project') {
                    sh 'mvn -v'
                }
            }
        }

    }
}
```

```yaml
podTemplate(containers: [
    containerTemplate(name: 'jnlp', image: '192.168.80.54:8081/library/jenkins/agent_maven:v1.0.5_alpha', ttyEnabled: true)
  ],
  	volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock'),
                hostPathVolume(hostPath: '/usr/bin/docker', mountPath: '/usr/bin/docker'),
                hostPathVolume(hostPath: '/usr/local/bin/kubectl', mountPath: '/usr/local/bin/kubectl')]) {

    node(POD_LABEL) {
        stage('Get a Maven project') {
            container('maven') {
                stage('Build a Maven project') {
                    echo "11111111111111111111"
                }
            }
        }

    }
}
```

```yaml
podTemplate(containers: [
    containerTemplate(name: 'jnlp', image: '192.168.80.54:8081/library/jenkins/agent_maven:v1.0.5_alpha', ttyEnabled: true)
  ],
  	volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock'),
                hostPathVolume(hostPath: '/usr/bin/docker', mountPath: '/usr/bin/docker'),
                hostPathVolume(hostPath: '/usr/local/bin/kubectl', mountPath: '/usr/local/bin/kubectl')]) {

    node(POD_LABEL) {
        stage('Get a Maven project') {
            container('jnlp') {
                git  credentialsId: 'yanghaichao_ssh', url: 'http://192.168.71.68:10080/mall/rmemis.git', branch: 'dev-20201020'
                stage('Build a Maven project') {
                    echo "111111111111111"
                    sh "ls -la"
                    sh "echo 192.168.71.65 nexus.rdev.tech >> /etc/hosts"
                    sh "docker version"
                    sh "kubectl version"
                    sh "mvn -f pom.xml clean package"
                }
            }
        }

    }
}
```

```

```