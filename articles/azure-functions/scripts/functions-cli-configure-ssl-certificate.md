---
title: "Exemple de script Azure CLI - Lier un certificat SSL personnalisé à une Function App | Microsoft Docs"
description: "Exemple de script Azure CLI - Lier un certificat SSL personnalisé à une Function App dans Azure"
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
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="58697-103">Lier un certificat SSL personnalisé à une Function App</span><span class="sxs-lookup"><span data-stu-id="58697-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="58697-104">Cet exemple de script crée une Function App dans App Service avec ses ressources associées, puis y lie le certificat SSL d’un nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="58697-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="58697-105">Pour cet exemple, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="58697-105">For this sample, you need:</span></span>

* <span data-ttu-id="58697-106">Un accès à la page de configuration DNS du Registre de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="58697-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="58697-107">Un fichier .PFX valide et son mot de passe pour le certificat SSL que vous voulez charger et lier.</span><span class="sxs-lookup"><span data-stu-id="58697-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="58697-108">Pour lier un certificat SSL, votre Function App doit être créée dans un plan App Service et non dans un plan de consommation.</span><span class="sxs-lookup"><span data-stu-id="58697-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="58697-109">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="58697-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="58697-110">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="58697-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="58697-111">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="58697-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="58697-112">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="58697-112">Sample script</span></span>

<span data-ttu-id="58697-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Lier un certificat SSL personnalisé à une application web")]</span><span class="sxs-lookup"><span data-stu-id="58697-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="58697-114">Explication du script</span><span class="sxs-lookup"><span data-stu-id="58697-114">Script explanation</span></span>

<span data-ttu-id="58697-115">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="58697-115">This script uses the following commands.</span></span> <span data-ttu-id="58697-116">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="58697-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="58697-117">Commande</span><span class="sxs-lookup"><span data-stu-id="58697-117">Command</span></span> | <span data-ttu-id="58697-118">Remarques</span><span class="sxs-lookup"><span data-stu-id="58697-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="58697-119">az group create</span><span class="sxs-lookup"><span data-stu-id="58697-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="58697-120">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="58697-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="58697-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="58697-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="58697-122">Crée un plan App Service requis pour lier des certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="58697-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="58697-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="58697-123">az functionapp create</span></span>]() | <span data-ttu-id="58697-124">Crée une Function App.</span><span class="sxs-lookup"><span data-stu-id="58697-124">Creates a function app.</span></span> |
| [<span data-ttu-id="58697-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="58697-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="58697-126">Mappe un domaine personnalisé à la Function App.</span><span class="sxs-lookup"><span data-stu-id="58697-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="58697-127">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="58697-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="58697-128">Charge un certificat SSL personnalisé sur une Function App.</span><span class="sxs-lookup"><span data-stu-id="58697-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="58697-129">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="58697-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="58697-130">Lie un certificat SSL chargé à une Function App.</span><span class="sxs-lookup"><span data-stu-id="58697-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="58697-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58697-131">Next steps</span></span>

<span data-ttu-id="58697-132">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58697-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="58697-133">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service]().</span><span class="sxs-lookup"><span data-stu-id="58697-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
