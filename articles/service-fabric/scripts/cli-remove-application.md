---
title: aaaAzure Service Fabric CLI Script supprimer (exemple)
description: "Supprimer une application à partir d’un cluster Azure Service Fabric à l’aide de hello CLI d’Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: thraka
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
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="376b0-103">Supprimer une application d’un cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="376b0-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="376b0-104">Cet exemple de script supprime une instance en cours d’exécution de l’application Service Fabric, annule l’inscription d’un type d’application et la version du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="376b0-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="376b0-105">Instance de l’application hello suppression supprime également hello toutes les instances de service associés à cette application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="376b0-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="376b0-106">Ensuite, les fichiers de l’application hello sont supprimés à partir du magasin d’images hello.</span><span class="sxs-lookup"><span data-stu-id="376b0-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="376b0-107">Si nécessaire, installez hello [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="376b0-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="376b0-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="376b0-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="376b0-109">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="376b0-109">Next steps</span></span>

<span data-ttu-id="376b0-110">Pour plus d’informations, consultez hello [documentation relative à Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="376b0-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="376b0-111">Vous trouverez des exemples supplémentaires de Service Fabric CLI pour Azure Service Fabric Bonjour [exemples de Service Fabric CLI](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="376b0-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
