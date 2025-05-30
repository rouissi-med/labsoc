pipeline { // Defines a pipeline
  
  agent any // Specifies that the pipeline can be run on any available agent

 

  stages { // Defines the different stages of the pipeline
    
    stage('Checkout SCM') { //  'Checkout Source or scm' stage récupère le code source depuis un dépôt configurer dans jenkinz
      steps { // Specifies the steps to be executed within this stage
        git 'https://github.com/rouissi-med/labsoc.git' // Retrieves the source code from the specified GitHub repository
      }
    }

    stage ('Secret scanner') { 
      steps { 
        sh 'gitleaks detect --source  . -f json --report-path gitleaks.json || true'  
      }   
    }

    
   stage('Deploy') { //   Exécuter le playbook Ansible
      steps {
        ansiblePlaybook(
          playbook: 'deployelk.yml', // Chemin vers votre playbook
          inventory: 'inventory.yml',    // Chemin vers votre fichier d'inventaire
          //credentialsId: 'ansible-ssh-credentials', // ID des credentials SSH dans Jenkins
          //extras: '-e "image_name=votre-image:tag"' // Paramètres supplémentaires pour Ansible
        )
      }
    }


    
 }
}
 
