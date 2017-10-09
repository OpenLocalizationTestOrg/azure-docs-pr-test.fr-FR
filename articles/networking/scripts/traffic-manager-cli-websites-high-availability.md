---
title: "Exemple de Script CLI - acheminer le trafic pour la haute disponibilité des applications d’aaaAzure | Documents Microsoft"
description: "Exemple de script Azure CLI - Acheminer le trafic pour la haute disponibilité des applications"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="7c83b-103">Acheminer le trafic pour la haute disponibilité des applications</span><span class="sxs-lookup"><span data-stu-id="7c83b-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="7c83b-104">Ce script crée un groupe de ressources, deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="7c83b-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="7c83b-105">Traffic Manager dirige application toohello au trafic dans une région en tant que zone principale de hello et la région secondaire toohello lors de l’application hello dans la région principale de hello n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="7c83b-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="7c83b-106">Avant d’exécuter le script de hello, vous devez modifier hello MyWebApp, MyWebAppL1 et MyWebAppL2 valeurs toounique valeurs sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7c83b-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="7c83b-107">Après avoir exécuté le script de hello, vous pouvez accéder à application hello dans la région principale de hello avec hello URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="7c83b-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7c83b-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="7c83b-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="7c83b-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="7c83b-109">Clean up deployment</span></span> 

<span data-ttu-id="7c83b-110">Après exécution de l’exemple de script hello, la commande de suivi de hello peut être groupe de ressources utilisé tooremove hello, application de Service d’applications et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="7c83b-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="7c83b-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="7c83b-111">Script explanation</span></span>

<span data-ttu-id="7c83b-112">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’application web, le profil traffic manager, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="7c83b-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="7c83b-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="7c83b-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7c83b-114">Commande</span><span class="sxs-lookup"><span data-stu-id="7c83b-114">Command</span></span> | <span data-ttu-id="7c83b-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="7c83b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c83b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="7c83b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7c83b-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="7c83b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7c83b-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="7c83b-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7c83b-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="7c83b-119">Creates an App Service plan.</span></span> <span data-ttu-id="7c83b-120">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="7c83b-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="7c83b-121">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="7c83b-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="7c83b-122">Crée une application web Azure dans hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="7c83b-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="7c83b-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="7c83b-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="7c83b-124">Crée un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="7c83b-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="7c83b-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="7c83b-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="7c83b-126">Ajoute un point de terminaison de tooan profil Traffic Manager de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c83b-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c83b-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c83b-127">Next steps</span></span>

<span data-ttu-id="7c83b-128">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c83b-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7c83b-129">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation de la mise en réseau Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c83b-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
