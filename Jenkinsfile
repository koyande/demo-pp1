 pipeline {

  agent any
 
  stages {

    stage('TF Plan') {
      steps {
          sh 'terraform init'
          sh """
          export TF_VAR_okta_user_first_name=${params.UserFirstName}
          export TF_VAR_okta_user_last_name=${params.UserLastName}
          export TF_VAR_okta_user_login=${params.UserLogin}
          export TF_VAR_okta_user_email=${params.UserEmail}
          export TF_VAR_okta_group_name=${params.GroupName}
          export TF_VAR_group_description=${params.GroupDescription}
          export TF_VAR_okta_auth_server_name=${params.ServerName}
          export TF_VAR_okta_auth_server_description=${params.ServerDescription}
          export TF_VAR_okta_app_saml_label=${params.SamlLabel}
          export TF_VAR_okta_inline_hook_name=${params.HookName}
          export TF_VAR_okta_idp_social_name=${params.IdpName}

          

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
          export TF_VAR_okta_user_first_name=${params.UserFirstName}
          export TF_VAR_okta_user_last_name=${params.UserLastName}
          export TF_VAR_okta_user_login=${params.UserLogin}
          export TF_VAR_okta_user_email=${params.UserEmail}
          export TF_VAR_okta_group_name=${params.GroupName}
          export TF_VAR_group_description=${params.GroupDescription}
          export TF_VAR_okta_auth_server_name=${params.ServerName}
          export TF_VAR_okta_auth_server_description=${params.ServerDescription}
          export TF_VAR_okta_app_saml_label=${params.SamlLabel}
          export TF_VAR_okta_inline_hook_name=${params.HookName}
          export TF_VAR_okta_idp_social_name=${params.IdpName}
          
          terraform apply -input=false -auto-approve myplan 
          """
        }
      }
  }

}
