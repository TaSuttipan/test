pipeline{
  agent{
      label "linux-slave"
  }
  triggers {
    GenericTrigger(
      genericVariables: [
        [key: 'ref', value: '$.ref']
      ],

      causeString: 'Triggered on $ref',

      token: 'testez',
      //  tokenCredentialId: '',

      //  printContributedVariables: true,
      //  printPostContent: true,

      //  silentResponse: false,

      regexpFilterText: '$ref',
      regexpFilterExpression: 'refs/heads/main'
    )
  }
  environment{
        GIT_URL = "https://github.com/TaSuttipan/pipeline"
        GIT_CREDENTIALS = "TaSuttipan"
        GIT_BRANCH = "main"
        AWS_CREDENTIALS = "The1_non_prod_T1C"
        CONSENT_PUBLIC_BUCKET = "the1-consent-stg"
        MULESOFT_BUCKET = "the1-mulesoft-dcs-stg"
        AEM_API = "https://uatlibrary.the1.co.th"
        // CONSENT_VERSION = "Version-1-1.model.json"
        // EXTERNALCONSENT_VERSION = "Version-8-0.model.json"
        // PRIVACY_POLICY_VERSION = "Version-1-1.model.json"
        // TERMS_CONDITIONS_VERSION = "Version-1-1.model.json"
    }
  stages{
      stage("Download Json file"){
          steps{
            script{
              // en
              sh '''
                wget -P en/Consent/ "${AEM_API}/content/the1/api/th/en/Consent/${CONSENT_VERSION}"
                wget -P en/ExternalConsent/ "${AEM_API}/content/the1/api/th/en/Consent/${EXTERNALCONSENT_VERSION}"
                wget -P en/privacy-policy/ "${AEM_API}/content/the1/api/th/en/privacy-policy/${PRIVACY_POLICY_VERSION}"
                wget -P en/terms-conditions/ "${AEM_API}/content/the1/api/th/en/terms-conditions/${TERMS_CONDITIONS_VERSION}"
              '''
              // th
              sh '''
                wget -P th/Consent/ "${AEM_API}/content/the1/api/th/th/Consent/${CONSENT_VERSION}"
                wget -P th/ExternalConsent/ "${AEM_API}/content/the1/api/th/th/Consent/${EXTERNALCONSENT_VERSION}"
                wget -P th/privacy-policy/ "${AEM_API}/content/the1/api/th/th/privacy-policy/${PRIVACY_POLICY_VERSION}"
                wget -P th/terms-conditions/ "${AEM_API}/content/the1/api/th/th/terms-conditions/${TERMS_CONDITIONS_VERSION}"
              '''
            }
          }
      }
      stage("List"){
          steps{
              sh "ls -l"
          }
      }
    stage("Checkout"){
          steps{
            script{
              // GIT_BRANCH = ref.split('/')[2]
              checkout([
                $class: 'GitSCM', 
                branches: [[name: "*/${GIT_BRANCH}"]], 
                doGenerateSubmoduleConfigurations: false, 
                extensions: [], 
                submoduleCfg: [], 
                userRemoteConfigs: [[
                  credentialsId: "${GIT_CREDENTIALS}", 
                  url: "${GIT_URL}"
                  ]]
              ])
            }
          }
      }
  }
  post{
    always{
      deleteDir()
    }
  }
}
