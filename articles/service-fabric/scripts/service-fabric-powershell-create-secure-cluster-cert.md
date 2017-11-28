---
title: "aaaAzure exemple de Script PowerShell - créer un cluster Service Fabric | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Créer un cluster Service Fabric"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="ac052-103">Créer un cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ac052-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="ac052-104">Cet exemple de script crée un cluster Service Fabric à cinq nœuds sécurisé avec un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="ac052-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="ac052-105">commande Hello crée un certificat auto-signé et il télécharge tooa nouveau coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ac052-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="ac052-106">Hello certificat est également copié tooa les répertoire local.</span><span class="sxs-lookup"><span data-stu-id="ac052-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="ac052-107">Ensemble hello *-OS* version de hello paramètre toochoose de Windows ou Linux qui s’exécute sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ac052-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="ac052-108">Personnaliser les paramètres de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="ac052-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="ac052-109">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview) , puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="ac052-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ac052-110">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="ac052-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ac052-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="ac052-111">Clean up deployment</span></span> 

<span data-ttu-id="ac052-112">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources utilisé tooremove hello, cluster et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="ac052-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="ac052-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="ac052-113">Script explanation</span></span>

<span data-ttu-id="ac052-114">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="ac052-114">This script uses hello following commands.</span></span> <span data-ttu-id="ac052-115">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="ac052-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ac052-116">Commande</span><span class="sxs-lookup"><span data-stu-id="ac052-116">Command</span></span> | <span data-ttu-id="ac052-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="ac052-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac052-118">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="ac052-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="ac052-119">Crée un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ac052-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac052-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ac052-120">Next steps</span></span>

<span data-ttu-id="ac052-121">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac052-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ac052-122">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ac052-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
