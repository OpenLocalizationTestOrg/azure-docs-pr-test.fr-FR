---
title: aaaDelete Azure cluster et ses ressources | Documents Microsoft
description: "Découvrez comment toocompletely supprimer une structure de Service de cluster un groupe de ressources hello suppression contenant hello cluster ou en supprimant sélectivement des ressources."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Supprimer un cluster Service Fabric sur les ressources Azure et hello qu’il utilise
Un cluster Service Fabric est composé de nombreuses autres ressources Windows Azure en outre toohello du cluster lui-même. Toocompletely supprimer un cluster Service Fabric, vous devez également toodelete que tous hello il est constitué de ressources.
Vous avez deux options : un groupe de ressources hello delete hello cluster est dans (ce qui supprime la ressource de cluster hello et d’autres ressources dans le groupe de ressources hello) ou spécifiquement supprimer la ressource de cluster de hello et il est associé à des ressources (mais pas d’autres ressources de groupe de ressources hello).

> [!NOTE]
> Suppression de ressource de cluster hello **pas** supprimer tous les hello d’autres ressources de votre cluster Service Fabric est composé de.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>Supprimer le groupe de ressources entière hello (RG) qui hello Service Fabric cluster se trouve dans
Il s’agit de hello tooensure de façon plus simple que vous supprimez toutes les ressources de hello associées à votre cluster, y compris le groupe de ressources hello. Vous pouvez supprimer le groupe de ressources hello à l’aide de PowerShell ou via hello portail Azure. Si votre groupe de ressources comporte des ressources qui ne sont pas en cluster de l’ensemble fibre optique tooService connexes, vous pouvez supprimer des ressources spécifiques.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Supprimer le groupe de ressources hello à l’aide d’Azure PowerShell
Vous pouvez également supprimer le groupe de ressources hello en hello suivant d’applets de commande Azure PowerShell en cours d’exécution. Vérifiez qu’Azure PowerShell 1.0 ou une version ultérieure est installé sur votre ordinateur. Si vous n’avez pas fait avant, suivez les étapes de hello décrites dans [comment tooinstall et configurer Azure PowerShell.](/powershell/azure/overview)

Ouvrez une fenêtre PowerShell et exécutez hello suivant d’applets de commande PS :

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

Vous obtiendrez une suppression de hello tooconfirm invite si vous n’utilisez pas hello *-Force* option. Confirmation de hello RG et toutes les ressources hello qu’il contient sont supprimés.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Supprimer un groupe de ressources Bonjour portail Azure
1. Connexion toohello [portail Azure](https://portal.azure.com).
2. Accédez à cluster Service Fabric de toohello vous souhaitez toodelete.
3. Cliquez sur hello le nom du groupe de ressources sur la page d’essentials hello cluster.
4. Ceci fait apparaître hello **Essentials du groupe de ressources** page.
5. Cliquez sur **Supprimer**.
6. Suivez les instructions de hello sur cette page toocomplete hello la suppression du groupe de ressources hello.

![Supprimer un groupe de ressources][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>Supprimer la ressource de cluster hello et ressources hello qu’il utilise, mais pas d’autres ressources dans le groupe de ressources hello
Si votre groupe de ressources a uniquement les ressources qui sont le cluster Service Fabric de toohello connexes souhaité toodelete, il est plus facile groupe de ressource entier toodelete hello. Si vous souhaitez que les ressources de hello tooselectively supprimer un par un dans votre groupe de ressources, puis procédez comme suit.

Si vous avez déployé votre cluster à l’aide du portail de hello ou à l’aide d’un des modèles du Gestionnaire de ressources de l’infrastructure de Service hello à partir de la galerie de modèles de hello, toutes les ressources hello hello de cluster utilise sont balisés avec hello suivant deux balises. Vous pouvez les utiliser toodecide les ressources que vous souhaitez toodelete.

***Balise n° 1 :*** clé = clusterName, valeur = « nom du cluster de hello »

***Balise 2 :*** Clé = resourceName, Valeur = ServiceFabric

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Supprimer des ressources spécifiques dans hello portail Azure
1. Connexion toohello [portail Azure](https://portal.azure.com).
2. Accédez à cluster Service Fabric de toohello vous souhaitez toodelete.
3. Accédez trop**tous les paramètres** sur le panneau d’essentials hello.
4. Cliquez sur **balises** sous **gestion des ressources** dans le panneau des paramètres hello.
5. Cliquez sur un des hello **balises** dans tooget Panneau de balises hello une liste de toutes les ressources hello avec cette balise.
   
    ![Balises de ressource][ResourceTags]
6. Une fois que vous avez liste hello de ressources avec balises, cliquez sur chacune des ressources de hello et les supprimer.
   
    ![Ressources balisées][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Supprimer des ressources hello à l’aide d’Azure PowerShell
Vous pouvez supprimer des ressources de hello un-à-un en exécutant hello suivant d’applets de commande PowerShell de Azure. Vérifiez qu’Azure PowerShell 1.0 ou une version ultérieure est installé sur votre ordinateur. Si vous n’avez pas fait avant, suivez les étapes de hello décrites dans [comment tooinstall et configurer Azure PowerShell.](/powershell/azure/overview)

Ouvrez une fenêtre PowerShell et exécutez hello suivant d’applets de commande PS :

```powershell
Login-AzureRmAccount
```
Pour chacune des ressources de hello, vous souhaitez que toodelete, exécutez hello suivante :

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

ressource de cluster hello toodelete, exécutez hello suivante :

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>Étapes suivantes
Hello en lecture suivant tooalso en savoir plus sur la mise à niveau un cluster et le partitionnement des services :

* [En savoir plus sur les mises à niveau de cluster](service-fabric-cluster-upgrade.md)
* [En savoir plus sur le partitionnement de services avec état pour une mise à l’échelle maximale](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
