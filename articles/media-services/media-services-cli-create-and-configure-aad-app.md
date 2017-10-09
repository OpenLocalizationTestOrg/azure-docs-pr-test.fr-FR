---
title: aaaUse CLI 2.0 toocreate une application Azure AD et configurez-le tooaccess API Azure Media Services | Documents Microsoft
description: Cette rubrique montre comment toouse CLI 2.0 toocreate une application Azure AD et configurez-le tooaccess API Azure Media Services.
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
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a><span data-ttu-id="2f104-103">Utilisez CLI 2.0 toocreate une application AAD et configurez-le tooaccess API Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="2f104-103">Use CLI 2.0 toocreate an AAD app and configure it tooaccess Azure Media Services API</span></span>

<span data-ttu-id="2f104-104">Cette rubrique vous montre comment toouse CLI 2.0 toocreate une application Azure Active Directory (Azure AD) tooaccess principal du service Azure Media Services et ressources.</span><span class="sxs-lookup"><span data-stu-id="2f104-104">This topic shows you how toouse CLI 2.0 toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2f104-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2f104-105">Prerequisites</span></span>

- <span data-ttu-id="2f104-106">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="2f104-106">An Azure account.</span></span> <span data-ttu-id="2f104-107">Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f104-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="2f104-108">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="2f104-108">A Media Services account.</span></span> <span data-ttu-id="2f104-109">Pour plus d’informations, consultez [créer un compte Azure Media Services à l’aide de hello Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="2f104-109">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-hello-azure-cloud-shell"></a><span data-ttu-id="2f104-110">Utilisez hello Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="2f104-110">Use hello Azure Cloud Shell</span></span>

1. <span data-ttu-id="2f104-111">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2f104-111">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2f104-112">Lancez hello Cloud Shell à partir du volet de navigation supérieur hello du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="2f104-112">Launch hello Cloud Shell from hello upper navigation pane of hello portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="2f104-114">Pour plus d’informations, voir la [présentation d’Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f104-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a><span data-ttu-id="2f104-115">Créer une application Azure AD et configurer le compte d’accès toohello media avec CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2f104-115">Create an Azure AD app and configure access toohello media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="2f104-116">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2f104-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="2f104-117">Dans cet exemple, hello **étendue** est chemin d’accès de ressource complet hello pour les médias de hello compte des services.</span><span class="sxs-lookup"><span data-stu-id="2f104-117">In this example, hello **scope** is hello full resource path for hello media services account.</span></span> <span data-ttu-id="2f104-118">Toutefois, hello **étendue** peut être n’importe quel niveau.</span><span class="sxs-lookup"><span data-stu-id="2f104-118">However, hello **scope** can be at any level.</span></span>

<span data-ttu-id="2f104-119">Par exemple, cela peut être un des hello suivant les niveaux :</span><span class="sxs-lookup"><span data-stu-id="2f104-119">For example, it could be one of hello following levels:</span></span>
 
* <span data-ttu-id="2f104-120">Hello **abonnement** niveau.</span><span class="sxs-lookup"><span data-stu-id="2f104-120">hello **subscription** level.</span></span>
* <span data-ttu-id="2f104-121">Hello **groupe de ressources** niveau.</span><span class="sxs-lookup"><span data-stu-id="2f104-121">hello **resource group** level.</span></span>
* <span data-ttu-id="2f104-122">Hello **ressource** niveau (par exemple, un compte de support).</span><span class="sxs-lookup"><span data-stu-id="2f104-122">hello **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="2f104-123">Pour plus d’informations, voir [Créer un principal du service avec Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f104-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="2f104-124">Consultez également [Manage Role-Based le contrôle d’accès avec hello interface de ligne de commande Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2f104-124">Also see [Manage Role-Based Access Control with hello Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2f104-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f104-125">Next steps</span></span>

<span data-ttu-id="2f104-126">Prise en main [téléchargement de fichiers tooyour compte](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="2f104-126">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
