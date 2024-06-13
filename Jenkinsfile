#! /bin/env/groovy

node('terraform') {
    def err = null
    try{
        stage('Checkout'){
        checkout scm
        }
        stage('Terraform Init'){
            sh "terraform init"
        }
        stage('Prepare'){
            sh """
                terraform fmt
                terraform validate
                """
        }
        stage('Terraform plan'){
            sh "terraform plan -out=tfplan"
        }
        stage('Terraform apply'){
            sh 'terraform apply "tfplan"'
        }
    }
    catch(caughtError){
        currentBuild.result = 'FAILUTE'
        err = caughtError
    }
    finally{
        if (err){
            throw err
        }
    }
}