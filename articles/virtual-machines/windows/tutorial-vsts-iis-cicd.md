---
title: "aaaCreate un pipeline de l’élément de configuration/CD dans Azure avec Team Services | Documents Microsoft"
description: "Découvrez comment toocreate un Visual Studio Team Services pipeline pour l’intégration continue et de remise qui déploie un tooIIS d’application web sur une machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>Création d’un pipeline d’intégration continue avec Visual Studio Team Services et IIS
génération de hello tooautomate, de test et des phases de déploiement du développement d’applications, vous pouvez utiliser une intégration continue et le pipeline de déploiement de (l’élément de configuration/CD). Dans ce didacticiel, vous créez un pipeline CI/CD à l’aide de Visual Studio Team Services et d’une machine virtuelle Windows (VM) dans Azure qui exécute IIS. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Publier un projet d’équipe Services ASP.NET web application tooa
> * Créer une définition de build qui est déclenchée par les validations de code
> * Installer et configurer IIS sur une machine virtuelle dans Azure
> * Ajouter un groupe de déploiement hello tooa de l’instance IIS dans Team Services
> * Créez une version définition toopublish web tooIIS de packages de déploiement
> * Tester le pipeline de l’élément de configuration/CD hello

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez `Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).


## <a name="create-project-in-team-services"></a>Création d’un projet dans Team Services
Visual Studio Team Services simplifie la collaboration et permet le développement sans recours à une solution de gestion de code en local. Team Services offre des fonctionnalités de test de code, de création et d’analyse de l’application dans le cloud. Vous pouvez choisir le référentiel de contrôle de version et l’IDE qui conviennent le mieux au développement de votre code. Pour ce didacticiel, vous pouvez utiliser un compte gratuit toocreate une base d’application web ASP.NET et le pipeline de l’élément de configuration/CD. Si vous n’avez pas encore de compte Team Services, [créez-en un](http://go.microsoft.com/fwlink/?LinkId=307137).

processus de validation code toomanage hello, définitions de build et définitions de version, créez un projet dans Team Services, comme suit :

1. Ouvrez votre tableau de bord Team Services dans un navigateur web et choisissez **Nouveau projet**.
2. Entrez *myWebApp* pour hello **nom du projet**. Laissez toutes les autres toouse de valeurs par défaut *Git* contrôle de version et *Agile* processus de l’élément de travail.
3. Choisir hello trop**partager avec** *membres de l’équipe*, puis sélectionnez **créer**.
5. Une fois que votre projet a été créé, choisir hello trop**initialiser avec un fichier Lisez-moi ou la gitignore**, puis **initialiser**.
6. À l’intérieur de votre nouveau projet, choisissez **tableaux de bord** haut de hello, puis sélectionnez **ouvert dans Visual Studio**.


## <a name="create-aspnet-web-application"></a>Création d’une application web ASP.NET
Dans l’étape précédente de hello, vous avez créé un projet dans Team Services. étape finale de Hello ouvre votre nouveau projet dans Visual Studio. Vous gérez vos validations code Bonjour **Team Explorer** fenêtre. Créez une copie locale de votre nouveau projet, puis créez une application web ASP.NET à partir d’un modèle comme suit :

1. Sélectionnez **Clone** toocreate un référentiel git local de votre projet Team Services.
    
    ![Clonage du référentiel à partir du projet Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. Sous **Solutions**, sélectionnez **Nouveau**.

    ![Création de la solution d’application web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. Sélectionnez **Web** modèles, puis choisissez hello **Application Web ASP.NET** modèle.
    1. Entrez un nom pour votre application, tel que *myWebApp*, puis décochez la case hello pour **créer le répertoire pour la solution**.
    2. Si l’option de hello est disponible, hello désactivez case à cocher trop**ajouter Application Insights tooproject**. Application Insights a besoin votre application web avec Azure Application Insights vous tooauthorize. tookeep il simple dans ce didacticiel, ignorez ce processus.
    3. Sélectionnez **OK**.
4. Choisissez **MVC** à partir de la liste des modèles hello.
    1. Pour **Modifier l’authentification**, sélectionnez **Aucune authentification**, puis sélectionnez **OK**.
    2. Sélectionnez **OK** toocreate votre solution.
5. Bonjour **Team Explorer** fenêtre, choisissez **modifications**.

    ![Valider le référentiel git de modifications locales tooTeam Services](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. Dans la zone de texte de validation hello, entrez un message tel que *la validation initiale*. Choisissez **valider tous les et synchronisation** à partir du menu déroulant de hello.


## <a name="create-build-definition"></a>Création d’une définition de build
Dans les Services d’équipe, vous utilisez un toooutline de définition de build comment votre application doit être créée. Dans ce didacticiel, nous créer une définition de base que prend notre code source, génère hello solution, puis crée web déployer le package, nous pouvons utiliser toorun hello web application sur un serveur IIS.

1. Dans votre projet de Services d’équipe, choisissez **générer & version** haut de hello, puis sélectionnez **génère**.
3. Sélectionnez **+ Nouvelle définition**.
4. Choisissez hello **ASP.NET (version préliminaire)** modèle et sélectionnez **appliquer**.
5. Laissez par défaut de hello toutes les valeurs de la tâche. Sous **obtenir les sources**, vérifiez que hello *myWebApp* référentiel et *master* branche sont sélectionnés.

    ![Création d’une définition de build dans le projet Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. Sur hello **déclencheurs** onglet, déplacez le curseur hello pour **activer ce déclencheur** trop*activé*.
7. Enregistrer la définition de build hello et file d’attente une nouvelle build en sélectionnant **enregistrer et de file d’attente** , puis **enregistrer et de file d’attente** à nouveau. Laissez les valeurs par défaut hello et sélectionnez **file d’attente**.

Espion que build de hello est planifiée sur un agent hébergé, puis commence à toobuild. Hello la sortie est similaire toohello l’exemple suivant :

![Génération réussie du projet Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>Create virtual machine
tooprovide un toorun plateforme votre application web ASP.NET, vous avez besoin d’une machine virtuelle Windows qui exécute IIS. Team Services utilise une toointeract de l’agent avec une instance IIS hello que vous validez le code et les builds sont déclenchées.

Créez une machine virtuelle Windows Server 2016 à l’aide de [cet exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json). Il prend quelques minutes pour hello script toorun et créer hello machine virtuelle. Une fois que hello machine virtuelle a été créé, ouvrez le port 80 pour le trafic web avec [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) comme suit :

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooconnect tooyour machine virtuelle, obtenir l’adresse IP publique de hello avec [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) comme suit :

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

Créer une machine virtuelle de tooyour session Bureau à distance :

```cmd
mstsc /v:<publicIpAddress>
```

Sur la machine virtuelle de hello, ouvrez un **administrateur PowerShell** invite de commandes. Installez IIS et les fonctionnalités .NET requises comme suit :

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>Créer un groupe de déploiement
serveur IIS toohello du package de déploiement de toopush out web de hello, vous définissez un groupe de déploiement dans les Services d’équipe. Ce groupe vous permet de toospecify quels serveurs sont cible hello de nouvelles builds que vous validez tooTeam code Services et les builds sont terminées.

1. Dans Team Services, choisissez **Build & Release** (Générer et publier), puis sélectionnez **Groupes de déploiement**.
2. Choisissez **Add Deployment group** (Ajouter un groupe de déploiement).
3. Entrez un nom pour le groupe de hello, tel que *myIIS*, puis sélectionnez **créer**.
4. Bonjour **enregistrer des ordinateurs** section, vérifiez que *Windows* est sélectionné, puis la case hello trop**utiliser un jeton d’accès personnel dans le script de hello pour l’authentification**.
5. Sélectionnez **copier le script tooclipboard**.


### <a name="add-iis-vm-toohello-deployment-group"></a>Ajouter le groupe de déploiement IIS VM toohello
Avec le groupe de déploiement hello créé, ajoutez chaque groupe toohello d’instances IIS. Team Services génère un script qui télécharge et configure un agent sur hello machine virtuelle qui reçoit le nouveau site web déploiement de packages, puis applique tooIIS.

1. Dans hello **administrateur PowerShell** session sur votre machine virtuelle, coller et exécuter le script hello copié à partir de Team Services.
2. Lorsque les balises tooconfigure demandées pour l’agent hello, choisissez *Y* et entrez *web*.
3. Lorsque vous y êtes invité pour le compte d’utilisateur hello, appuyez sur *retourner* tooaccept, hello par défaut.
4. Attendez que toofinish de script hello avec un message *vstsagent.account.computername de Service a démarré correctement*.
5. Bonjour **groupes de déploiement** page Hello **générer & version** menu, ouvrez hello *myIIS* groupe de déploiement. Sur hello **Machines** , vérifiez que votre machine virtuelle est répertorié.

    ![Machine virtuelle correctement ajouté le groupe de déploiement de Services tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>Création d’une définition de mise en production
toopublish vos builds, vous créez une définition de version dans Team Services. Cette définition est déclenchée automatiquement en cas de réussite de la génération de votre application. Vous choisissez toopush de groupe de déploiement hello votre site web déployer le package à et définissez les paramètres IIS appropriés hello.

1. Choisissez **Build & Release** (Générer et publier), puis sélectionnez **Builds**. Choisissez la définition de build hello créée à l’étape précédente.
2. Sous **récemment terminé**, choisissez la build la plus récente hello, puis sélectionnez **version**.
3. Choisissez **Oui** toocreate une définition de mise en production.
4. Choisissez hello **vide** modèle, puis sélectionnez **suivant**.
5. Vérifiez la définition de build de projet et source hello sont renseignées avec votre projet.
6. Sélectionnez hello **déploiement continu** case à cocher, puis sélectionnez **créer**.
7. Sélectionnez zone de liste déroulante hello suivant trop**+ ajouter des tâches** et choisissez *ajouter une phase de déploiement de groupe*.
    
    ![Ajouter la définition de tâche toorelease Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. Choisissez **ajouter** suivant trop**IIS Web application Deploy(Preview)**, puis sélectionnez **fermer**.
9. Sélectionnez hello **s’exécutent sur le groupe de déploiement** tâche parente.
    1. Pour **groupe de déploiement**, sélectionnez le déploiement de hello groupe que vous avez créé précédemment, comme *myIIS*.
    2. Bonjour **balises d’ordinateurs** boîte, sélectionnez **ajouter** et choisissez hello *web* balise.
    
    ![Tâche de groupe de déploiement de définition de mise en production pour IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. Sélectionnez hello **déploiement : déploiement de l’application Web de IIS** tâche tooconfigure votre IIS instance des paramètres comme suit :
    1. Pour **Nom du site web**, entrez *Site web par défaut*.
    2. Laissez hello tous les autres paramètres par défaut.
12. Choisissez **Enregistrer**, puis sélectionnez **OK** deux fois.


## <a name="create-a-release-and-publish"></a>Création d’une version et publication
Vous pouvez désormais distribuer votre package de déploiement web en tant que nouvelle version. Cette étape communique avec l’agent de hello sur chaque instance qui fait partie du groupe de déploiement hello, exécute un push de web de hello déployer le package, puis configure l’application web IIS toorun hello mis à jour.

1. Dans votre définition de mise en production, sélectionnez **+ Mise en production**, puis choisissez **Créer une mise en production**.
2. Vérifiez que la build la plus récente hello est sélectionné dans la liste déroulante hello, avec **déploiement automatisé : après la création de la version**. Sélectionnez **Créer**.
3. Une petite bannière apparaît comme haut hello de votre définition de la mise en production, *version 'Version 1' a été créée*. Sélectionnez hello version lien.
4. Ouvrez hello **journaux** onglet progression de la version toowatch hello.
    
    ![Réussite de la mise en production Team Services et de la distribution du package de déploiement web](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Une fois la mise en production hello est terminée, ouvrez un navigateur web et entrez hello IIP adresse publique de votre machine virtuelle. Votre application web ASP.NET est en cours d’exécution.

    ![Application web ASP.NET s’exécutant sur une machine virtuelle IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>Pipeline de l’élément de configuration/CD ensemble test hello
Votre application web s’exécutant sur IIS, essayez à présent pipeline de l’élément de configuration/CD hello ensemble. Une fois que vous apportez une modification dans Visual Studio et de validation, que votre code, une build est déclenchée, qui déclenche ensuite une version de votre site web mis à jour déployer le package tooIIS :

1. Dans Visual Studio, ouvrez hello **l’Explorateur de solutions** fenêtre.
2. Accédez tooand ouvrir *myWebApp | Vues | Accueil | Index.cshtml*
3. Modifiez la ligne 6 tooread :

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. Enregistrez le fichier de hello.
5. Ouvrez hello **Team Explorer** fenêtre, sélectionnez hello *myWebApp* de projet, puis choisissez **modifications**.
6. Entrez un message de validation, tel que *l’élément de configuration de test/CD pipeline*, puis choisissez **tous de la validation et la synchronisation** à partir du menu déroulant de hello.
7. Dans l’espace de travail de Team Services, une nouvelle build est déclenchée à partir de la validation de code hello. 
    - Choisissez **Build & Release** (Générer et publier), puis sélectionnez **Builds**. 
    - Choisissez votre définition de build, puis sélectionnez hello **en file d’attente et en cours d’exécution** toowatch build comme hello build progresse.
9. Une fois la génération de hello est réussie, une nouvelle version est déclenchée.
    - Choisissez **générer & version**, puis **versions** envoyée tooyour IIS VM de package de déploiement web de hello de toosee. 
    - Sélectionnez hello **Actualiser** état de l’icône tooupdate hello. Hello lorsque *environnements* colonne affiche une coche verte, mise en production hello a été déployée tooIIS.
11. appliquer les modifications toosee, actualiser votre site Web d’IIS dans un navigateur.

    ![Application web ASP.NET s’exécutant sur une machine virtuelle IIS à partir d’un pipeline CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez créé une application web ASP.NET dans les Services d’équipe et tooIIS packages lors de la validation de chaque code de déployer de build configuré et définitions version toodeploy un site web. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Publier un projet d’équipe Services ASP.NET web application tooa
> * Créer une définition de build qui est déclenchée par les validations de code
> * Installer et configurer IIS sur une machine virtuelle dans Azure
> * Ajouter un groupe de déploiement hello tooa de l’instance IIS dans Team Services
> * Créez une version définition toopublish web tooIIS de packages de déploiement
> * Tester le pipeline de l’élément de configuration/CD hello

Avancer toolearn de didacticiel suivant toohello comment toosecure un serveur web avec les certificats SSL.

> [!div class="nextstepaction"]
> [Sécuriser un serveur web avec SSL](tutorial-secure-web-server.md)