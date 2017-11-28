---
title: "Exemple de script Azure CLI - Acheminer le trafic pour la haute disponibilité des applications | Microsoft Docs"
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
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="e9268-103">Acheminer le trafic pour la haute disponibilité des applications</span><span class="sxs-lookup"><span data-stu-id="e9268-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="e9268-104">Ce script crée un groupe de ressources, deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="e9268-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="e9268-105">Traffic Manager dirige le trafic vers l’application d’une région considérée comme région principale et d’une région secondaire lorsque l’application de la région principale n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="e9268-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="e9268-106">Avant d’exécuter le script, veillez à modifier les valeurs MyWebApp, MyWebAppL1 et MyWebAppL2 pour leur attribuer des valeurs uniques dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e9268-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="e9268-107">Après avoir exécuté le script, vous pouvez accéder à l’application de la région principale avec l’URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="e9268-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e9268-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e9268-108">Sample script</span></span>

<span data-ttu-id="e9268-109">[!code-azurecli-interactive[principal](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Acheminer le trafic pour la haute disponibilité")]</span><span class="sxs-lookup"><span data-stu-id="e9268-109">[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="e9268-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="e9268-110">Clean up deployment</span></span> 

<span data-ttu-id="e9268-111">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application App Service et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e9268-111">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e9268-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e9268-112">Script explanation</span></span>

<span data-ttu-id="e9268-113">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web, un profil Traffic Manager et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e9268-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="e9268-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="e9268-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e9268-115">Commande</span><span class="sxs-lookup"><span data-stu-id="e9268-115">Command</span></span> | <span data-ttu-id="e9268-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="e9268-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e9268-117">az group create</span><span class="sxs-lookup"><span data-stu-id="e9268-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e9268-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e9268-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e9268-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e9268-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e9268-120">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="e9268-120">Creates an App Service plan.</span></span> <span data-ttu-id="e9268-121">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e9268-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="e9268-122">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="e9268-122">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="e9268-123">Crée une application web Azure dans le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="e9268-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="e9268-124">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="e9268-124">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="e9268-125">Crée un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="e9268-125">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="e9268-126">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="e9268-126">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="e9268-127">Ajoute un point de terminaison à un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="e9268-127">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9268-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e9268-128">Next steps</span></span>

<span data-ttu-id="e9268-129">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9268-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e9268-130">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à la mise en réseau Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e9268-130">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>
