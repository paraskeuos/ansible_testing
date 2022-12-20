pipeline {
    agent any
    
    parameters {
        stashedFile 'inventory'
    }
    
    environment {
        NODE_KEY = credentials('BUILDER_NODE_KEY')
        NODE_USR_PASS_CREDS = credentials('BUILDER_NODE_USER_PASS')
    }
    
    stages {
        stage('Clone repo') {
            steps {
                git 'https://github.com/paraskeuos/ansible_testing.git'
            }
        }
        
        stage('Run Ansible script') {
            steps {
                sh "ansible-playbook -i inventory --private-key ${NODE_KEY} --extra-vars 'ansible_sudo_pass=${NODE_USR_PASS_CREDS_PSW}' run.yml"
            }
        }
        
        stage('Clean up') {
            steps {
                cleanWs()
            }
        }
    }
}