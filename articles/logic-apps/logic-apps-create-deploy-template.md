---
title: "aaaCreate des modèles de déploiement pour Azure Logic Apps | Documents Microsoft"
description: "Création de modèles Azure Resource Manager pour le déploiement d’applications logiques et la gestion des versions"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>Création de modèles pour le déploiement d’applications logiques et la gestion des versions

Après avoir créé une application logique, vous souhaiterez peut-être toocreate sous la forme d’un modèle Azure Resource Manager.
De cette manière, vous pouvez facilement déployer environnement de tooany application hello logique ou un groupe de ressources où vous en aurez besoin.
Pour en savoir plus sur les modèles Resource Manager, consultez les articles sur la [création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) et le [déploiement de ressources à l’aide de modèles Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="logic-app-deployment-template"></a>Modèle de déploiement de l’application logique

Une application logique possède trois composants de base :

* **Ressources d’application logique**: contient des informations sur les éléments tels que les prix de plan, l’emplacement et définition de workflow hello.
* **Définition de workflow**: décrit les étapes du flux de travail de votre application logique et comment moteur de Logic Apps hello doit exécuter les flux de travail hello.
Vous pouvez afficher cette définition dans la fenêtre **Mode Code** de votre application logique.
Dans la ressource application hello logique, vous pouvez trouver cette définition Bonjour `definition` propriété.
* **Connexions**: fait référence à des ressources tooseparate qui stockent les métadonnées relatives à toutes les connexions du connecteur, par exemple une chaîne de connexion et un jeton d’accès en toute sécurité.
Dans la ressource application hello logique, votre application logique fait référence à ces ressources Bonjour `parameters` section.

Vous pouvez afficher tous ces éléments pour les applications logiques existantes en utilisant un outil tel que [l’Explorateur de ressources Azure](http://resources.azure.com).

toomake un modèle pour un toouse application logique avec les déploiements de groupe de ressources, vous devez définir des ressources de hello et paramétrer en fonction des besoins.
Par exemple, si vous déployez un environnement de production, test et développement de tooa, vous préférerez certainement toouse connexion différentes chaînes tooa base de données SQL dans chaque environnement.
Ou bien, vous souhaiterez toodeploy dans différents abonnements ou les groupes de ressources.  

## <a name="create-a-logic-app-deployment-template"></a>Création d’un modèle de déploiement d’applications logiques

toohave de façon plus simple Hello un modèle de déploiement d’application logique valide est toouse le [Visual Studio Tools pour Logic Apps](logic-apps-deploy-from-vs.md).
outils de Visual Studio Hello génèrent un modèle de déploiement valide qui peut être utilisé sur n’importe quel abonnement ou l’emplacement.

Certains autres outils peuvent vous être utiles lorsque vous créez un modèle de déploiement d’application logique.
Vous pouvez créer manuellement, autrement dit, à l’aide de hello ressources déjà abordé ici toocreate paramètres en fonction des besoins.
Une autre option consiste à toouse un [créateur de modèle d’application logique](https://github.com/jeffhollan/LogicAppTemplateCreator) module PowerShell. Ce module open source évalue d’abord application logique de hello et toutes les connexions qu’il utilise et génère ensuite les ressources de modèle avec les paramètres nécessaires hello pour le déploiement.
Par exemple, si vous avez une application de logique qui reçoit un message d’une file d’attente Azure Service Bus et ajoute la base de données SQL Azure données tooan, outil de hello préserve toute la logique d’orchestration hello et adapte hello SQL et les chaînes de connexion de Service Bus afin qu’ils peuvent être définies au moment du déploiement.

> [!NOTE]
> Les connexions doivent être dans hello même groupe de ressources en tant qu’application logique de hello.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Installez le module PowerShell modèle hello logique application
le module Hello plus simple façon tooinstall hello est via hello [PowerShell Gallery](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), en utilisant la commande hello `Install-Module -Name LogicAppTemplate`.  

Module PowerShell de hello peut s’installer également pas manuellement :

1. Télécharger la version la plus récente de hello hello [créateur de modèle d’application logique](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).  
2. Extraire le dossier hello dans votre dossier de module PowerShell (généralement `%UserProfile%\Documents\WindowsPowerShell\Modules`).

Pour toowork de module hello avec l’accès client et d’abonnement jeton, nous vous recommandons d’utiliser il avec hello [ARMClient](https://github.com/projectkudu/ARMClient) outil de ligne de commande.  Ce [billet de blog ](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) présente ARMClient de façon plus détaillée.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>Générer un modèle d’application logique à l’aide de PowerShell
Une fois que PowerShell est installé, vous pouvez générer un modèle à l’aide de hello de commande suivante :

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`est l’ID d’abonnement Azure hello. Cette ligne obtient d’abord un accès jeton via ARMClient, puis il dirige via toohello script PowerShell, puis crée le modèle de hello dans un fichier JSON.

## <a name="add-parameters-tooa-logic-app-template"></a>Ajouter le modèle d’application de paramètres tooa logique
Après avoir créé votre modèle d’application logique, vous pouvez continuer tooadd ou modifier les paramètres que vous devrez peut-être. Par exemple, si votre définition inclut un ID de ressource tooan fonction Azure ou d’un workflow imbriqué que vous envisagez de toodeploy dans un déploiement unique, vous pourrez ajouter un modèle de tooyour plusieurs ressources et paramétrer des ID en fonction des besoins. Hello va de même tooany références toocustom API Swagger points de terminaison ou vous attendez toodeploy avec chaque groupe de ressources.

## <a name="deploy-a-logic-app-template"></a>Déployer un modèle d’application logique

Vous pouvez déployer votre modèle à l’aide d’outils, tels que PowerShell, l’API REST, [Visual Studio Team Services Release Management](#team-services)et de déploiement de modèle via hello portail Azure.
En outre, les valeurs hello toostore des paramètres, nous vous recommandons de créer un [fichier de paramètres](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).
Découvrez comment trop[déployer des ressources avec PowerShell et les modèles Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) ou [déployer des ressources avec des modèles Azure Resource Manager et hello Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).

### <a name="authorize-oauth-connections"></a>Autoriser des connexions OAuth

Après le déploiement, application logique de hello fonctionne de bout en bout avec des paramètres valides.
Toutefois, vous devez toujours autoriser OAuth connexions toogenerate un jeton d’accès valide.
tooauthorize OAuth connexions, ouvrez l’application logique de hello Bonjour logique de concepteur d’applications et autoriser ces connexions. Ou, pour un déploiement automatisé, vous pouvez utiliser un tooeach de tooconsent script OAuth connexion.
Vous trouverez un exemple de script sur GitHub sous le projet [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) .

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services Release Management

Un scénario courant pour déployer et gérer un environnement est toouse un outil tel que de la gestion des versions dans Visual Studio Team Services avec un modèle de déploiement d’application logique. Visual Studio Team Services inclut un [déployer un groupe de ressources Azure](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) tâches que vous pouvez ajouter tooany build ou libérer le pipeline. Vous devez toohave une [principal du service](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) pour l’autorisation toodeploy et que vous pouvez générer définition de la version hello.

1. Dans Release Management, sélectionnez **Vide** pour créer une définition vide.

    ![Créer une définition vide][1]

2. Choisissez le processus de génération de toutes les ressources que vous avez besoin pour cet, probablement notamment hello logique modèle d’application généré manuellement ou en tant que partie de hello.
3. Ajoutez une tâche de **déploiement d’un groupe de ressources Azure** .
4. Configurer avec un [principal du service](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)et référencer des fichiers de modèle et les paramètres de modèle hello.
5. Continuer toobuild étapes dans le processus de mise en production hello pour tout autre environnement, de tests automatisés ou les approbateurs en fonction des besoins.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
