---
title: "aaaAzure exemple de déploiement de Script Service Fabric CLI"
description: "Déployer un cluster d’Azure Service Fabric tooan application à l’aide de hello CLI d’Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="3b04b-103">Déployer un cluster de Service Fabric application tooa</span><span class="sxs-lookup"><span data-stu-id="3b04b-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="3b04b-104">Cet exemple de script copie d’un magasin d’image application package tooa cluster enregistre le type de l’application hello dans un cluster de hello et crée une instance d’application à partir du type d’application hello.</span><span class="sxs-lookup"><span data-stu-id="3b04b-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="3b04b-105">Tous les services par défaut sont également créés à ce stade.</span><span class="sxs-lookup"><span data-stu-id="3b04b-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="3b04b-106">Si nécessaire, installez hello [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3b04b-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="3b04b-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="3b04b-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3b04b-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="3b04b-108">Clean up deployment</span></span>

<span data-ttu-id="3b04b-109">Lorsque vous avez terminé, hello [supprimer](cli-remove-application.md) script peut être utilisé tooremove hello application.</span><span class="sxs-lookup"><span data-stu-id="3b04b-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="3b04b-110">script de suppression Hello supprime l’instance de l’application hello annule l’inscription du type de l’application hello et supprime le package d’application hello du magasin d’images.</span><span class="sxs-lookup"><span data-stu-id="3b04b-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b04b-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b04b-111">Next steps</span></span>

<span data-ttu-id="3b04b-112">Pour plus d’informations, consultez hello [documentation relative à Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3b04b-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="3b04b-113">Vous trouverez des exemples supplémentaires de Service Fabric CLI pour Azure Service Fabric Bonjour [exemples de Service Fabric CLI](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3b04b-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
