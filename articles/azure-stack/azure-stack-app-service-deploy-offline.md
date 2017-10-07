---
title: "Déployer App Service dans un environnement hors connexion : Azure Stack | Microsoft Docs"
description: "Obtenir des instructions détaillées sur la façon dont les toodeploy du Service d’applications dans un environnement déconnecté de la pile de Azure sécurisés par AD FS."
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: f7992c310532427b5ffb88555faab2679023c876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-app-service-resource-provider-tooa-disconnected-azure-stack-environment-secured-by-ad-fs"></a>Ajouter qu'un tooa de fournisseur de ressources du Service d’applications déconnecté environnement Azure pile sécurisé par AD FS

Vous devez ajouter une [fournisseur de ressources du Service d’applications Azure](azure-stack-app-service-overview.md) tooyour déploiement de la pile de Azure :

* Si vous exécutez Azure Stack dans un environnement isolé sécurisé par AD FS. 
* Si vous voulez que toogive votre locataires hello fonctionnalité toocreate, mobile et les applications API--applications web et les fonctions Azure--avec leur abonnement Azure pile. 

toodo par conséquent, les étapes hello dans cet article.

## <a name="download-hello-required-components"></a>Télécharger les composants requis de hello

1. Télécharger hello [du Service d’applications sur le programme d’installation de la version d’évaluation Azure pile](http://aka.ms/appsvconmasrc1installer).

2. Télécharger hello [du Service d’applications sur des scripts d’assistance de déploiement Azure pile](http://aka.ms/appsvconmasrc1helper).

3. Extrayez les fichiers de hello du fichier zip de hello d’assistance des scripts. Hello structure de dossiers et les fichiers suivants apparaissent :

   - Create-AppServiceCerts.ps1
   - Create-IdentityApp.ps1
   - Modules
      - AzureStack.Identity.psm1
      - GraphAPI.psm1

## <a name="create-an-offline-installation-package"></a>Créer un package d'installation hors connexion

toodeploy du Service d’applications dans un environnement isolé, vous devez créer un package d’installation hors connexion à partir d’un ordinateur qui se connecte toohello Internet.

1. Exécutez hello du Service d’applications sur le programme d’installation de Azure pile preview (AppService.exe) à partir d’un ordinateur qui est connecté toohello Internet.

2. Cliquez sur hello **avancé** onglet, puis cliquez sur **créer un package d’installation hors connexion**.

    ![Créer un package d’installation hors connexion App Service sur Azure Stack][1]

3. Hello d’installation du Service de l’application crée un package d’installation hors connexion, affiche le chemin d’accès hello et donne un dossier de hello tooopen option.

   ![Package d’installation hors connexion App Service sur Azure Stack][2]

4. Copiez hello du Service d’applications sur le programme d’installation de Azure pile preview (AppService.exe) et l’ordinateur hôte de la pile de Azure hello installation hors connexion package toohello.

## <a name="create-certificates-required-by-app-service-on-azure-stack"></a>Créer les certificats requis par App Service sur Azure Stack

Ce premier script fonctionne avec hello Azure pile toocreate trois certificats d’autorité dont a besoin le Service d’applications. Exécuter le script de hello sur l’ordinateur hôte de pile de Azure hello et assurez-vous que vous exécutez PowerShell en tant qu’azurestack\administrator.

1. Dans une session PowerShell en cours d’exécution en tant qu’azurestack\administrator, exécutez hello **AppServiceCerts.ps1-créer** script à partir de l’emplacement de hello où vous avez extrait les scripts d’assistance hello.  script de Hello crée trois certificats Bonjour même dossier que hello créer le script de certificats qui sont requis par le Service d’applications.

2. Entrez un fichier .pfx de mot de passe toosecure hello et prenez note de celui-ci. Vous devez tooenter dans hello du Service d’applications sur le programme d’installation de la pile de Azure.

### <a name="create-appservicecertsps1-parameters"></a>Paramètres Create-AppServiceCerts.ps1

| Paramètre | Obligatoire ou facultatif | Valeur par défaut | Description |
| --- | --- | --- | --- |
| pfxPassword | Requis | Null | Mot de passe utilisé tooprotect hello clé privée. |
| DomainName | Requis | local.azurestack.external | Suffixe de la région et du domaine Azure Stack |
| CertificateAuthority | Requis | AzS-CA01.azurestack.local | Point de terminaison de l’autorité de certification |

## <a name="complete-hello-offline-installation-of-app-service-on-azure-stack"></a>Terminer l’installation en mode hors connexion de hello du Service d’application sur la pile de Azure

> [!NOTE]
> Vous *doit* utiliser le programme d’installation de hello tooexecute compte avec élévation de privilèges (administrateur local ou de domaine). Si vous êtes connecté en tant que azurestack\azurestackuser, vous êtes invité à entrer des informations d’identification avec élévation de privilèges.

1. Exécutez appservice.exe en tant que azurestack\administrator.

2. Cliquez sur hello **avancé** onglet, puis cliquez sur **terminer l’installation en mode hors connexion**.

    ![Terminer l’installation hors connexion d’App Service sur Azure Stack][3]

3. Spécifier l’emplacement de hello hello hors connexion du package d’installation que vous avez créé, puis cliquez sur **suivant**.

    ![Emplacement du package d’installation hors connexion App Service sur Azure Stack][4]

4. Passez en revue et acceptez hello préliminaire le contrat de licence, puis cliquez sur **suivant**.

5. Passez en revue et accepter les termes du contrat de licence de tiers hello, puis cliquez sur **suivant**.

6. Hello de révision du Service d’applications cloud des informations de configuration, puis cliquez sur **suivant**.

    ![Configuration cloud App Service sur Azure Stack][5]

    > [!NOTE]
    > Hello du Service d’applications sur le programme d’installation de la pile de Azure fournit des valeurs par défaut de hello pour une installation de la pile de Azure un nœud. Si vous avez personnalisé les options lors du déploiement de la pile de Azure (par exemple, un suffixe de domaine hello), vous devez en conséquence les valeurs hello tooedit dans cette fenêtre. Par exemple, si vous utilisez mycloud.com de suffixe de domaine hello, votre point de terminaison Azure Resource Manager admin doit toochange tooadminmanagement. [Région]. mycloud.com.

7. Cliquez sur hello **Connect** toohello suivant du bouton **Azure pile abonnements** boîte. Entrez votre compte d’administrateur, par exemple, azurestackadmin@azurestack.local. Entrez votre mot de passe, puis cliquez sur **Se connecter**.

8. Sélectionnez votre abonnement Bonjour **Azure pile abonnements** boîte.

9. Bonjour **les emplacements de pile Azure** zone, emplacement sélectionnez hello correspondant région toohello que vous déployez. Par exemple, sélectionnez **local**. Cliquez sur **Suivant**.

    ![Sélection d’abonnement App Service sur Azure Stack][6]

10. Entrez hello **nom de groupe de ressources** pour votre déploiement du Service d’applications. Par défaut, il est défini trop**APPSERVICE LOCAL**.

11. Entrez hello **nom de compte de stockage** toocreate de Service de l’application souhaitée dans le cadre de l’installation de hello. Par défaut, il est défini trop**appsvclocalstor**.

12. Entrez les détails de SQL Server hello pour instance hello toohost utilisé de hello des bases de données fournisseur de ressources du Service d’applications. Cliquez sur **suivant**, et le programme d’installation hello valide les propriétés de connexion SQL hello.

13. Cliquez sur hello **Parcourir** toohello suivant du bouton **fichier de certificat SSL du Service d’applications par défaut** boîte. Accédez toohello **_.appservice.local.AzureStack.external** certificat [créé précédemment](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps). Si vous avez spécifié un autre emplacement et le suffixe de domaine lorsque vous avez créé le certificat de hello, sélectionnez le certificat correspondant de hello.

14. Mot de passe hello certificat que vous définissez lorsque vous avez créé le certificat de hello.

15. Cliquez sur hello **Parcourir** toohello suivant du bouton **fichier de certificat SSL de ressource fournisseur** boîte. Accédez toohello **api.appservice.local.AzureStack.external** certificat [créé précédemment](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps). Si vous avez spécifié un autre emplacement et le suffixe de domaine lorsque vous avez créé le certificat de hello, sélectionnez le certificat correspondant de hello.

16. Mot de passe hello certificat que vous définissez lorsque vous avez créé le certificat de hello.

17. Cliquez sur hello **Parcourir** toohello suivant du bouton **fichier de certificat racine de ressource fournisseur** boîte. Accédez toohello **AzureStackCertificationAuthority** certificat [créé précédemment](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).

18. Cliquez sur **Suivant**. programme d’installation Hello vérifie le mot de passe de certificat hello fourni.

    ![Détails du certificat App Service sur Azure Stack][8]

19. Passez en revue hello configuration du rôle du Service d’applications. valeurs par défaut de Hello sont renseignées avec hello minimale recommandée instance références (SKU) pour chaque rôle. Un résumé des besoins en mémoire et de base est fourni toohelp planifier votre déploiement. Une fois vos sélections effectuées, cliquez sur **Suivant**.

    - **Contrôleur** : par défaut, une instance A1 Standard est sélectionnée. Il s’agit de minimum hello recommandé. rôle de contrôleur Hello est responsable de la gestion et maintenance d’intégrité hello hello cloud Service d’application.
    - **Gestion** : par défaut, une instance A2 Standard est sélectionnée. tooprovide basculement, nous vous recommandons de deux instances. rôle de gestion Hello est chargé de hello App Service Azure Resource Manager et des points de terminaison API, des extensions portails (admin, client, du portail de fonctions) et service de données hello.
    - **Serveur de publication** : par défaut, une instance A1 Standard est sélectionnée. Il s’agit de minimum hello recommandé. rôle de serveur de publication Hello est responsable de la publication du contenu via FTP et web de déploiement.
    - **Frontal** : par défaut, une instance A1 Standard est sélectionnée. Il s’agit de minimum hello recommandé. rôle de serveur frontal Hello est responsable des applications de Service de routage demandes tooApp.
    - **Traitement partagé**: par défaut, une seule instance A1 Standard est sélectionnée, mais vous souhaiterez peut-être tooadd plus. En tant qu’administrateur, vous pouvez définir votre offre et choisir n’importe quel niveau de référence. niveaux de Hello doivent avoir un minimum d’un cœur. rôle de traitement partagé Hello est responsable de l’hébergement web, mobile, ou les applications API et les applications de fonctions d’Azure.

    ![Configuration du rôle App Service sur Azure Stack][9]

    > [!NOTE]
    > Dans les versions d’évaluation technique hello, hello programme d’installation de fournisseur de ressources du Service d’applications déploie également un toooperate d’instance A1 Standard comme un Bonjour toosupport du serveur de fichiers simple Azure Resource Manager. Cette configuration est conservée pour un point de contact à un seul nœud. Pour les charges de production, à hello de disponibilité générale du Service d’applications installer permet hello un haute disponibilité du serveur de fichiers.

20. Choisissez votre déploiement **Windows Server 2016** image de machine virtuelle à partir de celles qui sont disponibles dans le fournisseur de ressources de calcul hello pour hello cloud Service d’application. Cliquez sur **Suivant**. 

    ![Sélection d’image de machine virtuelle App Service sur Azure Stack][10]

21. Entrez un nom d’utilisateur et un mot de passe pour les rôles de travail hello configurés Bonjour cloud Service d’application. Entrez un nom d’utilisateur et un mot de passe pour tous les autres rôles App Service. Cliquez sur **Suivant**.

    ![Saisie des informations d’identification App Service sur Azure Stack][11]

22. Sur l’écran de résumé hello, vérifiez les sélections de hello que vous avez apportées. modifications de toomake, passer en revue les écrans hello et modifier vos sélections. Si hello est l’aspect souhaité, cochez hello. déploiement de hello toostart, cliquez sur **suivant**. 

    ![Synthèse des sélections App Service sur Azure Stack][12]

23. Suivre la progression de l’installation hello. Service d’applications sur Azure pile prend environ 45 toodeploy de minutes too60 selon les sélections par défaut de hello.

    ![Progression de l’installation App Service sur Azure Stack][13]

24. Une fois le programme d’installation Bonjour s’est correctement déroulée, cliquez sur **Exit**.

## <a name="configure-an-ad-fs-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a>Configurer un principal du service AD FS pour l’intégration de jeu mise à l’échelle de machine virtuelle sur les niveaux de workers et l’authentification unique pour les outils de portail et avancées développeur Azure fonctions hello

>[!NOTE]
> Ces étapes s’appliquent tooAD que FS sécurisés environnements Azure pile uniquement.

Les administrateurs doivent tooconfigure SSO pour :

* Configurer un principal du service pour l’intégration d’un groupe de machines virtuelles identiques sur les niveaux Worker.
* Activer hello avancée des outils de développement au sein du Service d’applications (Kudu).
* Activer l’utilisation de hello d’utilisation du portail Azure fonctions hello. 

Procédez comme suit :

1. Ouvrez une instance PowerShell en tant que azurestack\azurestackadmin.

2. Atteindre l’emplacement toohello de scripts hello téléchargé et extrait Bonjour [préalablement](#Download-Required-Components).

3. [Installez](azure-stack-powershell-install.md) et [configurez un environnement PowerShell Azure Stack](azure-stack-powershell-configure-admin.md).

4. Bonjour même session PowerShell, exécutez hello **CreateIdentityApp.ps1** script. Lorsque vous êtes invité à entrer votre ID de locataire Azure Active Directory (Azure AD), entrez **ADFS**.

5. Bonjour **informations d’identification** fenêtre, entrez votre compte administrateur de service AD FS et le mot de passe. Cliquez sur **OK**.

6. Entrez hello certificat fichier chemin d’accès et le certificat de mot de passe hello [certificat créé précédemment](# Create certificates toobe used by App Service on Azure Stack). certificat Hello par défaut créé pour cette étape est sso.appservice.local.azurestack.external.pfx.

7. script de Hello crée une nouvelle application dans le locataire hello Azure AD et génère un script PowerShell.

8. Copier fichier de certificat application hello identité et hello généré script toohello **CN0-VM** à l’aide d’une session Bureau à distance.

9. Trop de retour**CN0-VM**.

10. Ouvrez une fenêtre PowerShell d’administrateur et parcourir le répertoire toohello où le fichier de script hello et de certificat ont été copiés à l’étape 7.

11. Exécutez le fichier de script hello. Ce fichier de script entre des propriétés de hello Bonjour du Service d’applications sur la configuration de la pile d’Azure et initie une opération de réparation sur les rôles de serveur frontal et la gestion.

| Paramètre | Obligatoire ou facultatif | Valeur par défaut | Description |
| --- | --- | --- | --- |
| DirectoryTenantName | Obligatoire | Null | Utilisez **ADFS** pour l’environnement de hello AD FS |
| TenantAzure Resource ManagerEndpoint | Obligatoire | management.local.azurestack.external | locataire Hello point de terminaison Azure Resource Manager |
| AzureStackCredential | Obligatoire | Null | compte d’administrateur service Hello AD FS |
| CertificateFilePath | Obligatoire | Null | Fichier chemin d’accès toohello identité application certificat généré précédemment |
| CertificatePassword | Obligatoire | Null | Mot de passe utilisé tooprotect hello clé privée. |
| DomainName | Requis | local.azurestack.external | Suffixe de la région et du domaine Azure Stack |
| AdfsMachineName | Facultatif | Nom de l’ordinateur AD FS, par exemple, AzS-ADFS01.azurestack.local |


## <a name="validate-hello-app-service-on-azure-stack-installation"></a>Valider hello du Service d’applications sur l’installation de la pile de Azure

1. Dans le portail d’administration hello pile d’Azure, accédez toohello groupe de ressources créé par le programme d’installation hello. Par défaut, ce groupe est **APPSERVICE-LOCAL**.

2. Recherchez hello **CN0-VM**. tooconnect toohello machine virtuelle, cliquez sur **Connect** sur hello **Machine virtuelle** panneau.

3. Sur le bureau de hello de cet ordinateur virtuel, double-cliquez sur **Console de gestion du Cloud Web**.

4. Accédez trop**serveurs gérés**.

5. Lorsque tous les hello machines affichage **prêt** pour un ou plusieurs threads de travail, passez toostep 6.

6. Fermer l’ordinateur de bureau à distance hello et machine toohello retour où vous avez exécuté hello d’installation du Service d’application.

    > [!NOTE]
    > Vous n’avez pas besoin toowait pour un ou plusieurs toodisplay de travailleurs **prêt** installation de hello toocomplete du Service d’application sur la pile de Azure. Toutefois, vous devez au minimum d’un processus de travail est prêt toodeploy un site web, mobile, ou application API ou des fonctions de Azure.
    
    ![État des serveurs gérés App Service sur Azure Stack][14]

## <a name="test-drive-app-service-on-azure-stack"></a>Tester App Service sur Azure Stack

Une fois que vous déployez et inscrivez hello fournisseur de ressources du Service d’applications, tester toomake assurer que les locataires peuvent déployer les applications API web et mobile.

> [!NOTE]
> Vous devez toocreate une offre qui possède l’espace de noms Microsoft.Web hello dans le plan de hello. Vous devez ensuite toohave un abonnement locataire qui s’abonne toothis offre. Pour plus d’informations, consultez [Créer une offre](azure-stack-create-offer.md) et [Créer un plan](azure-stack-create-plan.md).
>

Vous *doit* ont un locataire abonnement toocreate les applications qui utilisent le Service de l’application sur la pile de Azure. Hello seules fonctionnalités qu’un administrateur de service peut effectuer au sein du portail d’administration hello sont toohello connexes administration du fournisseur de ressources du Service de l’application. Ces fonctionnalités incluent l’ajout de capacité, la configuration de sources de déploiement, l’ajout de niveaux Worker et de références.

À compter de la version d’évaluation technique troisième hello, toocreate, mobile, applications web et API, vous devez utiliser le portail de locataires hello et avoir un abonnement locataire.  

1. Dans le portail de locataires Azure pile hello, cliquez sur **nouveau** > **Web + Mobile** > **application Web**.

2. Sur hello **Web App** panneau, tapez un nom dans hello **application Web** boîte.

3. Sous **Groupe de ressources**, cliquez sur **Nouveau**. Puis tapez un nom dans hello **groupe de ressources** boîte.

4. Cliquez sur **Plan App Service/Emplacement** > **Créer**.

5. Sur hello **plan App Service** panneau, tapez un nom dans hello **plan App Service** boîte.

6. Cliquez sur **Niveau tarifaire** > **Libre-Partagé** ou **Partagé-Partagé** > **Sélectionnez** > **OK** > **Créer**.

7. Dans moins d’une minute, une vignette pour l’application web hello apparaît dans le tableau de bord hello. Cliquez sur la vignette de hello.

8. Sur hello **Web App** panneau, cliquez sur **Parcourir** site Web par défaut de hello tooview pour cette application.

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a>Déployer un site web WordPress, DNN ou Django (facultatif)

1. Dans le portail de locataires Azure pile hello, cliquez sur  **+** . Accédez toohello Azure Marketplace, déployez un site Web Django et attendre l’achèvement réussi. plateforme de Hello Django web utilise une base de données basée sur le système de fichier. Elle ne nécessite aucun fournisseur de ressources supplémentaire comme SQL ou MySQL.

2. Si vous avez également déployé d’un fournisseur de ressources MySQL, vous pouvez déployer un site Web de WordPress à partir de hello Marketplace. Lorsque vous êtes invité à entrer les paramètres de base de données, entrez le nom d’utilisateur hello en tant que  *User1@Server1* , avec le nom d’utilisateur hello et le nom du serveur de votre choix.

3. Si vous avez également déployé d’un fournisseur de ressources SQL Server, vous pouvez déployer un site Web de profonds DNN de hello Marketplace. Lorsque vous êtes invité à entrer les paramètres de base de données, choisissez une base de données dans l’ordinateur hello exécutant SQL Server qui est le fournisseur de ressources tooyour connecté.

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez également tester d’autres [services PaaS](azure-stack-tools-paas-services.md).

- [Fournisseur de ressources SQL Server](azure-stack-sql-resource-provider-deploy.md)
- [Fournisseur de ressources MySQL](azure-stack-mysql-resource-provider-deploy.md)

<!--Image references-->
[1]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step1.png
[2]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step2.png
[3]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step3.png
[4]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step4.png
[5]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-cloud-configuration.png
[6]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-subscription-location-populated.png
[7]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-resource-group-SQL.png
[8]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-certificates.png
[9]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-role-configuration.png
[10]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-vm-image-selection.png
[11]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-role-credentials.png
[12]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-selection-summary.png
[13]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-installation-progress.png
[14]: ./media/azure-stack-app-service-deploy-offline/managed-servers.png


<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525
