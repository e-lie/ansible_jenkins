
pipeline {
  agent {
    kubernetes {
      // this label will be the prefix of the generated pod's name
      label 'jenkins-agent-flask-app'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    component: ci
spec:
  containers:
    - name: ansible
      image: williamyeh/ansible:ubuntu18.04
      command:
        - cat
      tty: true
"""
    }
  }

  stages {
    stage('Ansible test') {
      steps {
        container('ansible') {
          ansiColor('xterm') {
            ansiblePlaybook(
                playbook: 'ping.yml',
                inventory: 'ansible.cfg',
                credentialsId: 'id_ssh_lxd',
                colorized: true)
          }
        }
      }
    }
  }

}
