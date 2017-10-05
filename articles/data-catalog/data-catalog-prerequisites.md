---
title: "Conditions préalables à l’utilisation d’Azure Data Catalog | Microsoft Docs"
description: "Découvrez les prérequis dont vous avez besoin pour bien démarrer avec Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 3fdef7bb58a5cd5dfbe4d37d9baf9c8e392ebe42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="d9d20-103">Configuration requise pour Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="d9d20-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="d9d20-104">Vous devez vous occuper de certaines choses avant de configurer Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="d9d20-104">You need to take care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="d9d20-105">Ce processus ne sera pas long.</span><span class="sxs-lookup"><span data-stu-id="d9d20-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="d9d20-106">Abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="d9d20-106">Azure subscription</span></span>
<span data-ttu-id="d9d20-107">Pour configurer Data Catalog, vous devez être le propriétaire ou le copropriétaire d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d9d20-107">To set up Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="d9d20-108">Les abonnements Azure vous permettent d’organiser l’accès aux ressources du service cloud telles que Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="d9d20-108">Azure subscriptions help you organize access to cloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="d9d20-109">Ils vous permettent également de contrôler le signalement, la facturation et le paiement des ressources utilisées.</span><span class="sxs-lookup"><span data-stu-id="d9d20-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="d9d20-110">Chaque abonnement peut disposer d’une configuration de facturation et de paiement différente. Vous pouvez donc avoir différents abonnements et différents plans par département, projet, bureau régional, etc.</span><span class="sxs-lookup"><span data-stu-id="d9d20-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="d9d20-111">Chaque service cloud appartient à un abonnement. Vous devez donc avoir un abonnement avant de configurer Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="d9d20-111">Every cloud service belongs to a subscription, and you need to have a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="d9d20-112">Pour plus d’informations, consultez [Manage Accounts, Subscriptions, and Administrative Roles](../active-directory/active-directory-assign-admin-roles.md) (Gérer les comptes, les abonnements et les rôles d’administrateur).</span><span class="sxs-lookup"><span data-stu-id="d9d20-112">To learn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="d9d20-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9d20-113">Azure Active Directory</span></span>
<span data-ttu-id="d9d20-114">Pour configurer Data Catalog, vous devez être connecté avec un compte d’utilisateur Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9d20-114">To set up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="d9d20-115">Azure AD permet à votre entreprise de gérer facilement les identités et les accès, à la fois dans le cloud et en local.</span><span class="sxs-lookup"><span data-stu-id="d9d20-115">Azure AD provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="d9d20-116">Les utilisateurs peuvent se servir du même compte professionnel ou scolaire pour utiliser l’authentification unique sur n’importe quelle application web locale ou cloud.</span><span class="sxs-lookup"><span data-stu-id="d9d20-116">Users can use a single work or school account for single sign-in to any cloud and on-premises web application.</span></span> <span data-ttu-id="d9d20-117">Data Catalog utilise Azure AD pour authentifier la connexion.</span><span class="sxs-lookup"><span data-stu-id="d9d20-117">Data Catalog uses Azure AD to authenticate sign-in.</span></span> <span data-ttu-id="d9d20-118">Pour plus d’informations, consultez l’article [Qu’est-ce qu’Azure Active Directory ?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9d20-118">To learn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d9d20-119">Le [portail Azure](http://portal.azure.com/) permet de se connecter à l’aide d’un compte Microsoft personnel ou d’un compte professionnel ou scolaire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9d20-119">By using the [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="d9d20-120">Pour configurer Data Catalog à l’aide du portail Azure ou du [portail Data Catalog](http://www.azuredatacatalog.com), vous devez vous connecter avec un compte Azure Active Directory, et non avec un compte personnel.</span><span class="sxs-lookup"><span data-stu-id="d9d20-120">To set up Data Catalog by using either the Azure portal or the [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="d9d20-121">Configuration de la stratégie Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9d20-121">Active Directory policy configuration</span></span>
<span data-ttu-id="d9d20-122">Il est possible que vous puissiez vous connecter au portail Data Catalog, mais que lorsque vous tentez de vous connecter à l’outil d’inscription de source de données, un message d’erreur s’affiche et vous empêche de vous connecter.</span><span class="sxs-lookup"><span data-stu-id="d9d20-122">You might encounter a situation where you can sign in to the Data Catalog portal, but when you attempt to sign in to the data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="d9d20-123">Ce problème peut aussi se produire quand l’utilisateur se trouve sur le réseau d’entreprise ou quand il se connecte en dehors du réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="d9d20-123">This problem behavior might occur only when you're on the company network, or it might occur only when you're connecting from outside the company network.</span></span>

<span data-ttu-id="d9d20-124">L’outil d’inscription de source de données utilise l’authentification par formulaire pour valider les informations d’identification par rapport à Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9d20-124">The data source registration tool uses Forms Authentication to validate your user credentials against Active Directory.</span></span> <span data-ttu-id="d9d20-125">Pour que vous puissiez vous connecter, un administrateur Active Directory doit activer l’authentification par formulaire dans la stratégie d’authentification globale.</span><span class="sxs-lookup"><span data-stu-id="d9d20-125">To help you sign in successfully, an Active Directory administrator must enable Forms Authentication in the Global Authentication Policy.</span></span>

<span data-ttu-id="d9d20-126">La stratégie d’authentification globale vous permet d’activer séparément des méthodes d’authentification pour les connexions intranet et extranet, comme le montre la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="d9d20-126">In the Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in the following screenshot.</span></span> <span data-ttu-id="d9d20-127">Des erreurs de connexion peuvent survenir si l’authentification par formulaire n’est pas activée pour le réseau à partir duquel vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="d9d20-127">Sign-in errors might occur if Forms Authentication is not enabled for the network from which you're connecting.</span></span>

 ![Stratégie d’authentification globale d’Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="d9d20-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9d20-129">Next steps</span></span>
<span data-ttu-id="d9d20-130">Pour plus d’informations, consultez [Configuration des stratégies d’authentification](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9d20-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
