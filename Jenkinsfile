pipeline{
    agent{
        label "worker-01-jenkins"
    }
    stages{
        stage("Pull the Infra Services Manifest files From SCM"){
            steps{
                echo "========Pull the Infra Services Manifest files From SCM========"
                git branch: 'master',
                    url: 'https://github.com/Narsi-Myteaching/weshopify-infra-services-deployment.git'
                echo "========Pull the Infra Services Manifest files From SCM completed========"
            }
        }
        stage("copy the files to ansible server"){
            steps{
                echo "Connecting to Ansible Server"
                sshagent(['ANSIBLE_SERVER']){
                    sh 'scp * ansible-admin@172.31.7.122:/opt/weshopify-infra-svc-deploy'
                    sh '''
                        ssh -tt ansible-admin@172.31.7.122 << EOF
                            ansible-playbook /opt/weshopify-infra-svc-deploy/weshopify-infra-svc-playbook.yml
                            exit
                        EOF
                    '''
                }
            }
        }
    }
}
