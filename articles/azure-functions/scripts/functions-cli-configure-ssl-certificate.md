---
title: "aaaAzure exemple de Script CLI - lier à une application de fonction de tooa de certificat SSL personnalisée | Documents Microsoft"
description: "Exemple de Script CLI Azure - liaison d’une application du tooa fonction SSL certificat personnalisée dans Azure"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="2d2db-103">Lier une application personnalisée SSL certificat tooa (fonction)</span><span class="sxs-lookup"><span data-stu-id="2d2db-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="2d2db-104">Cet exemple de script crée une application de la fonction dans le Service d’applications avec ses ressources connexes, puis lie le certificat SSL de hello d’un tooit de nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2d2db-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="2d2db-105">Pour cet exemple, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2d2db-105">For this sample, you need:</span></span>

* <span data-ttu-id="2d2db-106">Page de configuration tooyour domaine du bureau d’enregistrement DNS d’accès.</span><span class="sxs-lookup"><span data-stu-id="2d2db-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="2d2db-107">Valide. Le fichier PFX et son mot de passe hello SSL de certificat vous souhaitez tooupload et établir une liaison.</span><span class="sxs-lookup"><span data-stu-id="2d2db-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="2d2db-108">toobind un certificat SSL, votre application de la fonction doit être créée dans un plan App Service et non dans un plan de la consommation.</span><span class="sxs-lookup"><span data-stu-id="2d2db-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2d2db-109">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2d2db-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2d2db-110">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="2d2db-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2d2db-111">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2d2db-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2d2db-112">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="2d2db-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2d2db-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="2d2db-113">Script explanation</span></span>

<span data-ttu-id="2d2db-114">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="2d2db-114">This script uses hello following commands.</span></span> <span data-ttu-id="2d2db-115">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="2d2db-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2d2db-116">Commande</span><span class="sxs-lookup"><span data-stu-id="2d2db-116">Command</span></span> | <span data-ttu-id="2d2db-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="2d2db-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2d2db-118">az group create</span><span class="sxs-lookup"><span data-stu-id="2d2db-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2d2db-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="2d2db-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2d2db-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="2d2db-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2d2db-121">Crée un toobind de plan requises du Service d’applications de certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="2d2db-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="2d2db-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="2d2db-122">az functionapp create</span></span>]() | <span data-ttu-id="2d2db-123">Crée une Function App.</span><span class="sxs-lookup"><span data-stu-id="2d2db-123">Creates a function app.</span></span> |
| [<span data-ttu-id="2d2db-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="2d2db-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="2d2db-125">Mappe une application de fonction toohello domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2d2db-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="2d2db-126">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="2d2db-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="2d2db-127">Télécharge une application de fonction de tooa de certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="2d2db-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="2d2db-128">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="2d2db-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="2d2db-129">Lie une application de fonction de tooa de certificat SSL téléchargée.</span><span class="sxs-lookup"><span data-stu-id="2d2db-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2d2db-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d2db-130">Next steps</span></span>

<span data-ttu-id="2d2db-131">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2d2db-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2d2db-132">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service]().</span><span class="sxs-lookup"><span data-stu-id="2d2db-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
