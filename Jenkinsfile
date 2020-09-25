 pipeline {

  agent any
 
  stages {

    stage('TF Plan') {
      steps {
          sh 'terraform init'
          sh """
          export TF_VAR_okta_user_first_name=${params.userfirstname}
          export TF_VAR_okta_user_last_name=${params.userlastname}
          export TF_VAR_okta_user_login=${params.userlogin}
          export TF_VAR_okta_user_email=${params.useremail}
          export TF_VAR_okta_group_name=${params.groupname}
          export TF_VAR_group_description=${params.groupdescription}
          export TF_VAR_okta_auth_server_name=${params.servername}
          export TF_VAR_okta_auth_server_description=${params.serverdescription}
          export TF_VAR_okta_app_saml_label=${params.samllabel}
          export TF_VAR_okta_inline_hook_name=${params.hookname}
          export TF_VAR_okta_idp_social_name=${params.idpname}

          

          terraform plan -out myplan
          """
        }
      }


    stage('Approval') {
      steps {
        script {
          def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
        }
      }
    }

    stage('TF Apply') {
      steps {
          sh """
          export TF_VAR_okta_user_first_name=${params.userfirstname}
          export TF_VAR_okta_user_last_name=${params.userlastname}
          export TF_VAR_okta_user_login=${params.userlogin}
          export TF_VAR_okta_user_email=${params.useremail}
          export TF_VAR_okta_group_name=${params.groupname}
          export TF_VAR_group_description=${params.groupdescription}
          export TF_VAR_okta_auth_server_name=${params.servername}
          export TF_VAR_okta_auth_server_description=${params.serverdescription}
          export TF_VAR_okta_app_saml_label=${params.samllabel}
          export TF_VAR_okta_inline_hook_name=${params.hookname}
          export TF_VAR_okta_idp_social_name=${params.idpname}
          
          terraform apply -input=false -auto-approve myplan 
          """
        }
      }
  }

}
