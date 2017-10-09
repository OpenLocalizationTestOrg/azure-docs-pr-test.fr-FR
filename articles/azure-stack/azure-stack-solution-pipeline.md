---
title: aaaDeploy votre application tooAzure et la pile de Azure | Documents Microsoft
description: "Découvrez comment toodeploy applications tooAzure et pile Azure avec un élément de configuration/CD hybride de pipeline."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: a468d7da6f34d04809ee98463a8c4146da581015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-apps-tooazure-and-azure-stack"></a>Déployer des applications tooAzure et la pile de Azure
Un hybride [intégration continue](https://www.visualstudio.com/learn/what-is-continuous-integration/)/[livraison continue](https://www.visualstudio.com/learn/what-is-continuous-delivery/)pipeline de (l’élément de configuration/CD) vous permet de toobuild, tester et déployer vos clouds de toomultiple d’application.  Dans ce didacticiel, vous générez un toolearn d’environnement exemple comment un pipeline de l’élément de configuration/CD hybride peut vous aider à :
 
> [!div class="checklist"]
> * Lancer une nouvelle build basée sur un référentiel de code validations tooyour Visual Studio Team Services (VSTS).
> * Déployer automatiquement votre tooAzure code nouvellement généré pour le test d’acceptation utilisateur.
> * Une fois que votre code a passé les tests, déployer automatiquement tooAzure pile. 


## <a name="prerequisites"></a>Composants requis
Quelques composants sont requis toobuild un pipeline de l’élément de configuration/CD hybride et peuvent prendre quelques tooprepare de temps.  Si vous avez déjà certains de ces composants, assurez-vous que ceux-ci répondent aux exigences de hello avant de commencer.

Cette rubrique suppose également que vous connaissez déjà Azure et Azure Stack. Si vous souhaitez toolearn plus avant de continuer, être toostart que les rubriques suivantes :

- [Introduction tooAzure](https://docs.microsoft.com/azure/fundamentals-introduction-to-azure)
- [Concepts clés d’Azure Stack](azure-stack-key-features.md)

### <a name="azure"></a>Microsoft Azure
 - Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.
 - Créez une [application web](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md), puis configurez-la pour la [publication FTP](../app-service-web/app-service-deploy-ftp.md).  Prenez note de hello nouvelle URL de l’application Web, tel qu’il est utilisé ultérieurement.


### <a name="azure-stack"></a>Azure Stack
 - [Déployez Azure Stack](azure-stack-run-powershell-script.md).  installation de Hello prend généralement quelques heures toocomplete, donc planifier en conséquence.
 - Déployer [du Service d’applications](azure-stack-app-service-deploy.md) tooAzure pile des services PaaS.
 - Créez une application web, puis configurez-la pour la [publication FTP](azure-stack-app-service-enable-ftp.md).  Prenez note de hello nouvelle URL de l’application Web, tel qu’il est utilisé ultérieurement.  

### <a name="developer-tools"></a>Outils de développeur
 - Créez un [espace de travail VSTS](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).  le processus d’inscription Hello crée un projet nommé « MyFirstProject ».  
 - [Installer Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio) et [tooVSTS de connexion](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#connect-and-share-code-from-visual-studio)
 - Connecter toohello projet et [cloner localement](https://www.visualstudio.com/docs/git/gitquickstart).
 - Créez un [pool d’agents](https://www.visualstudio.com/docs/build/concepts/agents/pools-queues#creating-agent-pools-and-queues) dans VSTS.
 - Installer Visual Studio et déployer un [l’agent de build VSTS](https://www.visualstudio.com/docs/build/actions/agents/v2-windows) virtuels tooa sur la pile de Azure. 
 

## <a name="create-app--push-toovsts"></a>Créer tooVSTS & par émission de données d’application

### <a name="create-application"></a>Créer une application
Dans cette section, vous créez une application ASP.NET simple et poussez tooVSTS.  Ces étapes représentent le flux de travail de développeur normal hello et pourrait être adaptés pour les langages et outils de développement. 

1.  Ouvrez Visual Studio.
2.  À partir de hello espace de Team Explorer et **Solutions...**  zone, cliquez sur **nouveau**.
3.  Sélectionnez **Visual C#** > **Web** > **Application web ASP.NET (.NET Framework)**.
4.  Fournissez un nom pour l’application hello et cliquez sur **OK**.
5.  Sur l’écran suivant de hello, conservez les valeurs par défaut de hello (Web forms), puis cliquez sur **OK**.

### <a name="commit-and-push-changes-toovsts"></a>Validez et envoyez des modifications tooVSTS
1.  À l’aide de Team Explorer dans Visual Studio, sélectionnez la liste déroulante de hello et cliquez sur **modifications**.
2.  Indiquez un message de validation, puis sélectionnez **Valider tout**. Vous pouvez soit être invité à toosave hello solution fichier, cliquez sur Oui toosave de tous les.
3.  Une fois validées, Visual Studio propose des projets de tooyour toosync modifications. Sélectionnez **Synchroniser**.

    ![écran de validation de hello image montrant une fois que la fin de la validation](./media/azure-stack-solution-pipeline/image1.png)

4.  Dans l’onglet synchronisation hello sous *sortant*, vous voyez votre nouvelle validation.  Sélectionnez **Push** toosynchronize hello modifier tooVSTS.

    ![image montrant les étapes de la synchronisation](./media/azure-stack-solution-pipeline/image2.png)

### <a name="review-code-in-vsts"></a>Revoir le code dans VSTS
Une fois vous avez validé une modification et envoyée tooVSTS, vérifiez que votre code à partir du portail VSTS hello.  Sélectionnez **Code**, puis **fichiers** à partir du menu déroulant de hello.  Vous pouvez voir des solutions hello que vous avez créé.

## <a name="create-build-definition"></a>Création d’une définition de build
processus de génération Hello définit la manière dont votre application est créée et empaquetée pour le déploiement sur chaque validation des modifications du code. Dans notre exemple, nous utiliser des processus de génération de hello inclus modèle tooconfigure hello pour une application ASP.NET, bien que cette configuration peut être adaptée en fonction de votre application.

1.  Se connecter tooyour espace de travail VSTS à partir d’un navigateur web.
2.  Dans la bannière de hello, sélectionnez **générer & version** , puis **génère**.
3.  Sélectionnez **+ Nouvelle définition**.
4.  Dans la liste hello des modèles, sélectionnez **ASP.NET (version préliminaire)** et sélectionnez **appliquer**.
5.  Modifier hello *Arguments MSBuild* champ *générer la Solution* à l’étape :

    `/p:DeployOnBuild=True /p:WebPublishMethod=FileSystem /p:DeployDefaultTarget=WebPublish /p:publishUrl="$(build.artifactstagingdirectory)\\"`

6.  Sélectionnez hello **Options** onglet file d’attente et sélectionnez hello agent pourquoi l’agent de build vous déployé tooa une machine virtuelle sur Azure pile. 
7.  Sélectionnez hello **déclencheurs** onglet et activer **intégration continue**.
7.  Cliquez sur **enregistrer et de file d’attente** , puis sélectionnez **enregistrer** à partir de la liste déroulante de hello. 

## <a name="create-release-definition"></a>Création d’une définition de mise en production
processus de mise en production Hello définit comment les générations à partir de l’étape précédente de hello sont déployés tooan environnement.  Dans ce didacticiel, nous publions notre application ASP.NET avec FTP tooan application Web Azure. tooconfigure un tooAzure mise en production, utilisez hello comme suit :

1.  Dans la bannière de VSTS hello, sélectionnez **générer & version** , puis **versions**.
2.  Cliquez sur hello verte **+ nouvelle définition**.
3.  Sélectionnez **Vide** et cliquez sur **Suivant**.
4.  Case de hello pour *déploiement continu*, puis cliquez sur **créer**.

Maintenant que vous avez créé une définition de version vide et il liée toohello build, nous ajoutons des étapes pour hello environnement Azure :

1.  Cliquez sur hello verte  **+**  tooadd tâches.
2.  Sélectionnez **tous les**, puis à partir de la liste de hello, ajoutez **de téléchargement FTP** et sélectionnez **fermer**.
3.  Sélectionnez hello **de téléchargement FTP** tâche que vous venez d’ajouter et configurer les paramètres suivants de hello :
    
    | Paramètre | Valeur |
    | ----- | ----- |
    |Méthode d'authentification| Entrer les informations d’identification|
    |URL du serveur | URL FTP de l’application web récupérée à partir du portail Azure |
    |Nom d’utilisateur | Nom d’utilisateur que vous avez configuré lors de la création des informations d’identification FTP pour l’application web |
    |Mot de passe | Mot de passe que vous avez créé lors de la définition des informations d’identification FTP pour l’application web|
    |Répertoire source | $(System.DefaultWorkingDirectory)\**\ |
    |Répertoire distant | /site/wwwroot/ |
    |Conserver les chemins de fichiers | Activé (coché)|

4.  Cliquez sur **Enregistrer**.

Enfin, vous configurer hello version définition toouse hello pool d’agents contenant agent hello déployé à l’aide de hello comme suit :
1.  Sélectionnez la définition de la version hello et cliquez sur **modifier**.
2.  Sélectionnez **s’exécutent sur l’agent** à partir de la colonne du milieu hello.  Dans la colonne de droite hello, sélectionnez la file d’attente de l’agent hello contenant l’agent de build hello en cours d’exécution sur la pile de Azure.  
    ![configuration d’affichant l’image de file d’attente spécifique version définition toouse](./media/azure-stack-solution-pipeline/image3.png)


## <a name="deploy-your-app-tooazure"></a>Déployer votre application tooAzure
Cette étape utilise votre nouvellement créé l’élément de configuration/CD pipeline toodeploy hello ASP.NET application tooa application Web sur Azure. 

1.  Dans la bannière de hello dans VSTS, sélectionnez **générer & version**, puis sélectionnez **génère**.
2.  Cliquez sur **...**  sur hello créée précédemment de définition de build, puis sélectionnez **nouvelle build en file d’attente**.
3.  Acceptez les valeurs par défaut hello et cliquez sur **Ok**.  génération de Hello commence et affiche la progression.
4.  Une fois la génération de hello est terminée, vous pouvez suivre l’état de hello en sélectionnant **générer & version** et en sélectionnant **versions**.
5.  Une fois la génération de hello est terminée, le site hello à l’aide des URL hello indiqué lors de la création de hello Web App.    


## <a name="add-azure-stack-toopipeline"></a>Ajouter Azure pile toopipeline
Maintenant que vous avez testé votre pipeline de l’élément de configuration/CD en déployant tooAzure, il est temps tooadd pipeline toohello de pile de Azure.  Bonjour comme suit, vous créez un environnement et ajoutez un toodeploy de tâche FTP télécharger votre tooAzure application pile.  Vous ajoutez également un approbateur de version, qui sert d’un toosimulate de façon « approbation » sur un tooAzure de version du code pile.  

1.  Dans la définition de la version de hello, sélectionnez **+ ajouter un environnement** et **créer un nouvel environnement**.
2.  Sélectionnez **Vide** et cliquez sur **Suivant**.
3.  Sélectionnez **Utilisateurs spécifiques** et spécifiez votre compte.  Sélectionnez **Créer**.
4.  Renommer l’environnement de hello en sélectionnant nom existant de hello et en tapant *Azure pile*.
5.  À présent, sélection hello environnement Azure pile, puis sélectionnez **ajouter des tâches**.
6.  Sélectionnez hello **de téléchargement FTP** de tâches et sélectionnez **ajouter**, puis sélectionnez **fermer**.


### <a name="configure-ftp-task"></a>Configurer une tâche FTP
Maintenant que vous avez créé une mise en production, vous allez configurer les étapes de hello requises pour la publication toohello application Web sur la pile de Azure.  Tout comme vous avez configuré la tâche de téléchargement FTP hello pour Azure, vous configurez tâche hello pour la pile de Azure :

1.  Sélectionnez hello **de téléchargement FTP** tâche que vous venez d’ajouter et configurer les paramètres suivants de hello :
    
    | Paramètre | Valeur |
    | -----     | ----- |
    |Méthode d'authentification| Entrer les informations d’identification|
    |URL du serveur | URL FTP de l’application web récupérée à partir du portail Azure Stack |
    |Nom d’utilisateur | Nom d’utilisateur que vous avez configuré lors de la création des informations d’identification FTP pour l’application web |
    |Mot de passe | Mot de passe que vous avez créé lors de la définition des informations d’identification FTP pour l’application web|
    |Répertoire source | $(System.DefaultWorkingDirectory)\**\ |
    |Répertoire distant | /site/wwwroot/|
    |Conserver les chemins de fichiers | Activé (coché)|

2.  Cliquez sur **Enregistrer**.

Enfin, configurez hello version définition toouse hello pool d’agents contenant agent hello déployé à l’aide de hello comme suit :
1.  Sélectionnez la définition de la version hello et cliquez sur **modifier**
2.  Sélectionnez **s’exécutent sur l’agent** à partir de la colonne du milieu hello. Dans la colonne de droite hello, sélectionnez la file d’attente de l’agent hello contenant l’agent de build hello en cours d’exécution sur la pile de Azure.  
    ![configuration d’affichant l’image de file d’attente spécifique version définition toouse](./media/azure-stack-solution-pipeline/image3.png)

## <a name="deploy-new-code"></a>Déployer un nouveau code
Vous pouvez désormais tester le pipeline de l’élément de configuration/CD hello hybride, avec tooAzure publication de l’étape finale de hello pile.  Dans cette section, vous modifiez le pied de page du site hello et démarrez le déploiement via le pipeline de hello.  Une fois terminé, vous verrez les modifications déploiement tooAzure pour révision, puis une fois que vous approuvez la mise en production hello, ils sont publié tooAzure pile.

1. Dans Visual Studio, ouvrez hello *site.master* de fichiers et de modifier cette ligne :
    
    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application</p>
    `

    toothis :

    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application delivered by VSTS, Azure, and Azure Stack</p>
    `
3.  La synchronisation tooVSTS et valider les modifications de hello.  
4.  À partir de l’espace de travail hello VSTS, vérifier l’état de la build hello en sélectionnant **générer & version** > **générer**
5.  Vous voyez une build en cours d’exécution.  Double-cliquez sur l’état de hello, et vous pouvez surveiller la progression de la génération hello.  Une fois que vous voyez « Build terminée » dans la console hello, déplacer sur la version de hello toocheck à partir de **générer & version** > **version**.  Double-cliquez sur mise en production hello.
6.  Vous recevrez une notification indiquant qu’une mise en production doit être examinée. Vérifiez hello URL de l’application Web et les nouvelles modifications de hello sont présentes.  Approuver la mise en production hello dans VSTS.
    ![configuration d’affichant l’image de file d’attente spécifique version définition toouse](./media/azure-stack-solution-pipeline/image4.png)
    
7.  Vérifiez la publication tooAzure que pile est terminée en visitant le site Web de hello à l’aide des URL hello indiqué lors de la création de hello Web App.
    ![image montrant l’application ASP.NET avec le pied de page modifié](./media/azure-stack-solution-pipeline/image5.png)


Vous pouvez maintenant utiliser votre nouveau pipeline CI/CD hybride comme bloc de construction pour d’autres modèles de cloud hybrides.

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toobuild un élément de configuration/CD hybride de pipeline qui :

> [!div class="checklist"]
> * Initialise une nouvelle build basée sur un référentiel de code validations tooyour Visual Studio Team Services (VSTS).
> * Déploie automatiquement votre tooAzure code nouvellement généré pour le test d’acceptation utilisateur.
> * Une fois que votre code a passé les tests, déploie automatiquement tooAzure pile. 

Maintenant que vous avez un pipeline de l’élément de configuration/CD hybride, continuez en apprentissage comment toodevelop des applications pour la pile de Azure.

> [!div class="nextstepaction"]
> [Développer pour Azure Stack](azure-stack-developer.md)


