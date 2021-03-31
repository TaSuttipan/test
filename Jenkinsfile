pipeline{
  agent{
      label "linux-slave"
  }
  environment{
        GIT_URL = "https://github.com/The1Central/mulesoft-consent"
        GIT_CREDENTIALS = "the1card_github_token"
        GIT_BRANCH = "develop"
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
  }
  post{
    always{
      deleteDir()
    }
  }
}
