---
title: "Azure B2C Active Directory : Basculement tooa B2C client | Documents Microsoft"
description: Comment tooswitch en contexte hello de votre B2C Active Directory de client
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 572f9ab283ecac68d284bb04fdfc98575bcf9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="switching-tooyour-azure-ad-b2c-tenant"></a><span data-ttu-id="2c8e2-103">Commutation tooyour Azure AD B2C locataire</span><span class="sxs-lookup"><span data-stu-id="2c8e2-103">Switching tooyour Azure AD B2C tenant</span></span>

<span data-ttu-id="2c8e2-104">Dans l’ordre tooconfigure Azure AD B2C, vous devez toobe dans le contexte de hello de votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-104">In order tooconfigure Azure AD B2C, you need toobe in hello context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="2c8e2-105">Se connecter au locataire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2c8e2-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="2c8e2-106">toonavigate tooyour de locataire Azure AD B2C, vous devez être connecté en tant qu’un administrateur général du locataire d’Azure AD B2C de hello en hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-106">toonavigate tooyour Azure AD B2C tenant, you must be logged into hello Azure portal as a global administrator of hello Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="2c8e2-107">L’authentification à hello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c8e2-107">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="2c8e2-108">Basculer les locataires en cliquant sur votre adresse de messagerie ou d’une image dans l’angle supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-108">Switch tenants by clicking your email address or picture in hello top-right corner.</span></span>
1. <span data-ttu-id="2c8e2-109">Bonjour `Directory` liste qui s’affiche, le locataire hello sélectionnez Azure AD B2C que vous souhaitez toomanage.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-109">In hello `Directory` list that appears, select hello Azure AD B2C tenant that you wish toomanage.</span></span>

<span data-ttu-id="2c8e2-110">Actualise Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-110">hello Azure Portal will refresh.</span></span>  <span data-ttu-id="2c8e2-111">Maintenant, vous êtes connecté à hello portail Azure dans le contexte de hello de votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-111">Now you are signed into hello Azure Portal in hello context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-toohello-b2c-features-blade"></a><span data-ttu-id="2c8e2-112">Accédez Panneau de fonctionnalités toohello B2C</span><span class="sxs-lookup"><span data-stu-id="2c8e2-112">Navigate toohello B2C features blade</span></span>

1. <span data-ttu-id="2c8e2-113">Cliquez sur **Parcourir** sur la navigation de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-113">Click **Browse** on hello left hand navigation.</span></span>
1. <span data-ttu-id="2c8e2-114">Cliquez sur **> davantage de services** , puis recherchez `Azure AD B2C` dans le volet de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-114">Click **> More services** and then search for `Azure AD B2C` in hello left navigation pane.</span></span>  <span data-ttu-id="2c8e2-115">(toopin tooyour gauche tableau d’accueil, cliquez sur à gauche en étoile toohello hello d’Azure AD B2C)</span><span class="sxs-lookup"><span data-stu-id="2c8e2-115">(toopin tooyour left-hand Startboard, click hello star toohello left of Azure AD B2C)</span></span>
1. <span data-ttu-id="2c8e2-116">Cliquez sur **Azure AD B2C** tooaccess hello Panneau de fonctionnalités B2C.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-116">Click **Azure AD B2C** tooaccess hello B2C features blade.</span></span>
   
    ![Capture d’écran du Panneau de navigation tooB2C fonctionnalités](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="2c8e2-118">Vous devez toobe un administrateur Global du panneau des fonctionnalités hello B2C locataire toobe tooaccess en mesure de hello B2C.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-118">You need toobe a Global Administrator of hello B2C tenant toobe able tooaccess hello B2C features blade.</span></span> <span data-ttu-id="2c8e2-119">L’administrateur général ou l’utilisateur de tout autre client ne pourra pas y accéder.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="2c8e2-120">Vous pouvez basculer tooyour B2C client à l’aide du sélecteur de locataire hello dans hello coin supérieur droit de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2c8e2-120">You can switch tooyour B2C tenant by using hello tenant switcher in hello top right corner of hello Azure portal.</span></span>
