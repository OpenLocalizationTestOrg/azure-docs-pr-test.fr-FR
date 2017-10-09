---
title: "aaaProvision et déployer des microservices prévisible dans Azure"
description: "Découvrez comment toodeploy une application composée de microservices dans Azure App Service comme une unité unique et de manière prévisible à l’aide de modèles de groupe de ressources JSON et l’écriture de scripts PowerShell."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Mise en service et déploiement de microservices de manière prévisible dans Azure
Ce didacticiel montre comment tooprovision et déployer une application composée de [microservices](https://en.wikipedia.org/wiki/Microservices) dans [Azure App Service](/services/app-service/) comme une unité unique et de manière prévisible à l’aide de modèles de groupe de ressources JSON et Exécution de scripts PowerShell. 

Lors de la configuration et au déploiement d’applications à grande échelle qui sont composées de microservices hautement découplée, répétabilité et la prévisibilité sont cruciales toosuccess. [Azure App Service](/services/app-service/) vous permet de microservices toocreate qui incluent des applications web, des applications mobiles, les applications API et applications de la logique. [Le Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) permet vous toomanage tous les hello microservices en tant qu’unité, ainsi que les dépendances des ressources telles que les paramètres de contrôle source et de la base de données. À présent, vous pouvez également déployer une application de ce type à l’aide de modèles JSON et de scripts PowerShell simples. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Procédure à suivre
Dans le didacticiel de hello, vous allez déployer une application qui comprend :

* Deux applications Web (par exemple, deux microservices)
* Une base de données SQL principale
* Paramètres d’application, chaînes de connexion et contrôle de code source
* Paramètres de mise à l’échelle automatique, alertes et Application Insights

## <a name="tools-you-will-use"></a>Outils à utiliser
Dans ce didacticiel, vous allez utiliser hello suite d’outils. Dans la mesure où il n’est pas plus d’informations sur les outils, je vais scénario de bout en bout toostick toohello et simplement vous donne une brève introduction tooeach, et où vous trouverez plus d’informations sur ce dernier. 

### <a name="azure-resource-manager-templates-json"></a>Modèles Microsoft Azure Resource Manager (JSON)
Chaque fois que vous créez une application web dans Azure App Service, par exemple, Azure Resource Manager utilise un groupe de ressources entière JSON modèle toocreate hello avec les ressources du composant hello. Un modèle complex à partir de hello [Azure Marketplace](/marketplace) comme hello [WordPress évolutive](/marketplace/partners/wordpress/scalablewordpress/) application peut inclure de base de données MySQL hello, comptes de stockage, hello plan App Service, l’application hello web lui-même, les règles d’alerte, application les paramètres, les paramètres de mise à l’échelle et plus et toutes ces modèles sont tooyou disponible via PowerShell. Pour plus d’informations sur la façon dont toodownload et utilisez ces modèles, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

Pour plus d’informations sur les modèles de hello Azure Resource Manager, consultez [de création de modèles de gestionnaire de ressources Azure](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>Kit de développement logiciel (SDK) Microsoft Azure version 2.6 pour Visual Studio
Hello plus récent SDK contient des améliorations toohello prise en charge du modèle de gestionnaire de ressources dans l’éditeur JSON hello. Vous pouvez utiliser ce tooquickly créer un modèle de groupe de ressources de toutes pièces ou ouvrir un modèle JSON existant (par exemple, un modèle de galerie téléchargé) pour la modification, remplir le fichier de paramètres hello et même déployer le groupe de ressources hello directement à partir de Azure Solution de groupe de ressources.

Pour en savoir plus, voir [Kit de développement logiciel (SDK) Microsoft Azure version 2.6 pour Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).

### <a name="azure-powershell-080-or-later"></a>Microsoft Azure PowerShell 0.8.0 ou plus
Depuis la version 0.8.0,, hello installation d’Azure PowerShell inclut un module du Gestionnaire de ressources Azure hello dans Ajout toohello module Azure. Ce nouveau module vous permet de déploiement de hello tooscript des groupes de ressources.

Pour en savoir plus, voir [Utilisation d’Azure PowerShell avec le Gestionnaire de ressources Azure](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Azure Resource Explorer
Cela [outil Aperçu](https://resources.azure.com) vous permet de définitions de JSON hello tooexplore de tous les groupes de ressources hello dans votre abonnement et hello des ressources individuelles. Dans l’outil de hello, vous pouvez modifier des définitions de JSON hello d’une ressource, supprimer un ensemble de la hiérarchie des ressources et créer des ressources.  informations Hello disponibles dans cet outil sont très utiles pour la création de modèle, car elle vous indique ce que vous devez tooset pour un type particulier de ressource, hello de propriétés corriger les valeurs, etc.. Vous pouvez même créer votre groupe de ressources Bonjour [Azure Portal](https://portal.azure.com/), puis vérifiez que ses définitions de JSON dans hello explorer outil toohelp vous modéliser le groupe de ressources hello.

### <a name="deploy-tooazure-button"></a>TooAzure bouton déployer
Si vous utilisez GitHub pour le contrôle de code source, vous pouvez placer un [déployer tooAzure bouton](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) dans votre fichier Lisez-moi. MD, ce qui permet une tooAzure de l’interface utilisateur du déploiement de clés en main. Pendant que vous pouvez le faire pour n’importe quelle application web simple, vous pouvez étendre cette tooenable déploiement d’un groupe de ressources entière en plaçant un fichier azuredeploy.json dans la racine du référentiel hello. Ce fichier JSON, qui contient le modèle de groupe de ressources hello, sera utilisé par groupe de ressources hello déployer tooAzure bouton toocreate hello. Pour obtenir un exemple, consultez hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) exemple, que vous utiliserez dans ce didacticiel.

## <a name="get-hello-sample-resource-group-template"></a>Obtenir le modèle de groupe de ressources exemple hello
Passons tooit droite maintenant.

1. Accédez toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) exemple de Service d’applications.
2. Dans readme.md, cliquez sur **déployer tooAzure**.
3. Vous êtes dirigé toohello [à déployer sur azure](https://deploy.azure.com) site et les paramètres de déploiement tooinput posées. Notez que la plupart des champs de hello est renseignée avec le nom du référentiel hello et certaines chaînes aléatoires pour vous. Vous pouvez modifier tous les champs hello si vous le souhaitez, mais hello uniquement choses tooenter connexion d’administration de SQL Server hello et mot de passe de hello, puis cliquez sur **suivant**.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. Ensuite, cliquez sur **déployer** processus de déploiement toostart hello. Une fois le processus de hello exécute toocompletion, cliquez sur hello http://todoapp*XXXX*. hello de toobrowse azurewebsites.net lien déployé l’application. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   Hello UI serait un peu lent lorsque vous parcourez d’abord tooit car hello applications sont en cours de démarrage, mais vous inciter à qu’il s’agit d’une application entièrement fonctionnelle.
5. Dans la page de déploiement hello, cliquez sur hello **gérer** lien toosee hello nouvelle application Bonjour portail Azure.
6. Bonjour **Essentials** liste déroulante, cliquez sur le lien de groupe de ressources hello. Notez également que l’application hello web est déjà connecté référentiel GitHub de toohello sous **projet externe**. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. Dans le panneau des ressources de groupe hello, notez qu’il existe déjà deux applications web et une base de données SQL dans un groupe de ressources hello.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

Tout ce que vous venez de voir dans quelques minutes est une application entièrement déployé deux-microservice, avec tous les composants de hello, dépendances, paramètres, de base de données et publication continue, définie par une orchestration automatisée dans Azure Resource Manager. Tout cela a été possible grâce à deux éléments :

* bouton de tooAzure Hello déployer
* azuredeploy.JSON dans la racine du dépôt hello

Vous pouvez déployer cette application même des dizaines, des centaines voire des milliers de fois et avoir hello exacte même configuration chaque fois. prévisibilité de répétabilité et hello Hello de cette approche vous permet des applications à grande échelle toodeploy avec facilité et en toute confiance.

## <a name="examine-or-edit-azuredeployjson"></a>Examiner ou modifier le fichier AZUREDEPLOY.JSON
Maintenant nous allons voir comment référentiel GitHub de hello a été configuré. Vous utiliserez l’éditeur JSON hello Bonjour Azure .NET SDK, donc si vous n’avez pas déjà installé [Azure .NET SDK 2.6](/downloads/), faites-le maintenant.

1. Hello du clone [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) référentiel à l’aide de votre outil préféré git. Dans la capture d’écran de hello ci-dessous, je fais cela Bonjour Team Explorer dans Visual Studio 2013.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. À partir de la racine du référentiel hello, ouvrez azuredeploy.json dans Visual Studio. Si vous ne voyez pas volet Structure JSON de hello, vous devez tooinstall Azure .NET SDK.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

Je ne suis pas continu toodescribe tous les détails du format JSON de hello, mais hello [plus de ressources](#resources) section comprend des liens pour apprendre le langage de modèle de groupe de ressources hello. Ici, je vais juste tooshow vous hello intéressant de fonctionnalités qui peuvent vous aider à démarrer dans la création de votre propre modèle personnalisé pour le déploiement de l’application.

### <a name="parameters"></a>Paramètres
Examinons hello paramètres section toosee que la plupart de ces paramètres est le hello **déployer tooAzure** bouton vous invite tooinput. site Hello derrière hello **déployer tooAzure** bouton remplit hello entrée l’interface utilisateur à l’aide de paramètres de hello définis dans azuredeploy.json. Ces paramètres sont utilisés dans l’ensemble de définitions de ressource hello, telles que les noms de ressources, les valeurs de propriété, etc..

### <a name="resources"></a>Ressources
Dans le nœud de ressources hello, vous pouvez voir que les ressources de niveau supérieur 4 sont définies, notamment une instance de SQL Server, un plan App Service et les deux applications web. 

#### <a name="app-service-plan"></a>Plan App Service
Commençons par une ressource de niveau racine simple Bonjour JSON. Bonjour structure JSON, cliquez sur le plan de Service de l’application hello nommé **[hostingPlanName]** toohighlight hello code JSON correspondant. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

Notez que hello `type` élément spécifie la chaîne hello pour un plan App Service (elle a été appelée une batterie de serveurs fois long, long il y a), et d’autres éléments et propriétés sont renseignées à l’aide de paramètres hello définis dans le fichier JSON de hello cette ressource n’est pas toutes les ressources imbriquées.

> [!NOTE]
> Notez également que hello de `apiVersion` indique à Azure, version de définition ressource hello API REST toouse hello JSON avec et il peut affecter la façon dont les ressources hello doivent être formatés à l’intérieur de hello `{}`. 
> 
> 

#### <a name="sql-server"></a>SQL Server
Ensuite, cliquez sur les ressources de SQL Server hello nommé **SQLServer** Bonjour structure JSON.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

Hello Remarque suivant sur hello mis en surbrillance le code JSON :

* utilisation Hello de paramètres garantit hello créé sont nommés et des ressources configurées de manière à ce qui les rend cohérent avec l’autre.
* Hello SQLServer ressources a deux ressources imbriquées, chacune une valeur différente pour `type`.
* Hello imbriqués de ressources à l’intérieur de `“resources”: […]`, où la base de données hello et règles de pare-feu hello sont définis, ont un `dependsOn` élément qui spécifie l’ID de ressource de hello de ressources de SQL Server au niveau racine hello. Cela indique à Azure Resource Manager, « avant de créer cette ressource, qui doit exister d’autres ressources ; Si cet autre ressource est définie dans le modèle de hello, puis créez un tout d’abord ».
  
  > [!NOTE]
  > Pour plus d’informations sur la façon de toouse hello `resourceId()` , consultez [fonctions de modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).
  > 
  > 
* Hello effet Hello `dependsOn` élément est que Azure Resource Manager peut connaître les ressources qui peuvent être créés en parallèle et les ressources qui doivent être créés de façon séquentielle. 

#### <a name="web-app"></a>Application web
À présent, intéressons-nous toohello réel applications web eux-mêmes, qui sont plus complexes. Cliquez sur application web hello [variables('apiSiteName')] hello structure JSON toohighlight son code JSON. Vous pouvez constater que cela devient nettement plus intéressant. Pour cela, je vous parlerai de fonctionnalités de hello un par un :

##### <a name="root-resource"></a>Ressource racine
l’application Hello web dépend de deux ressources différentes. Cela signifie que Azure Resource Manager créera hello web application uniquement après les deux hello hello instance SQL Server et un plan App Service sont créés.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>Paramètres de l’application
paramètres de l’application Hello sont également définis comme une ressource imbriquée.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

Bonjour `properties` élément `config/appsettings`, vous avez deux paramètres de l’application au format de hello `“<name>” : “<value>”`.

* `PROJECT`est un [paramètre de KUDU](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) qui indique à déploiement d’Azure qui toouse de projet dans une solution Visual Studio à projets multiples. Je vous montrerai ultérieurement la configuration de contrôle de code source, mais puisque hello ToDoApp code est dans une solution Visual Studio à projets multiples, nous avons besoin de ce paramètre.
* `clientUrl`est simplement une application définissant ce code de l’application hello utilise.

##### <a name="connection-strings"></a>Chaînes de connexion
chaînes de connexion Hello sont également définis comme une ressource imbriquée.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

Bonjour `properties` élément `config/connectionstrings`, chaque chaîne de connexion est également définie comme une paire nom-valeur, avec format spécifique de hello de `“<name>” : {“value”: “…”, “type”: “…”}`. Pourquoi `type` élément, les valeurs possibles sont `MySql`, `SQLServer`, `SQLAzure`, et `Custom`.

> [!TIP]
> Pour obtenir une liste définitive des types de chaîne de connexion hello, exécutez hello commande dans Azure PowerShell suivante : \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>Contrôle de code source
paramètres de contrôle de source de Hello sont également définis comme une ressource imbriquée. Le Gestionnaire de ressources Azure utilise cette ressource tooconfigure continue la publication (consultez garde sur `IsManualIntegration` ultérieurement) et également tookick off déploiement hello du code d’application automatiquement lors du traitement de hello du fichier JSON de hello.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`et `branch` doit être très intuitive et doit pointer le nom de référentiel et hello de Git de toopublish de branche hello de toohello. Là encore, ces éléments sont définis par les paramètres d’entrée. 

Remarque Bonjour `dependsOn` élément qui, dans Ajout toohello web des ressources d’application lui-même, `sourcecontrols/web` dépend également `config/appsettings` et `config/connectionstrings`. Il s’agit, car une fois que `sourcecontrols/web` est configuré, hello processus de déploiement Azure tentera automatiquement toodeploy, générer et démarrer le code de l’application hello. Par conséquent, insertion de cette aide de dépendance pour vous assurer cette application hello a accès aux paramètres de l’application toohello requises et les chaînes de connexion avant l’exécution de code de l’application hello. 

> [!NOTE]
> Notez également que `IsManualIntegration` est défini trop`true`. Cette propriété est nécessaire dans ce didacticiel, car vous ne possédez pas réellement le référentiel GitHub de hello et par conséquent ne peut pas réellement accorder l’autorisation tooAzure tooconfigure publication en continu à partir de [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (c'est-à-dire push automatique tooAzure de mises à jour du référentiel). Vous pouvez utiliser la valeur par défaut de hello `false` du référentiel spécifié de hello uniquement si vous avez configuré des informations d’identification de GitHub du propriétaire hello Bonjour [portail Azure](https://portal.azure.com/) avant. En d’autres termes, si vous avez configuré tooGitHub de contrôle de code source ou BitBucket pour n’importe quelle application Bonjour [portail Azure](https://portal.azure.com/) précédemment, à l’aide de l’utilisateur des informations d’identification, puis Windows Azure n’oubliez pas d’informations d’identification hello et les utiliser à chaque fois que vous déployez une application GitHub ou BitBucket Bonjour futures. Toutefois, si vous n’avez pas encore fait, déploiement de modèle de JSON hello échoue quand Azure Resource Manager tente de paramètres de contrôle de source de l’application web tooconfigure hello, car il ne peut pas se connecter à GitHub ou BitBucket avec les informations d’identification du propriétaire du référentiel hello.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>Comparer le modèle JSON hello avec le groupe de ressources déployées
Ici, vous pouvez faire défiler les panneaux de l’application de tous les hello web Bonjour [Azure Portal](https://portal.azure.com/), mais il existe un autre outil qui est tout aussi utile, si de pas plus d’informations. Accédez toohello [Explorateur de ressources Azure](https://resources.azure.com) outil Aperçu, ce qui permet une représentation JSON de tous les groupes de ressources hello dans vos abonnements, tels qu’ils existent réellement Bonjour Azure principal. Vous pouvez également voir comment hiérarchie JSON du groupe de ressources hello dans Azure correspond à la hiérarchie de hello dans le fichier de modèle de hello qui a utilisé toocreate il.

Par exemple, lorsque vous accédez toohello [Explorateur de ressources Azure](https://resources.azure.com) outil et développez les nœuds dans l’Explorateur de hello Bonjour, je peux voir le groupe de ressources hello et ressources de niveau racine hello qui sont collectées sous leurs types de ressources respectives.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

Si vous consultez tooa l’application web, vous devez être en mesure de toosee web application configuration détails de toohello de similaire capture d’écran ci-dessous :

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

Là encore, hello ressources imbriquées doivent avoir un toothose très similaires de hiérarchie dans votre fichier de modèle JSON, et vous devez voir les paramètres de l’application hello, les chaînes de connexion, etc., correctement reflétées dans le volet JSON hello. absence de Hello de paramètres ici peut indiquer un problème avec votre fichier JSON et peut vous aider à résoudre les problèmes de votre fichier de modèle JSON.

## <a name="deploy-hello-resource-group-template-yourself"></a>Déploiement de modèle de groupe de ressources hello
Hello **déployer tooAzure** bouton est très utile, mais il vous permet de modèle de groupe de ressources toodeploy hello dans azuredeploy.json uniquement si vous avez déjà poussé azuredeploy.json tooGitHub. Hello Kit de développement .NET Azure fournit également des outils de hello pour vous toodeploy un fichier de modèle JSON directement à partir de votre ordinateur local. toodo, suit hello suivantes :

1. Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.
2. Cliquez sur **Visual C#** > **Cloud** > **Groupe de ressources Azure**, puis cliquez sur **OK**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. Dans **Sélectionner un modèle Azure**, choisissez **Modèle vide** et cliquez sur **OK**.
4. Faire glisser azuredeploy.json hello **modèle** dossier de votre nouveau projet.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. À partir de l’Explorateur de solutions, ouvrez hello copié azuredeploy.json.
6. Uniquement par souci de hello de démonstration de hello, nous allons ajouter certains standard Application Insight tooour JSON fichier de ressources en cliquant sur **ajouter une ressource**. Si vous êtes simplement intéressé de déploiement du fichier JSON de hello, ignorer toohello déployer comme suit.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. Sélectionnez **Application Insights pour les applications web**, puis assurez-vous qu’un plan App Service existant et une application web sont sélectionnés, puis cliquez sur **Ajouter**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   Vous devez maintenant être en mesure de toosee de nouvelles ressources que, selon les ressources hello et ce qu’il fait, ont des dépendances sur l’application web de plan ou hello App Service hello. Ces ressources ne sont pas activées par leur définition existante et que vous allez toochange qui.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. Bonjour structure JSON, cliquez sur **appInsights mise à l’échelle** toohighlight son code JSON. Il s’agit de hello mise à l’échelle de paramètre pour votre plan App Service.
9. Dans l’hello code JSON en surbrillance, recherchez hello `location` et `enabled` propriétés et de les définir comme indiqué ci-dessous.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. Bonjour structure JSON, cliquez sur **CPUHigh appInsights** toohighlight son code JSON. Il s’agit d’une alerte.
11. Recherchez hello `location` et `isEnabled` propriétés et de les définir comme indiqué ci-dessous. Hello même hello pour les autres trois alertes (ampoules violets).
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. Vous êtes maintenant prêt toodeploy. Droit hello projet, puis sélectionnez **déployer** > **nouveau déploiement**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. Le cas échéant, connectez-vous à votre compte Microsoft Azure.
14. Sélectionnez un groupe de ressources dans votre abonnement ou créez-en un nouveau, sélectionnez **azuredeploy.json**, puis cliquez sur **Modifier les paramètres**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    Vous allez maintenant être tooedit en mesure de tous les paramètres de hello définis dans le fichier de modèle hello dans une table complète. Les paramètres qui définissent des valeurs par défaut présentent déjà des valeurs par défaut, et ceux qui définissent une liste de valeurs autorisées s’affichent en tant que listes déroulantes.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. Renseignez tous les paramètres vide hello et utilisez hello [adresse référentiel GitHub ToDoApp](https://github.com/azure-appservice-samples/ToDoApp.git) dans **repoUrl**. Ensuite, cliquez sur **Enregistrer**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > Échelle automatique est une fonctionnalité proposée dans **Standard** niveau ou supérieure et au niveau du plan les alertes sont les fonctionnalités offertes par les **base** niveau ou une version ultérieure, vous devez tooset hello **référence (SKU)** paramètre trop**Standard** ou **Premium** commander toosee toutes les votre nouvelle application Insights ressources allument.
    > 
    > 
16. Cliquez sur **Déployer**. Si vous avez sélectionné **enregistrer les mots de passe**, mot de passe hello est enregistré dans le fichier de paramètres hello **en texte brut**. Dans le cas contraire, vous êtes invité mot de passe de base de données tooinput hello pendant le processus de déploiement hello.

Et voilà ! Maintenant vous devez simplement toogo toohello [Azure Portal](https://portal.azure.com/) et hello [Explorateur de ressources Azure](https://resources.azure.com) outil toosee hello nouvelles alertes et des paramètres de la mise à l’échelle ajoutés tooyour JSON déployé l’application.

Les étapes de cette section effectue principalement suivant de hello :

1. Fichier de modèle hello préparée
2. Créé un toogo de fichier de paramètres avec le fichier de modèle hello
3. Fichier de modèle hello déployé avec le fichier de paramètres hello

dernière étape de Hello est facilement effectué par une applet de commande PowerShell. toosee ce que fait Visual Studio lors du déploiement de votre application, ouvrez Scripts\Deploy-azureresourcegroup.ps1. Il y a beaucoup de code, mais je vais juste toohighlight tout code hello pertinentes vous avez besoin de fichier de modèle hello toodeploy avec le fichier de paramètres hello.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

Hello dernière applet de commande, `New-AzureResourceGroup`, est hello qui effectue les actions hello. Tout cela doit montrer tooyou, avec l’aide de hello d’outils, il est relativement simple toodeploy votre application de cloud computing comme prévu. Chaque fois que vous exécutez l’applet de commande hello sur hello même modèle avec hello même fichier de paramètres, vous allez tooget hello même résultat.

## <a name="summary"></a>Résumé
Dans DevOps, répétabilité et la prévisibilité sont des clés tooany réussir le déploiement d’une application à grande échelle composé de microservices. Dans ce didacticiel, vous avez déployé un tooAzure d’application deux-microservice en tant qu’un seul groupe de ressources à l’aide du modèle de gestionnaire de ressources Azure hello. Heureusement, il vous a donné hello connaissances que vous avez besoin dans toostart commande consiste à convertir votre application dans Azure dans un modèle et pouvez configurer et déployer de manière prévisible. 

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment trop[appliquer les méthodologies agiles et en permanence publier votre application microservices avec facilité](app-service-agile-software-development.md) et gestion avancée des techniques de déploiement comme [version d’évaluation de déploiement](app-service-web-test-in-production-controlled-test-flight.md) facilement.

<a name="resources"></a>

## <a name="more-resources"></a>Autres ressources
* [Langue du modèle Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [Fonctions des modèles Azure Resource Manager](../azure-resource-manager/resource-group-template-functions.md)
* [Déploiement d’une application avec un modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)
* [Utilisation d’Azure PowerShell avec Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Résolution des problèmes liés aux déploiements de groupes de ressources dans Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md)

