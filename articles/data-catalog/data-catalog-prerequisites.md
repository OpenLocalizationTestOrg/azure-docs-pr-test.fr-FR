---
title: "conditions préalables du catalogue de données aaaAzure | Documents Microsoft"
description: "En savoir plus sur la configuration requise de hello que vous devez tooget main d’Azure Data Catalog."
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
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="1aa69-103">Configuration requise pour Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="1aa69-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="1aa69-104">Vous devez tootake administration quelques éléments avant que vous pouvez configurer Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="1aa69-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="1aa69-105">Ce processus ne sera pas long.</span><span class="sxs-lookup"><span data-stu-id="1aa69-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="1aa69-106">Abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="1aa69-106">Azure subscription</span></span>
<span data-ttu-id="1aa69-107">tooset catalogue de données, vous devez être propriétaire de hello ou copropriétaire d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1aa69-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="1aa69-108">Abonnements Azure permettent d’organiser d’accéder aux ressources de service toocloud tels que des données de catalogue.</span><span class="sxs-lookup"><span data-stu-id="1aa69-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="1aa69-109">Ils vous permettent également de contrôler le signalement, la facturation et le paiement des ressources utilisées.</span><span class="sxs-lookup"><span data-stu-id="1aa69-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="1aa69-110">Chaque abonnement peut disposer d’une configuration de facturation et de paiement différente. Vous pouvez donc avoir différents abonnements et différents plans par département, projet, bureau régional, etc.</span><span class="sxs-lookup"><span data-stu-id="1aa69-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="1aa69-111">Chaque service cloud appartient tooa abonnement, et vous devez toohave un abonnement avant de configurer le catalogue de données.</span><span class="sxs-lookup"><span data-stu-id="1aa69-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="1aa69-112">toolearn, voir [gérer les comptes, les abonnements et les rôles d’administrateur](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1aa69-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="1aa69-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1aa69-113">Azure Active Directory</span></span>
<span data-ttu-id="1aa69-114">tooset catalogue de données, vous devez être connecté avec un compte d’utilisateur Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1aa69-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="1aa69-115">Azure AD fournit un moyen simple pour votre entreprise toomanage identités et des accès, à la fois dans le cloud de hello et sur site.</span><span class="sxs-lookup"><span data-stu-id="1aa69-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="1aa69-116">Les utilisateurs peuvent utiliser un seul compte professionnel ou scolaire pour le cloud de tooany de connexion unique et une application de web local.</span><span class="sxs-lookup"><span data-stu-id="1aa69-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="1aa69-117">Catalogue de données utilise l’authentification dans Azure AD tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="1aa69-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="1aa69-118">toolearn, voir [quoi consiste Azure Active Directory ?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1aa69-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1aa69-119">À l’aide de hello [portail Azure](http://portal.azure.com/), vous pouvez vous connecter avec un compte Microsoft personnel ou d’Azure Active Directory ou l’école de compte.</span><span class="sxs-lookup"><span data-stu-id="1aa69-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="1aa69-120">tooset catalogue de données à l’aide de hello soit portail Azure ou hello [portail Data Catalog](http://www.azuredatacatalog.com), vous devez vous connecter avec un compte Azure Active Directory, pas un compte personnel.</span><span class="sxs-lookup"><span data-stu-id="1aa69-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="1aa69-121">Configuration de la stratégie Active Directory</span><span class="sxs-lookup"><span data-stu-id="1aa69-121">Active Directory policy configuration</span></span>
<span data-ttu-id="1aa69-122">Vous pouvez rencontrer une situation où vous pouvez vous connecter dans le portail de toohello Data Catalog, mais lorsque vous essayez de toosign dans l’outil de l’enregistrement de source de données toohello, un message d’erreur qui vous empêche de se connecter.</span><span class="sxs-lookup"><span data-stu-id="1aa69-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="1aa69-123">Ce problème peut se produire uniquement lorsque vous êtes sur le réseau d’entreprise hello, ou elle peut se produire uniquement lorsque vous vous connectez à partir du réseau d’entreprise en dehors de hello.</span><span class="sxs-lookup"><span data-stu-id="1aa69-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="1aa69-124">outil de l’enregistrement de source de données Hello utilise l’authentification par formulaire toovalidate vos informations d’identification de l’utilisateur dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1aa69-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="1aa69-125">toohelp que vous vous connectez avec succès, un administrateur Active Directory doit activer l’authentification par formulaire Bonjour stratégie d’authentification globale.</span><span class="sxs-lookup"><span data-stu-id="1aa69-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="1aa69-126">Bonjour stratégie d’authentification globale, méthodes d’authentification peuvent être activées séparément pour l’intranet et extranet des connexions, comme indiqué dans hello suivant capture d’écran de.</span><span class="sxs-lookup"><span data-stu-id="1aa69-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="1aa69-127">Erreurs de connexion peuvent se produire si l’authentification par formulaire n’est pas activée pour le réseau hello à partir de laquelle vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="1aa69-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Stratégie d’authentification globale d’Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="1aa69-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1aa69-129">Next steps</span></span>
<span data-ttu-id="1aa69-130">Pour plus d’informations, consultez [Configuration des stratégies d’authentification](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="1aa69-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
