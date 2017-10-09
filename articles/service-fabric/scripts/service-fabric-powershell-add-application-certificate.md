---
title: aaaAzure exemple de Script PowerShell - ajouter application cert tooa cluster | Documents Microsoft
description: Script Azure PowerShell exemple - ajouter un cluster de Service Fabric application certificat tooa.
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
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="51305-103">Ajouter un cluster de Service Fabric application certificat tooa</span><span class="sxs-lookup"><span data-stu-id="51305-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="51305-104">Cet exemple de script crée un certificat auto-signé dans le coffre de clés Azure spécifié hello et l’installe tooall des nœuds de cluster du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="51305-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="51305-105">certificat de Hello télécharge également le dossier local de tooa.</span><span class="sxs-lookup"><span data-stu-id="51305-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="51305-106">nom Hello du certificat de hello téléchargé est hello identique au nom du certificat hello dans le coffre de clés hello hello.</span><span class="sxs-lookup"><span data-stu-id="51305-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="51305-107">Personnaliser les paramètres de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="51305-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="51305-108">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview) , puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="51305-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="51305-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="51305-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="51305-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="51305-110">Script explanation</span></span>

<span data-ttu-id="51305-111">Ce script utilise hello suivant de commandes : chaque commande dans la table de hello lie la documentation spécifique de toocommand.</span><span class="sxs-lookup"><span data-stu-id="51305-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="51305-112">Commande</span><span class="sxs-lookup"><span data-stu-id="51305-112">Command</span></span> | <span data-ttu-id="51305-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="51305-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="51305-114">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="51305-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="51305-115">Ajouter qu'une nouvelle application certificat toohello machine virtuelle identiques qui composent le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="51305-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="51305-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51305-116">Next steps</span></span>

<span data-ttu-id="51305-117">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="51305-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="51305-118">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="51305-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
