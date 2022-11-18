---
title: "The Git Credential Plugin Bug in Jenkins"
author: ["Saikat"]
date: 2022-11-18
draft: false
description: "The Git Credential Plugin Bug in Jenkins"
tags: ["git", "jenkins", "groovy"]
categories: ["TIL"]
---

Recently one of our Jenkins build pipelines started failing after we changed the Git password. 

```groovy
REPO_BRANCH = 'main'
REPO_BASE_PATH = 'mygithub.com/user/my-repo.git'


pipeline {
    agent any

    options {
        disableConcurrentBuilds()
    }
    
    environment {
        GIT_CREDS = credentials("my-git-credential")
        GIT_PASS_ENC = URLEncoder.encode(GIT_CREDS_PSW, "UTF-8")
    }

    stages {
        stage('Build') {
            steps {
                // cleanWs()
                script {
                    sh """
                        set +x
                        git clone https://${GIT_CREDS_USR}:${GIT_PASS_ENC}@${REPO_BASE_PATH} -b ${REPO_BRANCH}
                        set -x 
                    """
                }
            }
        }
    }

}

```

TODO: https://issues.jenkins.io/browse/JENKINS-47514
