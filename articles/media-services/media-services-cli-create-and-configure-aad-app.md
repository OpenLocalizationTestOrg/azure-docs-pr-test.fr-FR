---
title: "Utiliser l’interface CLI 2.0 pour créer une application Azure AD et la configurer pour accéder à l’API Azure Media Services | Microsoft Docs"
description: "Cette rubrique montre comment utiliser l’interface CLI 2.0 pour créer une application Azure AD et la configurer pour accéder à l’API d’Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 01a2bb6d99776feec936315bc882c3097ce832d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-cli-20-to-create-an-aad-app-and-configure-it-to-access-azure-media-services-api"></a><span data-ttu-id="3b998-103">Utiliser l’interface CLI 2.0 pour créer une application AAD et la configurer pour accéder à l’API Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="3b998-103">Use CLI 2.0 to create an AAD app and configure it to access Azure Media Services API</span></span>

<span data-ttu-id="3b998-104">Cette rubrique vous montre comment utiliser l’interface CLI 2.0 pour créer une application Azure Active Directory (Azure AD) et un principal de service pour accéder aux ressources Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="3b998-104">This topic shows you how to use CLI 2.0 to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3b998-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3b998-105">Prerequisites</span></span>

- <span data-ttu-id="3b998-106">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3b998-106">An Azure account.</span></span> <span data-ttu-id="3b998-107">Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b998-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="3b998-108">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="3b998-108">A Media Services account.</span></span> <span data-ttu-id="3b998-109">Pour plus d’informations, voir [Création d’un compte Azure Media Services à l’aide du portail Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="3b998-109">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-the-azure-cloud-shell"></a><span data-ttu-id="3b998-110">Utiliser Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="3b998-110">Use the Azure Cloud Shell</span></span>

1. <span data-ttu-id="3b998-111">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3b998-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3b998-112">Lancez Cloud Shell à partir du volet de navigation supérieur du portail.</span><span class="sxs-lookup"><span data-stu-id="3b998-112">Launch the Cloud Shell from the upper navigation pane of the portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="3b998-114">Pour plus d’informations, voir la [présentation d’Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b998-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-to-the-media-account-with-cli-20"></a><span data-ttu-id="3b998-115">Créer une application Azure AD et configurer l’accès au compte multimédia avec l’interface CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3b998-115">Create an Azure AD app and configure access to the media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="3b998-116">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3b998-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="3b998-117">Dans cet exemple, l’**étendue** est le chemin d’accès complet de la ressource pour le compte de services multimédia.</span><span class="sxs-lookup"><span data-stu-id="3b998-117">In this example, the **scope** is the full resource path for the media services account.</span></span> <span data-ttu-id="3b998-118">Toutefois, l’**étendue** peut être à n’importe quel niveau.</span><span class="sxs-lookup"><span data-stu-id="3b998-118">However, the **scope** can be at any level.</span></span>

<span data-ttu-id="3b998-119">Par exemple, il peut s’agir d’un des niveaux suivants :</span><span class="sxs-lookup"><span data-stu-id="3b998-119">For example, it could be one of the following levels:</span></span>
 
* <span data-ttu-id="3b998-120">Niveau d'**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="3b998-120">The **subscription** level.</span></span>
* <span data-ttu-id="3b998-121">Niveau de **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="3b998-121">The **resource group** level.</span></span>
* <span data-ttu-id="3b998-122">Niveau de **ressource** (par exemple, compte multimédia).</span><span class="sxs-lookup"><span data-stu-id="3b998-122">The **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="3b998-123">Pour plus d’informations, voir [Créer un principal du service avec Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3b998-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="3b998-124">Voir aussi [Gestion du contrôle d’accès en fonction du rôle avec l’interface de ligne de commande Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3b998-124">Also see [Manage Role-Based Access Control with the Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3b998-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b998-125">Next steps</span></span>

<span data-ttu-id="3b998-126">Commencez le [chargement de fichiers sur votre compte](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="3b998-126">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
