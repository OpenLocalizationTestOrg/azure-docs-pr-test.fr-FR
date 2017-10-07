---
title: les projets de groupe de ressources Windows Azure Studio aaaVisual | Documents Microsoft
description: "Utilisez Visual Studio toocreate un projet de groupe de ressources Azure et déployer hello ressources tooAzure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Création et déploiement de groupes de ressources Azure à l’aide de Visual Studio
Avec Visual Studio et hello [Azure SDK](https://azure.microsoft.com/downloads/), vous pouvez créer un projet qui déploie tooAzure de votre infrastructure et de code. Par exemple, vous pouvez définir des hello web hôte, site web et base de données pour votre application et déployer cette infrastructure et du code hello. Ou bien, vous pouvez définir une machine virtuelle, le réseau virtuel et le compte de stockage, puis déployer cette infrastructure parallèlement à un script exécuté sur la machine virtuelle. Hello **groupe de ressources Azure** permet à un projet de déploiement vous toodeploy toutes les ressources hello nécessité dans une opération unique et reproductible. Pour plus d’informations sur le déploiement et la gestion des ressources, consultez [Présentation d’Azure Resource Manager](resource-group-overview.md).

Les projets de groupe de ressources Azure contiennent des modèles Azure Resource Manager JSON, qui définissent les ressources hello que vous déployez tooAzure. toolearn sur les éléments de hello du modèle du Gestionnaire de ressources hello, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md). Visual Studio permet de vous tooedit ces modèles et fournit des outils qui simplifient l’utilisation des modèles.

Dans cet article, vous déployez une application web et SQL Database. Toutefois, les étapes de hello sont presque hello même pour n’importe quelle ressource de type. Vous pouvez tout aussi facilement déployer une machine virtuelle et ses ressources associées. Visual Studio fournit de nombreux modèles de démarrage différents pour déployer des scénarios courants.

