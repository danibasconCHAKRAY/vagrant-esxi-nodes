// comment
pipeline {
 agent any
 stages {
        stage('Checkout-git'){
               steps{
		git poll: true, url: 'git@github.com:danibasconCHAKRAY/vagrant-esxi-nodes.git'
               }
        }
        stage('CreateVirtualEnv') {
            steps {
		sh '''
			bash -c "virtualenv entorno_virtual && source entorno_virtual/bin/activate"
		'''
            }
        }
        stage('InstallRequirements') {
            steps {
            	sh '''
            		bash -c "source ${WORKSPACE}/entorno_virtual/bin/activate && pwd && ${WORKSPACE}/entorno_virtual/bin/python ${WORKSPACE}/entorno_virtual/bin/pip install -r requirements.txt"
                '''
            }
        }   
        stage('RunApp') {
            steps {
            	sh '''
            		bash -c "source entorno_virtual/bin/activate ; ${WORKSPACE}/entorno_virtual/bin/python ansible.py > host"
                '''
            }
        } 
  }
}

