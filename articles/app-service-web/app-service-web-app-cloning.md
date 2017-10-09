---
title: "aaaWeb application clonage à l’aide de PowerShell"
description: "Découvrez comment tooclone vos applications Web de toonew les applications Web à l’aide de PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>Clonage de l’application Azure App Service à l’aide de PowerShell
Avec la version de hello de Microsoft Azure PowerShell version 1.1.0 une nouvelle option a été ajouté AzureRMWebApp tooNew qui donnerait hello utilisateur hello capacité tooclone une application existante tooa nouvellement créé d’application Web dans une autre région ou dans hello même région. Cela permet aux clients toodeploy un nombre d’applications sur différentes régions rapidement et facilement.

Le clonage d’application n’est actuellement pris en charge que pour les plans de service d’application de niveau Premium. nouvelles utilisations de fonctionnalité Hello hello même limitations en tant que fonctionnalité de sauvegarde des applications Web, consultez [sauvegardez une application web dans Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn sur l’utilisation du Gestionnaire de ressources Azure en fonction toomanage des applets de commande Azure PowerShell vérification de vos applications Web [Azure Resource Manager en fonction des commandes PowerShell pour l’application Web Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>Clonage d’une application existante
Scénario : Une application web existante dans la région Amérique du Sud, hello l’utilisateur souhaiterait tooclone hello contenu tooa nouvelle application web dans la région Amérique du Nord. Cela peut être accompli à l’aide de la version du Gestionnaire de ressources Azure hello de toocreate d’applet de commande PowerShell hello une application web avec l’option - SourceWebApp de hello.

Le fait de connaître les ressources hello nom du groupe qui contient la source de l’application web de hello, nous pouvons utiliser hello informations PowerShell commande tooget hello source application web (dans ce cas nommées webapp-source) suivantes :

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

toocreate un nouveau Plan App Service, nous pouvons utiliser la commande New-AzureRmAppServicePlan comme dans l’exemple suivant de hello

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

À l’aide de la commande hello AzureRmWebApp de nouveau, nous pouvons créer une application web hello dans la région de hello Amérique du Nord et comment lier il tooan couche premium existante du Plan App Service, en outre, nous pouvons utiliser hello même ressource de groupe en tant qu’application web de hello source, ou définir un nouveau groupe de ressources , suivant de hello montre que :

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

tooclone une application web existante, y compris tous les emplacements de déploiement associé, hello devra toouse hello IncludeSourceWebAppSlots paramètre, hello PowerShell commande suivante illustre l’utilisation de hello de ce paramètre avec hello New-AzureRmWebApp commande :

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

tooclone une application web existante dans hello même région, hello devra toocreate un groupe de ressources et d’un nouveau service d’application plan Bonjour même région, puis en utilisant hello suivants PowerShell commande tooclone hello web app

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Le clonage d’un tooan d’application existant environnement App Service
Scénario : Une application web existante dans la région Amérique du Sud, hello l’utilisateur souhaiterait tooclone hello contenu tooa nouveau web application tooan existant d’environnement de Service d’application (ASE).

Le fait de connaître les ressources hello nom du groupe qui contient la source de l’application web de hello, nous pouvons utiliser hello informations PowerShell commande tooget hello source application web (dans ce cas nommées webapp-source) suivantes :

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

Connaître le nom de hello ASE et nom de groupe de ressources hello hello ASE appartient à, utilisateur de hello pouvez utiliser la commande hello New-AzureRmWebApp toocreate hello application web dans ASE existant hello, hello suivant montre que :

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

paramètre d’emplacement Hello est nécessaire en raison de la raison de toolegacy, mais dans les cas de hello de création d’une application dans un environnement app service seront ignorés. 

## <a name="cloning-an-existing-app-slot"></a>Clonage d’un emplacement d’application existant
Scénario : hello aimerait tooclone une tooeither l’emplacement d’application Web existante une application Web ou un nouvel emplacement de l’application Web. Hello nouvelle application Web peut être Bonjour même région comme emplacement de l’application Web hello d’origine ou dans une autre région.

Le fait de connaître les ressources hello nom du groupe qui contient la source de l’application web de hello, nous pouvons utiliser hello commande PowerShell informations tooget hello source web application de l’emplacement (dans ce cas nommées source-webappslot) lié tooWeb application source-application Web suivante :

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

suivant de Hello illustre la création d’un clone de hello source web application tooa nouvelle application web :

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>Configuration de Traffic Manager lors du clonage d’une application
Créer des applications web de plusieurs régions et configurer Azure Traffic Manager tooroute trafic tooall ces applications web, est un tooinsure n scénarios importants qui les applications clients sont hautement disponibles, durant le clonage d’une application web existante, vous avez hello option tooconnect web applications tooeither un profil traffic manager nouveau ou existant - Notez que seul Azure Resource Manager la version de Traffic Manager est pris en charge.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>Création d’un profil Traffic Manager lors du clonage d’une application
Scénario : hello l’utilisateur souhaiterait tooclone une région de tooanother web app, lors de la configuration d’un profil de gestionnaire de ressources Azure traffic manager qui incluent les deux applications web. suivant de Hello illustre la création d’un clone de hello source web application tooa nouvelle application web lors de la configuration d’un nouveau profil Traffic Manager :

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>Ajout de nouveaux cloné Web App tooan profil Traffic Manager existant
Scénario : utilisateur de hello dispose déjà d’un profil traffic manager de Azure Resource Manager qu’il souhaite tooadd à la fois les applications en tant que points de terminaison web. toodo par conséquent, nous devons tooassemble hello existant id de profil traffic manager, nous devons id d’abonnement hello, nom de groupe de ressources et nom du profil hello existant traffic manager.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

Une fois que l’id de gestionnaire de trafic hello, suivant de hello illustre la création d’un clone de hello source web application tooa nouvelle application web lors de l’ajout de leur profil de Traffic Manager existant tooan :

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>Restrictions actuelles
Cette fonctionnalité est actuellement en version préliminaire, nous travaillons tooadd nouvelles fonctionnalités au fil du temps, hello suivant liste sont hello restrictions connues sur la version actuelle de hello au clonage de l’application :

* Les paramètres de mise à l’échelle automatique ne sont pas clonés.
* Les paramètres de planification de sauvegarde ne sont pas clonés.
* Les paramètres de réseau virtuel ne sont pas clonés.
* Application Insights ne sont pas automatiquement définies sur l’application web de destination hello
* Les paramètres d’authentification simple ne sont pas clonés.
* Les paramètres d’extension Kudu ne sont pas clonés.
* Les règles TiP ne sont pas clonées.
* Les contenus de la base de données ne sont pas clonés.

### <a name="references"></a>Références
* [Commandes PowerShell basées sur Azure Resource Manager pour Application web Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Clonage d’application web à l’aide du portail Azure](app-service-web-app-cloning-portal.md)
* [Sauvegarde d’une application web dans Azure App Service](web-sites-backup.md)
* [Prise en charge d’Azure Resource Manager pour la version préliminaire d’Azure Traffic Manager](../traffic-manager/traffic-manager-powershell-arm.md)
* [Introduction tooApp environnement de Service](app-service-app-service-environment-intro.md)
* [Utilisation d'Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md)

