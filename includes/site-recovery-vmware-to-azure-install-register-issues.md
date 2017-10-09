
### <a name="installation-failures"></a>Échecs d’installation
| **Exemple de message d’erreur** | **Action recommandée** |
|--------------------------|------------------------|
|ERREUR Échec tooload comptes. Erreur : System.IO.IOException : tooread impossible des données à partir de hello connexion de transport lors de l’installation et l’inscription de serveur CS hello.| Vérifiez que TLS 1.0 est activé sur l’ordinateur de hello. |

### <a name="registration-failures"></a>Échecs d’enregistrement
Les échecs d’enregistrement peuvent être débogués en examinant les journaux hello Bonjour **%ProgramData%\ASRLogs** dossier.

| **Exemple de message d’erreur** | **Action recommandée** |
|--------------------------|------------------------|
|**09:20:06** :InnerException.Type : SrsRestApiClientLib.AcsException,InnerException.<br>Message : ACS50008 : Jeton SAML non valide.<br>ID de suivi : 1921ea5b-4723-4be7-8087-a75d3f9e1072<br>ID de corrélation : 62fea7e6-2197-4be4-a2c0-71ceb7aa2d97><br>Timestamp : **2016-12-12 14:50:08Z<br>** | Assurez-vous que le temps hello sur l’horloge de votre système n’est pas plus de 15 minutes d’arrêt heure locale de hello. Exécutez à nouveau l’inscription de hello installer toocomplete hello.|
|**De 09:35:27** : DRRegistrationException lors de la tentative de tooget tous les coffre de récupération d’urgence pour le certificat sélectionné de hello : : a levé une Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException, Exception.Message : ACS50008 : Jeton SAML n’est pas valide.<br>ID de suivi : e5ad1af1-2d39-4970-8eef-096e325c9950<br>ID de corrélation : abe9deb8-3e64-464d-8375-36db9816427a<br>Timestamp : **2016-05-19 01:35:39Z**<br> | Assurez-vous que le temps hello sur l’horloge de votre système n’est pas plus de 15 minutes d’arrêt heure locale de hello. Exécutez à nouveau l’inscription de hello installer toocomplete hello.|
|06:28:45 : certificat de toocreate ayant échoué<br>06:28:45 : Impossible de poursuivre le programme d’installation. Un certificat requis tooSite tooauthenticate que récupération ne peut pas être créée. Réexécuter le programme d’installation | Assurez-vous d’exécuter le programme d’installation en tant qu’administrateur local. |
