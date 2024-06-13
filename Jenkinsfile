#! /bin/env/groovy

node('terraform') {
    def err = null
    try{
        stage('Checkout'){
        checkout scm
        }
        stage('Prepare'){
            sh """
                terraform fmt
                terraform validate
                """
        }
        stage('Terraform Init'){
            sh "terraform init"
        }
        stage('Terraform plan'){
            sh "terraform plan -out=tfplan"
        }
        stage('Terraform apply'){
            echo "Terraform apply tfplan"
        }
    }
    catch(caughtError){
        currentBuild.result = 'FAILUTE'
        err = caughtError
    }
    finally{
        if err{
            throw err
        }
    }
}