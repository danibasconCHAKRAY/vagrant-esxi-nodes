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
        stage('Copyng config') {
            steps {
            	sh '''
            		cp ${WORKSPACE}/../k8s/hosts ${WORKSPACE}/hosts_vagrant
                '''
            }
        }
        stage('Configuring  host') {
            steps {
                sh '''
			sed -i "s|#node1| $(head -n 1 ${WORKSPACE}/hosts_vagrant | tail -n 1) |" ${WORKSPACE}/hosts.ini
                        sed -i "s|#node2| $(head -n 2 ${WORKSPACE}/hosts_vagrant | tail -n 1) |" ${WORKSPACE}/hosts.ini	
			sed -i "s|#node3| $(head -n 3 ${WORKSPACE}/hosts_vagrant | tail -n 1) |" ${WORKSPACE}/hosts.ini
			sed -i "s|#node4| $(head -n 4 ${WORKSPACE}/hosts_vagrant | tail -n 1) |" ${WORKSPACE}/hosts.ini
			sed -i "s|#node5| $(head -n 5 ${WORKSPACE}/hosts_vagrant | tail -n 1) |" ${WORKSPACE}/hosts.ini
		'''	
            }
        }
  }
}

