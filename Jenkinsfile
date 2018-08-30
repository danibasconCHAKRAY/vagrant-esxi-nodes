// comment
pipeline {
 agent any
 stages {
        stage('Checkout-git vagrant-esxi-nodes'){
               steps{
		git poll: true, url: 'git@github.com:danibasconCHAKRAY/vagrant-esxi-nodes.git'
               }
        }
        stage('Checkout-git kubespray'){
               steps{
		sh '''
			rm -rf kubespray
			git clone git@github.com:danibasconCHAKRAY/kubespray.git
               '''
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
            		bash -c "source ${WORKSPACE}/entorno_virtual/bin/activate && ${WORKSPACE}/entorno_virtual/bin/python ${WORKSPACE}/entorno_virtual/bin/pip install -r  ${WORKSPACE}/kubespray/requirements.txt"
                '''
            }
        }   
        stage('RunApp') {
            steps {
            	sh '''
            		cp ${WORKSPACE}/../k8s/host ${WORKSPACE}
                '''
            }
        } 
  }
}