Cet article présente Visual Studio 2017. Si vous utilisez Visual Studio 2015 Update 2 et Microsoft Azure SDK pour .NET 2.9, ou Visual Studio 2013 avec Azure SDK 2.9, votre expérience est en grande partie hello identiques. Vous pouvez utiliser les versions de hello Azure SDK de 2.6 ou version ultérieure ; Toutefois, votre expérience de l’interface utilisateur de hello peut être différent de celui de l’interface utilisateur hello illustré dans cet article. Nous recommandons fortement d’installer la version la plus récente de hello hello [Azure SDK](https://azure.microsoft.com/downloads/) avant de commencer les étapes hello. 

## <a name="create-azure-resource-group-project"></a>Créer un projet de groupe de ressources Azure
Au cours de cette procédure, vous allez apprendre à créer un projet de groupe de ressources Azure avec un modèle **Application web + SQL** .

1. Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**, puis choisissez **C#** ou **Visual Basic**. Choisissez ensuite **Cloud** et le projet de **Groupe de ressources Azure**.
   
    ![Projet de déploiement cloud](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Choisissez le modèle de hello que vous souhaitez toodeploy tooAzure le Gestionnaire de ressources. Notez, il existe de nombreuses options en fonction de hello type de projet que vous souhaitez toodeploy. Pour cet article, choisissez hello **Web application + SQL** modèle.
   
    ![Sélectionner un modèle](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    Vous pouvez choisir de modèle de Hello est simplement un point de départ ; Vous pouvez ajouter et supprimer des ressources toofulfill votre scénario.
   
   > [!NOTE]
   > Visual Studio extrait une liste des modèles disponibles en ligne. liste de Hello peut changer.
   > 
   > 
   
    Visual Studio crée un projet de déploiement de groupe de ressources pour l’application web hello et base de données SQL.
3. toosee ce que vous avez créé, regardez au nœud hello hello projet de déploiement.
   
    ![afficher les nœuds](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Étant donné que nous avons choisi hello Web application + modèle SQL pour cet exemple, vous consultez hello fichiers suivants : 
   
   | Nom de fichier | Description |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |Un script PowerShell qui appelle tooAzure toodeploy de commandes PowerShell Gestionnaire de ressources.<br />**Remarque** Visual Studio utilise ce toodeploy de script PowerShell de votre modèle. Toutes les modifications que vous apportez toothis script affectent le déploiement dans Visual Studio, soyez donc prudent. |
   | WebSiteSQLDatabase.json |modèle de gestionnaire de ressources Hello qui définit l’infrastructure hello à déployer tooAzure et paramètres hello que vous pouvez fournir au cours du déploiement. Il définit également les dépendances de hello entre les ressources de hello pour le Gestionnaire de ressources déploie des ressources hello dans l’ordre correct de hello. |
   | WebSiteSQLDatabase.parameters.json |Un fichier de paramètres qui contient les valeurs requises par le modèle de hello. Vous passez toocustomize de valeurs de paramètre chaque déploiement. |
   
    Tous les projets de déploiement de groupe de ressources Azure contiennent ces fichiers de base. Autres projets peuvent contenir des fichiers supplémentaires toosupport autres fonctionnalités.

## <a name="customize-hello-resource-manager-template"></a>Personnaliser le modèle de gestionnaire de ressources hello
Vous pouvez personnaliser un projet de déploiement en modifiant les modèles hello JSON qui décrivent les ressources hello toodeploy. JSON signifie JavaScript Object Notation et est un format des données sérialisées facile toowork avec. fichiers au format JSON Hello utilisent un schéma que vous référencez haut hello de chaque fichier. Si vous souhaitez que le schéma de hello toounderstand, vous pouvez télécharger et l’analyser. Hello schéma définit quels éléments sont valides, hello types et formats de champs, les valeurs possibles des valeurs énumérées de hello et ainsi de suite. toolearn sur les éléments de hello du modèle du Gestionnaire de ressources hello, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).

toowork sur votre modèle, ouvrez **WebSiteSQLDatabase.json**.

les outils de Hello Visual Studio fournit de l’éditeur tooassist vous édition hello modèle du Gestionnaire de ressources. Hello **structure JSON** fenêtre rend les éléments de hello toosee facilement définis dans votre modèle.

![afficher la structure JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

En sélectionnant un des éléments de hello dans le plan de hello participe vous toothat du modèle de hello et met en évidence hello correspondant JSON.

![explorer JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

Vous pouvez ajouter une ressource en soit en sélectionnant hello **ajouter une ressource** dans hello la partie supérieure de la fenêtre de structure JSON hello ou en double-cliquant sur **ressources** et en sélectionnant **ajouter une nouvelle ressource**.

![ajouter une ressource](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

Pour ce didacticiel, sélectionnez **Compte de stockage** et donnez-lui un nom. Choisissez un nom qui ne contient pas plus de 11 caractères et uniquement des chiffres et des lettres minuscules.

![ajouter du stockage](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Notez que non seulement les ressources hello ajouté, mais également pourquoi un paramètre de type de compte de stockage et une variable pour le nom hello hello du compte de stockage.

![afficher la structure](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

Hello **storageType** paramètre est prédéfini avec les types autorisés et d’un type par défaut. Vous pouvez laisser ces valeurs ou les modifier pour votre scénario. Si vous ne souhaitez pas que tout le monde toodeploy un **Premium_LRS** compte de stockage via ce modèle, supprimez-le hello types autorisé. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Visual Studio fournit également toohelp intellisense vous comprenez quelles propriétés sont disponibles lors de la modification du modèle de hello. Par exemple, les propriétés de hello tooedit pour votre plan de Service d’applications, accédez toohello **HostingPlan** ressource, ajoutez une valeur pour hello **propriétés**. Notez qu’intellisense affiche les valeurs disponibles hello et fournit une description de cette valeur.

![afficher intellisense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

Vous pouvez définir **numberOfWorkers** too1.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>Déployer tooAzure de projet de groupe de ressources hello
Vous est toodeploy maintenant prêt à votre projet. Lorsque vous déployez un projet de groupe de ressources Azure, vous déployez groupe de ressources Azure tooan. groupe de ressources Hello est un regroupement logique des ressources qui partagent un cycle de vie courants.

1. Dans le menu contextuel de hello du nœud de projet de déploiement hello, choisissez **déployer** > **nouveau**.
   
    ![Déployer, élément de menu Nouveau déploiement](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    Hello **déployer tooResource groupe** boîte de dialogue s’affiche.
   
    ![TooResource boîte de dialogue groupe de déploiement](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. Bonjour **groupe de ressources** zone de liste déroulante, choisissez un groupe de ressources existant ou créez-en un. toocreate un groupe de ressources, ouvrez hello **groupe de ressources** liste déroulante et sélectionnez **créer un nouveau**.
   
    ![TooResource boîte de dialogue groupe de déploiement](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    Hello **créer un groupe de ressources** boîte de dialogue s’affiche. Donnez à votre groupe d’un nom et un emplacement, puis sélectionnez les hello **créer** bouton.
   
    ![Boîte de dialogue Créer un groupe de ressources](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Modifier les paramètres de hello pour le déploiement de hello en sélectionnant hello **modifier les paramètres** bouton.
   
    ![Bouton Modifier les paramètres](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Fournir des valeurs pour les paramètres vides hello et sélectionnez hello **enregistrer** bouton. les paramètres vides Hello sont **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, et **databaseName**.
   
    **hostingPlanName** spécifie un nom pour hello [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate. 
   
    **administratorLogin** Spécifie le nom d’utilisateur hello pour l’administrateur de SQL Server hello. N’utilisez pas de noms d’administrateur communs comme **sa** ou **admin**. 
   
    Hello **administratorLoginPassword** Spécifie le mot de passe d’administrateur SQL Server. Hello **enregistrer les mots de passe en texte brut dans le fichier de paramètres hello** option n’est pas sécurisée ; par conséquent, ne sélectionnez pas de cette option. Étant donné que le mot de passe hello n’est pas enregistrée en tant que texte brut, vous devez tooprovide ce mot de passe à nouveau lors du déploiement. 
   
    **databaseName** spécifie un nom pour toocreate de base de données hello. 
   
    ![Boîte de dialogue Modifier les paramètres](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Choisissez hello **déployer** bouton toodeploy hello projet tooAzure. Il ouvre une console PowerShell en dehors de l’instance de Visual Studio hello. Entrez le mot de passe administrateur de SQL Server hello dans la console PowerShell hello lorsque vous y êtes invité. **Votre console PowerShell est masqué par d’autres éléments ou réduite dans la barre des tâches hello.** Recherchez cette console et le mot de passe tooprovide hello sélectionner.
   
   > [!NOTE]
   > Visual Studio peut vous demander tooinstall hello applets de commande PowerShell de Azure. Vous devez hello Azure PowerShell toosuccessfully d’applets de commande déployer des groupes de ressources. Si vous y êtes invité, installez-les.
   > 
   > 
6. déploiement de Hello peut prendre quelques minutes. Bonjour **sortie** windows, vous voyez l’état hello du déploiement de hello. Déploiement de hello terminée, dernier message de type hello indique un déploiement réussi avec quelque chose de similaire à :
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. Dans un navigateur, ouvrez hello [portail Azure](https://portal.azure.com/) et tooyour compte de connexion. toosee hello groupe de ressources, sélectionnez **groupes de ressources** et groupe de ressources hello vous avez déployé sur.
   
    ![sélectionner un groupe](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Affiche toutes les ressources hello déployé. Notez que le nom du hello hello compte de stockage n’est pas exactement ce que vous spécifié lors de l’ajout de cette ressource. compte de stockage Hello doit être unique. Hello modèle ajoute automatiquement une chaîne de nom de toohello caractères vous avez fourni tooprovide un nom unique. 
   
    ![afficher des ressources](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Si vous modifiez et que vous souhaitez tooredeploy votre projet, choisissez le groupe de ressources existant hello à partir du menu contextuel de hello du projet de groupe de ressources Azure. Dans le menu contextuel de hello, choisissez **déployer**, puis choisissez le groupe de ressources hello vous avez déployé.
   
    ![Groupe de ressources Azure déployé](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Déployer le code avec votre infrastructure
À ce stade, vous avez déployé l’infrastructure de hello pour votre application, mais aucun code réel déployé avec hello projet. Cet article explique comment toodeploy une application web et la base de données SQL des tables au cours du déploiement. Si vous déployez un ordinateur virtuel au lieu d’une application web, vous souhaitez toorun du code sur l’ordinateur hello dans le cadre du déploiement. Hello du processus de déploiement de code pour une application web ou pour la configuration d’un ordinateur virtuel est presque hello identiques.

1. Ajouter un projet de tooyour solution Visual Studio. Solution de hello d’avec le bouton droit, puis sélectionnez **ajouter** > **nouveau projet**.
   
    ![ajouter un projet](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Ajoutez une **application web ASP.NET**. 
   
    ![ajouter une application web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. Sélectionnez **MVC**.
   
    ![sélectionner MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Une fois que Visual Studio crée votre application web, vous voyez les deux projets dans la solution de hello.
   
    ![afficher les projets](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. Maintenant, vous devez toomake sûr que votre projet de groupe de ressources de projet hello. Retournez dans le projet de groupe de ressources tooyour (AzureResourceGroup1). Cliquez avec le bouton droit sur **Références** et sélectionnez **Ajouter une référence**.
   
    ![Ajouter une référence](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Sélectionnez le projet d’application web hello que vous avez créé.
   
    ![Ajouter une référence](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    En ajoutant une référence, vous liez des hello projet toohello ressource groupe projet d’application web et définissez automatiquement les trois propriétés de clé. Vous voyez ces propriétés Bonjour **propriétés** fenêtre pour la référence de hello.
   
      ![voir une référence](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    propriétés de Hello sont :
   
   * Hello **des propriétés supplémentaires** contient le package de déploiement web hello transit poussé toohello le stockage Azure. Notez le dossier hello (ExampleApp) et le fichier (package.zip). Vous devez tooknow ces valeurs, car vous fournissez comme paramètres lors du déploiement hello application. 
   * Hello **incluent le chemin d’accès** contient le chemin d’accès hello dans lequel le package de hello est créé. Hello **incluent les cibles** contient la commande hello qui s’exécute de déploiement. 
   * Hello la valeur par défaut de **générer ; Package** Active hello toobuild de déploiement et de créer un package de déploiement web (package.zip).  
     
     Vous n’avez pas besoin d’un profil de publication que le déploiement de hello Obtient les informations nécessaires hello à partir du package de hello propriétés toocreate hello.
7. TooWebSiteSQLDatabase.json revenir en arrière et ajouter un modèle de toohello de ressources.
   
    ![ajouter une ressource](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. Cette fois-ci, sélectionnez **Web Deploy pour les applications Web**. 
   
    ![ajouter web deploy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. Redéployez votre groupe projet toohello groupe de ressources. Cette fois, il y a de nouveaux paramètres. Vous n’avez pas besoin de valeurs tooprovide pour **_artifactsLocation** ou **_artifactsLocationSasToken** , car Visual Studio génère automatiquement ces valeurs. Toutefois, vous devez le dossier de hello tooset et nom toohello chemin d’accès qui contient le package de déploiement hello (indiqué en tant que **ExampleAppPackageFolder** et **ExampleAppPackageFileName** Bonjour suivant d’image ). Fournir les valeurs hello, vous avez vu précédemment dans hello des propriétés de la référence (**ExampleApp** et **package.zip**).
   
    ![ajouter web deploy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Pourquoi **compte de stockage artefact**, sélectionnez hello une déployée avec ce groupe de ressources.
10. Une fois le déploiement de hello est terminé, sélectionnez votre application web dans le portail de hello. Sélectionnez hello URL toobrowse toohello site.
    
     ![parcourir le site](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Notez que vous avez correctement déployé hello d’application ASP.NET par défaut.
    
     ![afficher l’application déployée](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la gestion de vos ressources via le portail de hello, consultez [Using hello toomanage portail Azure vos ressources Azure](resource-group-portal.md).
* toolearn savoir plus sur les modèles, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).

