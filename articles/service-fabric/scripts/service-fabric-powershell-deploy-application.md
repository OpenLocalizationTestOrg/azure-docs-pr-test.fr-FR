---
title: "aaaAzure exemple de Script PowerShell - déploiement d’application tooa cluster | Documents Microsoft"
description: "Script Azure PowerShell exemple - déploiement d’un cluster de Service Fabric application tooa."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="4160f-103">Déployer un cluster de Service Fabric application tooa</span><span class="sxs-lookup"><span data-stu-id="4160f-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="4160f-104">Cet exemple de script copie d’un magasin d’image application package tooa cluster enregistre le type de l’application hello dans un cluster de hello et crée une instance d’application à partir du type d’application hello.</span><span class="sxs-lookup"><span data-stu-id="4160f-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="4160f-105">Si tous les services par défaut ont été définies dans le manifeste de l’application hello hello cible du type d’application, ces services sont créés pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="4160f-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="4160f-106">Personnaliser les paramètres de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="4160f-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="4160f-107">Si nécessaire, installez le module PowerShell de l’infrastructure de Service de hello avec hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4160f-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4160f-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="4160f-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4160f-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="4160f-109">Clean up deployment</span></span> 

<span data-ttu-id="4160f-110">Une fois l’exemple de script hello a été exécuté, hello script dans [supprimer une application](service-fabric-powershell-remove-application.md) peut être l’instance de l’application hello tooremove utilisé, annuler l’inscription du type de l’application hello et supprimer le package d’application hello à partir du magasin d’images hello.</span><span class="sxs-lookup"><span data-stu-id="4160f-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="4160f-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="4160f-111">Script explanation</span></span>

<span data-ttu-id="4160f-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="4160f-112">This script uses hello following commands.</span></span> <span data-ttu-id="4160f-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="4160f-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4160f-114">Commande</span><span class="sxs-lookup"><span data-stu-id="4160f-114">Command</span></span> | <span data-ttu-id="4160f-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="4160f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4160f-116">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="4160f-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="4160f-117">Copier un magasin d’image application package toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="4160f-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="4160f-118">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="4160f-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="4160f-119">Inscrit un type d’application et la version sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4160f-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="4160f-120">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="4160f-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="4160f-121">Crée une application à partir d’un type d’application inscrit.</span><span class="sxs-lookup"><span data-stu-id="4160f-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4160f-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4160f-122">Next steps</span></span>

<span data-ttu-id="4160f-123">Pour plus d’informations sur le module PowerShell de l’infrastructure de Service de hello, consultez [documentation Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4160f-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="4160f-124">Vous trouverez des exemples supplémentaires de Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4160f-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
