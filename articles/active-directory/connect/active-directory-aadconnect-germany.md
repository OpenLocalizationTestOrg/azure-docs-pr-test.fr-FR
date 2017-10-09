---
title: aaaAzure AD Connect en Allemagne de Microsoft Cloud
description: "Azure AD Connect intègre vos répertoires locaux à Azure Active Directory. Cela vous permet de tooprovide une identité commune pour les applications Office 365, Azure et SaaS intégrée à Azure AD."
keywords: "Introduction tooAzure AD Connect, vue d’ensemble de Azure AD Connect, ce qui est Azure AD Connect, installer active directory, Allemagne, noir forêt"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="a3cd1-105">Azure AD Connect dans Microsoft Cloud Germany - Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="a3cd1-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="a3cd1-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="a3cd1-106">Introduction</span></span>
<span data-ttu-id="a3cd1-107">Azure AD Connect fournit la synchronisation entre Active Directory local et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="a3cd1-108">Actuellement, la plupart des scénarios de hello dans [Microsoft Cloud Allemagne](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) doit être réalisée par l’opérateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="a3cd1-109">Lorsque vous utilisez Microsoft Cloud Allemagne, vous devez être conscient des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="a3cd1-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="a3cd1-110">Hello URL suivantes doivent être ouvert sur un serveur proxy pour la synchronisation toooccur correctement :</span><span class="sxs-lookup"><span data-stu-id="a3cd1-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="a3cd1-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="a3cd1-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="a3cd1-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="a3cd1-112">*.windows.net</span></span>
  * * <span data-ttu-id="a3cd1-113">Listes de révocation de certificat</span><span class="sxs-lookup"><span data-stu-id="a3cd1-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="a3cd1-114">Lorsque vous vous connectez dans Windows Azure AD tooyour, vous devez utiliser un compte dans le domaine de onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="a3cd1-115">Hello suivant les fonctionnalités n’est pas disponible :</span><span class="sxs-lookup"><span data-stu-id="a3cd1-115">hello following features are not available:</span></span>
  * <span data-ttu-id="a3cd1-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="a3cd1-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="a3cd1-117">Mises à jour automatiques</span><span class="sxs-lookup"><span data-stu-id="a3cd1-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="a3cd1-118">Télécharger</span><span class="sxs-lookup"><span data-stu-id="a3cd1-118">Download</span></span>
<span data-ttu-id="a3cd1-119">Vous pouvez télécharger Azure AD Connect à partir du panneau d’Azure AD Connect hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="a3cd1-120">Utilisez les instructions hello sous le panneau d’Azure AD Connect toolocate hello.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="a3cd1-121">Hello Panneau de connexion Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3cd1-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="a3cd1-122">Une fois que vous avez connecté toohello portail Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="a3cd1-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="a3cd1-123">Accédez tooBrowse</span><span class="sxs-lookup"><span data-stu-id="a3cd1-123">Go tooBrowse</span></span>
2. <span data-ttu-id="a3cd1-124">Sélectionnez Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3cd1-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="a3cd1-125">Puis sélectionnez Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="a3cd1-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="a3cd1-126">Vous devez voir s’afficher hello :</span><span class="sxs-lookup"><span data-stu-id="a3cd1-126">You should see hello following:</span></span>

![Panneau Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="a3cd1-128">Hello tableau suivant décrit les fonctionnalités de hello indiquées dans le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="a3cd1-129">Intitulé</span><span class="sxs-lookup"><span data-stu-id="a3cd1-129">Title</span></span> | <span data-ttu-id="a3cd1-130">Description</span><span class="sxs-lookup"><span data-stu-id="a3cd1-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3cd1-131">ÉTAT DE LA SYNCHRONISATION</span><span class="sxs-lookup"><span data-stu-id="a3cd1-131">SYNC STATUS</span></span> |<span data-ttu-id="a3cd1-132">Vous indique si la synchronisation est activée ou désactivée.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="a3cd1-133">DERNIÈRE SYNCHRONISATION</span><span class="sxs-lookup"><span data-stu-id="a3cd1-133">LAST SYNC</span></span> |<span data-ttu-id="a3cd1-134">Hello la dernière fois qu’une synchronisation réussie s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="a3cd1-135">DOMAINES FÉDÉRÉS</span><span class="sxs-lookup"><span data-stu-id="a3cd1-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="a3cd1-136">Affiche le nombre hello de domaines fédérés actuellement configuré.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="a3cd1-137">Installation</span><span class="sxs-lookup"><span data-stu-id="a3cd1-137">Installation</span></span>
<span data-ttu-id="a3cd1-138">tooinstall Azure AD Connect, vous pouvez utiliser la documentation de hello [ici](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="a3cd1-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="a3cd1-139">Fonctionnalités avancées et informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a3cd1-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="a3cd1-140">Pour plus d’informations et des conseils sur les paramètres personnalisés ou les configurations avancées, commencez par [Intégration des identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="a3cd1-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="a3cd1-141">Cette page fournit des informations et des liens tooadditional Guide.</span><span class="sxs-lookup"><span data-stu-id="a3cd1-141">This page provides information and links tooadditional guidance.</span></span>

