pipeline {
  agent any

  environment {
    // Customize this path if needed
    ANSIBLE_VENV = "${WORKSPACE}/venv"
  }

  stages {
    stage('Checkout Code') {
      steps {
        git 'https://github.com/yourusername/nginx-ansible-playbook.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh '''
          python3 -m venv ${ANSIBLE_VENV}
          . ${ANSIBLE_VENV}/bin/activate
          pip install --upgrade pip
          pip install ansible
        '''
      }
    }

    stage('Run Ansible Playbook') {
      steps {
        sh '''
          . ${ANSIBLE_VENV}/bin/activate
          ansible-playbook -i inventory.yml playbook.yml
        '''
      }
    }
  }

  post {
    failure {
      echo '❌ Playbook failed.'
    }
    success {
      echo '✅ Playbook executed successfully.'
    }
  }
}
