---
title: "commandes d’aaaAzure basée sur le Gestionnaire de ressources de PowerShell pour l’application Web de Azure | Documents Microsoft"
description: "Découvrez comment toouse hello nouvelle toomanage de commandes PowerShell de basée sur le Gestionnaire de ressources Azure, vos applications Web Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>À l’aide de PowerShell de Azure Resource Manager-Based tooManage Azure Web Apps
> [!div class="op_single_selector"]
> * [Interface de ligne de commande Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Avec Microsoft Azure PowerShell version 1.0.0 nouvelles commandes ont été ajoutés, qui donnent hello utilisateur hello capacité toouse basée sur le Gestionnaire de ressources Azure de PowerShell commandes toomanage les applications Web.

toolearn sur la gestion des groupes de ressources, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md). 

toolearn sur la liste complète des paramètres et des options pour les applets de commande PowerShell de hello hello voir hello [complète la référence d’applet de commande de basée sur le Web application Azure Resource Manager des PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Gestion des plans App Service
### <a name="create-an-app-service-plan"></a>Créer un plan App Service
toocreate un plan app service, utilisez hello **New-AzureRmAppServicePlan** applet de commande.

Voici les descriptions des paramètres différents de hello :

* **Nom**: nom du plan de service d’application hello.
* **Location**: emplacement du plan de service.
* **ResourceGroupName**: groupe de ressources qui inclut le plan de service d’application hello nouvellement créé.
* **Couche**: hello souhaité niveau tarifaire (valeur par défaut est libre, les autres options sont Shared, Basic, Standard et Premium.)
* **WorkerSize**: hello taille des travailleurs (valeur par défaut est petit, si le paramètre de niveau hello a été spécifié comme base, Standard ou Premium. Les autres options sont Moyen et Grand.)
* **La valeur NumberofWorkers**: hello du nombre de threads de travail dans le plan de service d’application hello (valeur par défaut est 1). 

Exemple toouse cette applet de commande :

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Création d’un plan App Service dans un environnement App Service
planification d’un service d’application toocreate dans un environnement app service, utilisez hello même commande **New-AzureRmAppServicePlan** avec le nom de hello toospecify de paramètres supplémentaires de ASE et le nom de groupe de ressources de ASE.

Exemple toouse cette applet de commande :

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

toolearn plus en détail l’environnement app service, vérification [Introduction tooApp environnement de Service](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Répertorier les plans App Service existants
toolist hello app service place, utilisez **Get-AzureRmAppServicePlan** applet de commande.

toolist tous les plans de service d’application sous votre abonnement, utilisez : 

    Get-AzureRmAppServicePlan

toolist tous les plans de service d’application sous un groupe de ressources spécifique, utilisez :

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget un plan de service d’application spécifique, utilisez :

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Configurer un plan App Service existant
toochange hello paramètres d’un plan app service existant, utilisez hello **Set-AzureRmAppServicePlan** applet de commande. Vous pouvez modifier le niveau de hello, la taille du travail et le nombre de traitements hello 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Mise à l’échelle d’un plan App Service
tooscale une existante du Plan App Service, utilisez :

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Modification de la taille du travail hello d’un Plan App Service
taille de hello toochange des travailleurs dans une existante du Plan App Service, utilisez :

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>La modification hello niveau d’un Plan App Service
couche de hello toochange d’une existante du Plan App Service, utilisez :

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Supprimer un plan App Service existant
toodelete un plan de service d’application existant, assigné web applications besoin toobe déplacés ou supprimés en premier. Puis à l’aide de hello **Remove-AzureRmAppServicePlan** vous pouvez supprimer le plan de service d’application hello applet de commande.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Gestion d’App Service Web Apps
### <a name="create-a-web-app"></a>Créer une application web
toocreate une application web, utilisez hello **New-AzureRmWebApp** applet de commande.

Voici les descriptions des paramètres différents de hello :

* **Nom**: nom de l’application web hello.
* **AppServicePlan**: nom de plan de service hello utilisé toohost hello web app.
* **ResourceGroupName**: groupe de ressources qui héberge le plan de service d’application hello.
* **Emplacement**: hello d’emplacement de l’application web.

Exemple toouse cette applet de commande :

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Créer une application web dans un environnement App Service
toocreate une application web dans un environnement de Service de l’application (ASE). Utilisez hello même **New-AzureRmWebApp** avec le nom de paramètres supplémentaires toospecify hello ASE et nom de groupe de ressources hello hello ASE appartient à.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

toolearn plus en détail l’environnement app service, vérification [Introduction tooApp environnement de Service](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Supprimer une application web existante
toodelete une application web existante, vous pouvez utiliser hello **Remove-AzureRmWebApp** applet de commande, vous devez toospecify hello nom hello web app et nom de groupe de ressources hello.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Répertorier les applications web existantes
toolist hello des applications web existantes, utilisez hello **Get-AzureRmWebApp** applet de commande.

toolist toutes les applications web sous votre abonnement, utilisez :

    Get-AzureRmWebApp

toolist toutes les applications web sous un groupe de ressources spécifique, utilisez :

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget une application web spécifique, utilisez :

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Configurer une application web existante
paramètres de hello toochange et configurations pour une application web existante, utilisez hello **Set-AzureRmWebApp** applet de commande. Pour obtenir une liste complète des paramètres, consultez hello [lien de référence d’applet de commande](https://msdn.microsoft.com/library/mt652487.aspx)

Exemple (1) : utilisez cette applet de commande toochange les chaînes de connexion

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Exemple (2) : ajouter ou modifier les paramètres de l’application

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


Exemple (3) : set hello web application toorun en mode 64 bits

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Changement d’état d’une application Web existante hello
#### <a name="restart-a-web-app"></a>Redémarrer une application web
toorestart une application web, vous devez spécifier hello nom ressource groupe et de l’application web hello.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Arrêter une application web
toostop une application web, vous devez spécifier hello nom ressource groupe et de l’application web hello.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Démarrer une application web
toostart une application web, vous devez spécifier hello nom ressource groupe et de l’application web hello.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Gérer les profils de publication Web Apps
Chaque application web a un profil de publication qui peut être utilisé toopublish vos applications, plusieurs opérations peuvent être exécutées sur les profils de publication.

#### <a name="get-publishing-profile"></a>Obtenir le profil de publication
hello tooget publication profil pour une application web, utilisez :

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Cette commande renvoie hello publication de ligne de commande toohello profil ainsi hello publication profil tooa texte fichier de sortie.

#### <a name="reset-publishing-profile"></a>Réinitialiser le profil de publication
tooreset à la fois hello mot de passe de publication pour FTP et web deploy pour une application web, utilisez :

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Gérer les certificats d’application web
toolearn sur comment toomanage web des certificats de l’application, consultez [liaison de certificats SSL à l’aide de PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Étapes suivantes
* toolearn sur la prise en charge du Gestionnaire de ressources de Azure PowerShell, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager.](../powershell-azure-resource-manager.md)
* toolearn sur les environnements de Service d’application, consultez [Introduction tooApp environnement de Service.](app-service-app-service-environment-intro.md)
* toolearn sur la gestion des certificats SSL de Service d’application à l’aide de PowerShell, consultez [liaison de certificats SSL à l’aide de PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* toolearn sur la liste complète des applets de commande PowerShell de basée sur Azure Resource Manager pour les applications Web Azure, hello consultez [référence d’applet de commande Azure de PowerShell Cmdlets de Web Apps Azure Resource Manager.](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn sur la gestion du Service d’applications à l’aide de la CLI, consultez [Using Azure Resource Manager-Based XPlat CLI pour l’application Web Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)

