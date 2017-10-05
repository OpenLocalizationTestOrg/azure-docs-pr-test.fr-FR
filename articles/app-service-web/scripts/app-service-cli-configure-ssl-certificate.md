---
title: "Exemple de script Azure CLI - Lier un certificat SSL personnalisé à une application web | Microsoft Docs"
description: "Exemple de script Azure CLI - Lier un certificat SSL personnalisé à une application web"
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
ms.openlocfilehash: d4fab3fb2c297bf5f498b63bee46692febb9180b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="d887a-103">Lier un certificat SSL personnalisé à une application web</span><span class="sxs-lookup"><span data-stu-id="d887a-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="d887a-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis lie le certificat SSL d’un nom de domaine personnalisé à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="d887a-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="d887a-105">Pour cet exemple, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d887a-105">For this sample, you will need:</span></span>

* <span data-ttu-id="d887a-106">Un accès à la page de configuration DNS du Registre de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="d887a-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="d887a-107">Un fichier .PFX valide et son mot de passe pour le certificat SSL que vous voulez charger et lier.</span><span class="sxs-lookup"><span data-stu-id="d887a-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d887a-108">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d887a-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d887a-109">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="d887a-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="d887a-110">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d887a-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="d887a-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d887a-111">Sample script</span></span>

<span data-ttu-id="d887a-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Lier un certificat SSL personnalisé à une application web")]</span><span class="sxs-lookup"><span data-stu-id="d887a-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d887a-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d887a-113">Script explanation</span></span>

<span data-ttu-id="d887a-114">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d887a-114">This script uses the following commands.</span></span> <span data-ttu-id="d887a-115">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="d887a-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d887a-116">Commande</span><span class="sxs-lookup"><span data-stu-id="d887a-116">Command</span></span> | <span data-ttu-id="d887a-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="d887a-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d887a-118">az group create</span><span class="sxs-lookup"><span data-stu-id="d887a-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d887a-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d887a-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d887a-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="d887a-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="d887a-121">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="d887a-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d887a-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="d887a-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="d887a-123">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="d887a-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="d887a-124">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="d887a-124">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="d887a-125">Mappe un domaine personnalisé à une application web.</span><span class="sxs-lookup"><span data-stu-id="d887a-125">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="d887a-126">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="d887a-126">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="d887a-127">Charge un certificat SSL personnalisé sur une application web.</span><span class="sxs-lookup"><span data-stu-id="d887a-127">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="d887a-128">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="d887a-128">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="d887a-129">Lie un certificat SSL chargé à une application web.</span><span class="sxs-lookup"><span data-stu-id="d887a-129">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d887a-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d887a-130">Next steps</span></span>

<span data-ttu-id="d887a-131">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d887a-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d887a-132">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d887a-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
