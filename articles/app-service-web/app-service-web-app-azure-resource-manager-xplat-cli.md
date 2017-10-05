---
title: "Outils en ligne de commande multiplateformes basés sur Azure Resource Manager pour Azure Web App | Microsoft Docs"
description: "Découvrez comment utiliser les nouveaux outils en ligne de commande multiplateformes basés sur Azure Resource Manager pour gérer vos applications Azure Web Apps."
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
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Utilisation de l’interface de ligne de commande XPlat basée sur Azure Resource Manager pour Azure App Service
> [!div class="op_single_selector"]
> * [Interface de ligne de commande Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

La version 0.10.5 des outils en ligne de commande multiplateformes Microsoft Azure comporte de nouvelles commandes. Ces commandes permettent à l’utilisateur de gérer App Service à l’aide de commandes PowerShell basées sur Azure Resource Manager.

Pour en savoir plus sur la gestion des groupes de ressources, voir [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md) (Utiliser l’interface de ligne de commande Azure pour gérer les ressources et les groupes de ressources Azure). 

> [!NOTE] 
> Essayez également [Azure CLI 2.0](https://github.com/Azure/azure-cli), une interface de ligne de commande nouvelle génération écrite en Python pour le modèle de déploiement Resource Manager.
>
>

## <a name="managing-app-service-plans"></a>Gestion des plans App Service
### <a name="create-an-app-service-plan"></a>Créer un plan App Service
Pour créer un plan App Service, utilisez la commande **azure appserviceplan create**.

Voici une description des différents paramètres :

* **--resource-group** : groupe de ressources contenant le nouveau plan App Service.
* **--name** : nom du plan App Service.
* **--location** : emplacement du plan App Service.
* **--sku** : SKU de tarification souhaité (Les options sont les suivantes : F1 (Gratuit). D1 (Partagé). B1 (De base, petit), B2 (De base, moyen) et B3 (De base, grand). S1 (Standard, petit), S2 (Standard, moyen) et S3 (Standard, grand). P1 (Premium, petit), P2 (Premium, moyen) et P3 (Premium, grand).)
* **--instances** : nombre de threads de travail dans le plan App Service (Valeur par défaut : 1).

Exemple d’utilisation de cette applet de commande :

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Créer un plan App Service Linux

En utilisant la même commande **azure appserviceplan create** avec le paramètre supplémentaire **--islinux true**. Consultez les restrictions et les régions décrites dans [Présentation d’App Service sur Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Répertorier les plans App Service existants
Pour répertorier les plans App Service existants, utilisez la commande **azure appserviceplan list**.

Pour répertorier tous les plans App Service associés à un groupe de ressources spécifique, utilisez :

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

Pour accéder à un plan App Service spécifique, utilisez la commande **azure appserviceplan show**.

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Configurer un plan App Service existant
Pour modifier les paramètres d’un plan App Service existant, utilisez la commande **azure appserviceplan config**. Vous pouvez modifier le SKU et le nombre de threads de travail. 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Mise à l’échelle d’un plan App Service
Pour mettre à l’échelle un plan App Service existant, utilisez :

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a>Modification du SKU d’un plan App Service
Pour modifier le SKU d’un plan App Service existant, utilisez :

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Supprimer un plan App Service existant
Pour supprimer un plan App Service existant, toutes les applications affectées doivent d’abord être déplacées ou supprimées. Ensuite, à l’aide de la commande **azure webapp delete**, vous pouvez supprimer le plan App Service.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Gestion des plans App Service
### <a name="create-a-web-app"></a>Créer une application web
Pour créer une application web, utilisez la commande **azure webapp create**.

Voici une description des différents paramètres :

* **--name** : nom de l’application web.
* **--plan** : nom du plan de service utilisé pour héberger l’application web.
* **--resource-group** : groupe de ressources qui héberge le plan App Service.
* **--location** : emplacement de l’application web.

Exemple d’utilisation de cette applet de commande :

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Supprimer une application existante
Pour supprimer une application existante, vous pouvez utiliser la commande **azure webapp delete**. Vous devez spécifier le nom de l’application et le nom du groupe de ressources.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Répertorier les applications existantes
Pour répertorier les applications existantes, utilisez la commande **azure webapp list**.

Pour répertorier toutes les applications dans un groupe de ressources spécifique, utilisez :

    azure webapp list --resource-group ContosoAzureResourceGroup

Pour accéder à une application spécifique, utilisez la commande **azure webapp show**.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Configurer une application existante
Pour modifier les paramètres et configurations d’une application existante, utilisez la commande **azure webapp config set**.

Exemple (1) : modifier la version php d’une application 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Exemple (2) : ajouter ou modifier les paramètres de l’application

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

Pour savoir quelle autre configuration peut être modifiée, utilisez la commande **azure webapp config set -h**.

### <a name="change-the-state-of-an-existing-app"></a>Modifier l’état d’une application existante
#### <a name="restart-an-app"></a>Redémarrer une application
Pour redémarrer une application, vous devez spécifier le nom et le groupe de ressources de cette application.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Arrêter une application
Pour arrêter une application, vous devez spécifier le nom et le groupe de ressources de cette application.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Démarrer une application
Pour démarrer une application, vous devez spécifier le nom et le groupe de ressources de cette application.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Gérer les profils de publication d’une application
Chaque application dispose d’un profil de publication qui peut être utilisé pour publier votre code.

#### <a name="get-publishing-profile"></a>Obtenir le profil de publication
Pour obtenir le profil de publication d’une application, utilisez :

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Cette commande renvoie le nom d’utilisateur et le mot de passe du profil de publication à la ligne de commande.

### <a name="manage-app-hostnames"></a>Gérer les noms d’hôte d’une application
Pour gérer les liaisons de nom d’hôte de votre application, utilisez la commande **azure webapp config hostnames**.  

#### <a name="list-hostname-bindings"></a>Répertorier les liaisons de nom d’hôte
Pour obtenir les liaisons de nom d’hôte actuelles pour une application, utilisez :

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Ajouter des liaisons de noms d’hôte
Pour ajouter des liaisons de noms d’hôte à une application, utilisez :

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Supprimer des liaisons de noms d’hôte
Pour supprimer des liaisons de noms d’hôte, utilisez :

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Étapes suivantes
* Pour en savoir plus sur la prise en charge de l’interface de ligne de commande Azure Resource Manager, voir [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md) (Utiliser l’interface de ligne de commande Azure pour gérer les ressources et les groupes de ressources Azure).
* Pour en savoir plus sur la gestion d’App Service à l’aide de PowerShell, voir [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps](app-service-web-app-azure-resource-manager-powershell.md) (Utilisation de PowerShell basé sur Azure Resource Manager pour gérer Azure Web Apps).
* Pour en savoir plus sur Azure App Service sur Linux, voir [Présentation d’App Service sur Linux](app-service-linux-intro.md)
