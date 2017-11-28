---
title: "aaaAzure exemple de Script CLI - lier une application du web tooa de certificat SSL personnalisée | Documents Microsoft"
description: "Exemple de Script CLI Azure - liaison d’une application web des tooa de certificat personnalisée SSL"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="1234e-103">Lier une application du web tooa de certificat SSL personnalisée</span><span class="sxs-lookup"><span data-stu-id="1234e-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="1234e-104">Cet exemple de script crée une application web dans le Service d’applications avec ses ressources connexes, puis lie le certificat SSL de hello d’un tooit de nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="1234e-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="1234e-105">Pour cet exemple, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1234e-105">For this sample, you will need:</span></span>

* <span data-ttu-id="1234e-106">Page de configuration tooyour domaine du bureau d’enregistrement DNS d’accès.</span><span class="sxs-lookup"><span data-stu-id="1234e-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="1234e-107">Valide. Le fichier PFX et son mot de passe hello SSL de certificat vous souhaitez tooupload et établir une liaison.</span><span class="sxs-lookup"><span data-stu-id="1234e-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1234e-108">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1234e-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1234e-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1234e-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1234e-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1234e-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="1234e-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="1234e-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1234e-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="1234e-112">Script explanation</span></span>

<span data-ttu-id="1234e-113">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="1234e-113">This script uses hello following commands.</span></span> <span data-ttu-id="1234e-114">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="1234e-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1234e-115">Commande</span><span class="sxs-lookup"><span data-stu-id="1234e-115">Command</span></span> | <span data-ttu-id="1234e-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="1234e-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1234e-117">az group create</span><span class="sxs-lookup"><span data-stu-id="1234e-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1234e-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="1234e-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1234e-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="1234e-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="1234e-120">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="1234e-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1234e-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="1234e-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="1234e-122">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="1234e-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="1234e-123">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="1234e-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="1234e-124">Mappe une domaine personnalisé tooa l’application web.</span><span class="sxs-lookup"><span data-stu-id="1234e-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="1234e-125">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="1234e-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="1234e-126">Télécharge une certificat SSL tooa l’application web.</span><span class="sxs-lookup"><span data-stu-id="1234e-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="1234e-127">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="1234e-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="1234e-128">Lie une application web des tooa de certificat téléchargée SSL.</span><span class="sxs-lookup"><span data-stu-id="1234e-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1234e-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1234e-129">Next steps</span></span>

<span data-ttu-id="1234e-130">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1234e-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1234e-131">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1234e-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
