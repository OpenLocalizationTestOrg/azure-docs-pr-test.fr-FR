---
title: "métadonnées du Service API Apps aaaApp pour la génération de code et de découverte des API | Documents Microsoft"
description: "Découvrez l’utilisation de la génération de code et de découverte la toofacilitate API des métadonnées Swagger par les API Apps dans Azure App Service."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>Les métadonnées d’App Service API Apps pour la détection d’API et la création de code
La prise en charge des métadonnées d’API [Swagger 2.0](http://swagger.io/) est intégrée aux applications API App Service. Vous n’avez pas toouse Swagger, mais si vous l’utilisez, vous pouvez tirer parti des fonctionnalités d’applications API qui facilite la découverte et la consommation.   

## <a name="swagger-endpoint"></a>Point de terminaison Swagger
Vous pouvez spécifier un point de terminaison qui fournit des métadonnées Swagger le JSON 2.0 pour une application API dans une propriété de l’application d’API hello. point de terminaison de Hello permettre être des URL de base toohello relatif de l’application d’API hello ou une URL absolue. URL absolues peuvent pointer en dehors de l’application d’API hello. 

Nombre de clients en aval (par exemple, la génération de code Visual Studio et le flux de « Ajouter des API » PowerApps), hello URL doit être accessible publiquement (non protégé par un utilisateur ou l’authentification du service). Cela signifie que si vous utilisez l’authentification de Service de l’application et que vous souhaitez définition à partir de l’API tooexpose hello au sein de votre application elle-même, vous devez option d’authentification toouse qui autorise le trafic anonyme tooreach votre API. Pour plus d’informations, consultez la page [Authentification et autorisation pour les applications d’API dans Azure App Service](app-service-api-authentication.md).

### <a name="portal-blade"></a>Panneau du portail
Bonjour [portail Azure](https://portal.azure.com/) hello du point de terminaison URL peut être affiché et modifié sur hello **définition d’API** panneau.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Propriété d’Azure Resource Manager
Vous pouvez également configurer l’URL de la définition d’une application API hello API à l’aide de [l’Explorateur de ressources](https://resources.azure.com/) ou [modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) dans les outils de ligne de commande tels que [Azure PowerShell](/powershell/azureps-cmdlets-docs)et hello [CLI d’Azure](../cli-install-nodejs.md). 

Dans **l’Explorateur de ressources**, accédez trop**abonnements > {votre abonnement} > resourceGroups > {votre groupe de ressources} > fournisseurs > Microsoft.Web > sites > {votre site} > config > web**, et vous verrez hello `apiDefinition` propriété :

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Pour obtenir un exemple d’un modèle de gestionnaire de ressources Azure qui définit hello `apiDefinition` propriété, ouvrez hello [fichier azuredeploy.json Bonjour application d’exemple de liste de tâches](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Rechercher la section hello du modèle hello qui ressemble à l’exemple JSON hello indiqué ci-dessus.

### <a name="default-value"></a>Valeur par défaut
Lorsque vous utilisez Visual Studio toocreate une application API, point de terminaison hello API définition est automatiquement défini toohello les URL de base de l’application hello API plue `/swagger/docs/v1`. Il s’agit d’URL par défaut de hello que hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) package NuGet utilise les métadonnées de Swagger tooserve générée de façon dynamique pour un projet d’API Web ASP.NET. 

## <a name="code-generation"></a>Génération de code
Un des avantages de hello de l’intégration de Swagger dans les applications API Azure est la génération de code automatique. Classes de client généré vous code toowrite plus simple qui appelle une application API.

Vous pouvez générer du code client pour une application API à l’aide de Visual Studio ou à partir de la ligne de commande hello. Pour plus d’informations sur comment les classes dans Visual Studio toogenerate client pour un projet d’API Web ASP.NET, consultez [prise en main avec API Apps et ASP.NET](app-service-api-dotnet-get-started.md#codegen). Pour plus d’informations sur comment toodo à partir de la commande hello ligne pour toutes les langues prises en charge, consultez le fichier Lisez-moi hello hello [Azure/autorest](https://github.com/azure/autorest) référentiel sur GitHub.com.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir un didacticiel qui vous guide dans la création, le déploiement et l’utilisation d’une application API, consultez [Prise en main des applications API dans Azure App Service](app-service-api-dotnet-get-started.md).

Si vous utilisez la gestion des API Azure avec API Apps, vous pouvez utiliser tooimport de métadonnées Swagger votre API dans Gestion des API. Pour plus d’informations, consultez [comment tooimport hello définition d’une API avec les opérations de gestion des API Azure](../api-management/api-management-howto-import-api.md). 

