---
title: "aaaAzure outils de ligne de commande multiplateforme basée sur le Gestionnaire de ressources pour l’application Web de Azure | Documents Microsoft"
description: "Découvrez comment toouse hello nouveaux outils de ligne de commande multiplateforme basée sur Azure Resource Manager toomanage vos applications Web Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Utilisation de l’interface de ligne de commande XPlat basée sur Azure Resource Manager pour Azure App Service
> [!div class="op_single_selector"]
> * [Interface de ligne de commande Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Avec la version hello de version des outils de ligne de commande de Microsoft Azure inter-plateformes 0.10.5, les nouvelles commandes ont été ajoutés. Ces commandes permettent de hello utilisateur hello capacité toouse basée sur le Gestionnaire de ressources Azure de PowerShell commandes toomanage du Service d’applications.

toolearn sur la gestion des groupes de ressources, consultez [utiliser hello CLI d’Azure toomanage Azure ressources et groupes de ressources](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> En outre, tester les [Azure CLI 2.0](https://github.com/Azure/azure-cli), une interface CLI de nouvelle génération écrit dans Python pour le modèle de déploiement de gestion de ressources hello.
>
>

## <a name="managing-app-service-plans"></a>Gestion des plans App Service
### <a name="create-an-app-service-plan"></a>Créer un plan App Service
toocreate un plan app service, utilisez hello **appserviceplan azure créer** commande.

Voici les descriptions des paramètres différents de hello :

* **: groupe de ressources**: groupe de ressources qui inclut le plan de service d’application hello nouvellement créé.
* **--nom**: nom du plan de service d’application hello.
* **--location** : emplacement du plan App Service.
* **--référence (SKU)**: hello souhaité tarification sku (hello options sont : F1 (Free). D1 (Partagé). B1 (De base, petit), B2 (De base, moyen) et B3 (De base, grand). S1 (Standard, petit), S2 (Standard, moyen) et S3 (Standard, grand). P1 (Premium, petit), P2 (Premium, moyen) et P3 (Premium, grand).)
* **--instances**: hello du nombre de threads de travail dans le plan de service d’application hello (valeur par défaut est 1).

Exemple toouse cette applet de commande :

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Créer un plan App Service Linux

À l’aide de hello même **appserviceplan azure créer** commande par hello paramètre supplémentaire **--islinux true**. Notez les restrictions hello et décrites dans les régions [Introduction tooApp Service sur Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Répertorier les plans App Service existants
toolist hello app service place, utilisez **appserviceplan azure liste** commande.

toolist tous les plans de service d’application sous un groupe de ressources spécifique, utilisez :

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

tooget un plan de service d’application spécifique, utilisez **appserviceplan azure afficher** commande :

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Configurer un plan App Service existant
toochange hello paramètres d’un plan app service existant, utilisez hello **appserviceplan azure config** commande. Vous pouvez modifier hello référence (SKU) et le nombre de traitements hello 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Mise à l’échelle d’un plan App Service
tooscale une existante du Plan App Service, utilisez :

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>La modification hello référence (SKU) d’un Plan App Service
toochange hello référence (SKU) d’un existant du Plan App Service, utilisez :

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Supprimer un plan App Service existant
toodelete un plan de service d’application existant, assigné applications besoin toobe déplacés ou supprimés en premier. Puis à l’aide de hello **webapp azure supprimer** commande, vous pouvez supprimer le plan de service d’application hello.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Gestion des plans App Service
### <a name="create-a-web-app"></a>Créer une application web
toocreate une application web, utilisez hello **webapp azure créer** commande.

Voici les descriptions des paramètres différents de hello :

* **--nom**: nom de l’application web hello.
* **--plan**: nom de plan de service hello utilisé toohost hello web app.
* **: groupe de ressources**: groupe de ressources qui héberge le plan de service d’application hello.
* **--emplacement**: hello d’emplacement de l’application web.

Exemple toouse cette applet de commande :

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Supprimer une application existante
toodelete une application existante, vous pouvez utiliser hello **webapp azure supprimer** commande. Vous devez toospecify hello nom application hello et nom de groupe de ressources hello.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Répertorier les applications existantes
toolist hello les applications existantes, utilisez hello **webapp azure liste** commande.

toolist toutes les applications dans un groupe de ressources spécifique, utilisez :

    azure webapp list --resource-group ContosoAzureResourceGroup

tooget une application spécifique, utilisez hello **webapp azure afficher** commande.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Configurer une application existante
paramètres de hello toochange et configurations pour une application existante, utilisez hello **jeu de configuration azure webapp** commande.

Exemple (1) : modification de la version de php hello d’une application 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Exemple (2) : ajouter ou modifier les paramètres de l’application

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

tooknow autres que leur configuration peut être modifiée, utilisez hello **-h du jeu de configuration de l’application Web azure** commande.

### <a name="change-hello-state-of-an-existing-app"></a>Changement d’état d’une application existante hello
#### <a name="restart-an-app"></a>Redémarrer une application
toorestart une application, vous devez spécifier le groupe de hello nom et les ressources de l’application hello.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Arrêter une application
toostop une application, vous devez spécifier le groupe de hello nom et les ressources de l’application hello.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Démarrer une application
toostart une application, vous devez spécifier le groupe de hello nom et les ressources de l’application hello.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Gérer les profils de publication d’une application
Chaque application possède un profil de publication qui peut être utilisé toopublish votre code.

#### <a name="get-publishing-profile"></a>Obtenir le profil de publication
hello tooget profil pour une application, l’utilisation de publication :

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Cette commande renvoie hello de ligne de commande toohello nom d’utilisateur et mot de passe des profils de publication.

### <a name="manage-app-hostnames"></a>Gérer les noms d’hôte d’une application
liaisons de nom d’hôte toomanage pour votre application, utilisez hello **noms d’hôte de la configuration azure webapp** commande  

#### <a name="list-hostname-bindings"></a>Répertorier les liaisons de nom d’hôte
liaisons actuelles nom d’hôte tooget hello pour une application, utilisez :

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Ajouter des liaisons de noms d’hôte
tooadd nom d’hôte liaisons tooan l’application, utilisez :

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Supprimer des liaisons de noms d’hôte
liaisons de nom d’hôte toodelete, utilisez :

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la prise en charge d’Azure Resource Manager CLI, consultez [utiliser hello CLI d’Azure toomanage Azure ressources et groupes de ressources.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* toolearn sur la gestion du Service d’applications à l’aide de PowerShell, consultez [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)
* toolearn sur le Service d’applications Azure sur Linux, consultez [Introduction tooApp Service sur Linux](app-service-linux-intro.md)
