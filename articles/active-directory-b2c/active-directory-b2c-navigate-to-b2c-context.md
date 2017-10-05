---
title: "Azure Active Directory B2C : Basculement vers un locataire B2C | Microsoft Docs"
description: "Comment basculer dans le contexte de votre locataire Active Directory B2C"
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
ms.openlocfilehash: 40d8d57d974a949fbdc0a06eeceb2d06bfbaa09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="switching-to-your-azure-ad-b2c-tenant"></a><span data-ttu-id="d2e56-103">Basculement vers votre locataire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d2e56-103">Switching to your Azure AD B2C tenant</span></span>

<span data-ttu-id="d2e56-104">Pour configurer Azure AD B2C, vous devez vous trouver dans le contexte de votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d2e56-104">In order to configure Azure AD B2C, you need to be in the context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="d2e56-105">Se connecter au locataire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d2e56-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="d2e56-106">Pour accéder à votre locataire Azure AD B2C, vous devez être connecté au portail Azure en tant qu’administrateur général du locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d2e56-106">To navigate to your Azure AD B2C tenant, you must be logged into the Azure portal as a global administrator of the Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="d2e56-107">Connectez-vous au [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2e56-107">Sign into the [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="d2e56-108">Basculez les locataires en cliquant sur votre adresse de messagerie ou sur l’image dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="d2e56-108">Switch tenants by clicking your email address or picture in the top-right corner.</span></span>
1. <span data-ttu-id="d2e56-109">Dans la liste `Directory` qui s’affiche, sélectionnez le locataire Azure AD B2C que vous souhaitez gérer.</span><span class="sxs-lookup"><span data-stu-id="d2e56-109">In the `Directory` list that appears, select the Azure AD B2C tenant that you wish to manage.</span></span>

<span data-ttu-id="d2e56-110">Le portail Azure s’actualise.</span><span class="sxs-lookup"><span data-stu-id="d2e56-110">The Azure Portal will refresh.</span></span>  <span data-ttu-id="d2e56-111">Vous êtes à présent connecté au portail Azure dans le contexte de votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d2e56-111">Now you are signed into the Azure Portal in the context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-to-the-b2c-features-blade"></a><span data-ttu-id="d2e56-112">Accéder au panneau de fonctionnalités B2C</span><span class="sxs-lookup"><span data-stu-id="d2e56-112">Navigate to the B2C features blade</span></span>

1. <span data-ttu-id="d2e56-113">Cliquez sur **Parcourir** dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="d2e56-113">Click **Browse** on the left hand navigation.</span></span>
1. <span data-ttu-id="d2e56-114">Cliquez sur **> Plus de services**, puis recherchez `Azure AD B2C` dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="d2e56-114">Click **> More services** and then search for `Azure AD B2C` in the left navigation pane.</span></span>  <span data-ttu-id="d2e56-115">(Pour l’épingler à votre Tableau d’accueil sur la gauche, cliquez sur l’étoile située à gauche d’Azure AD B2C.)</span><span class="sxs-lookup"><span data-stu-id="d2e56-115">(To pin to your left-hand Startboard, click the star to the left of Azure AD B2C)</span></span>
1. <span data-ttu-id="d2e56-116">Cliquez sur **Azure AD B2C** pour accéder au panneau de fonctionnalités B2C.</span><span class="sxs-lookup"><span data-stu-id="d2e56-116">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![Capture d’écran du bouton Parcourir du panneau de fonctionnalités B2C](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="d2e56-118">Vous devez être administrateur général du client B2C pour accéder au volet des fonctionnalités B2C.</span><span class="sxs-lookup"><span data-stu-id="d2e56-118">You need to be a Global Administrator of the B2C tenant to be able to access the B2C features blade.</span></span> <span data-ttu-id="d2e56-119">L’administrateur général ou l’utilisateur de tout autre client ne pourra pas y accéder.</span><span class="sxs-lookup"><span data-stu-id="d2e56-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="d2e56-120">Vous pouvez basculer vers votre client B2C en utilisant le sélecteur de client dans le coin supérieur droit du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d2e56-120">You can switch to your B2C tenant by using the tenant switcher in the top right corner of the Azure portal.</span></span>
