---
title: "Ajouter la personnalisation de votre société spécifique à une langue à votre page de connexion dans Azure Active Directory | Microsoft Docs"
description: "Découvrez comment ajouter des images et du texte de la société dans une langue spécifique à une page de connexion Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="6ac1e-103">Ajouter la personnalisation de votre société spécifique à une langue à votre page de connexion dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ac1e-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="6ac1e-104">Pour éviter toute confusion, de nombreuses entreprises veulent que tous les sites Web et services qu’elles gèrent aient un aspect similaire.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="6ac1e-105">Azure Active Directory offre cette possibilité en vous permettant de personnaliser l’apparence la page de connexion pour qu’elle affiche le logo de votre société et sa palette de couleurs personnalisée.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="6ac1e-106">La page de connexion s’affiche lorsque vous vous connectez à Office 365 ou à d’autres applications Web qui utilisent Azure AD comme fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="6ac1e-107">Vous interagissez avec cette page pour saisir vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="6ac1e-108">Personnalisation de la page de connexion pour une autre langue</span><span class="sxs-lookup"><span data-stu-id="6ac1e-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="6ac1e-109">Vous pouvez ajouter des éléments de langage spécifiques à votre page de connexion personnalisée uniquement si vous avez déjà créé une page de connexion personnalisée, comme décrit dans [Ajouter votre marque à votre page de connexion](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6ac1e-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="6ac1e-110">Vous pouvez configurer une page de connexion par répertoire avec un jeu d’éléments personnalisables par défaut.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="6ac1e-111">Une fois que vous avez configuré un jeu d’éléments de la page « par défaut », vous pouvez configurer des versions supplémentaires avec différents paramètres régionaux.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="6ac1e-112">Vous pouvez également combiner différents éléments.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-112">You can also mix and match various elements.</span></span> <span data-ttu-id="6ac1e-113">Par exemple, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="6ac1e-113">For example, you could:</span></span>

* <span data-ttu-id="6ac1e-114">Créez une **Image de page de connexion** par défaut adaptée à toutes les cultures, puis créez des versions spécifiques pour l’anglais et le français.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="6ac1e-115">Lorsque vous définissez vos navigateurs sur l’une de ces deux langues, l’image spécifique à la langue s’affiche, tandis que l’illustration par défaut apparaît pour toutes les autres langues.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="6ac1e-116">Configurez différents logos pour votre organisation (par exemple, des versions en japonais ou en hébreu).</span><span class="sxs-lookup"><span data-stu-id="6ac1e-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="6ac1e-117">Nous vous recommandons de garder un nombre raisonnable de variantes de langue, pour des raisons de performances et de maintenance.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="6ac1e-118">**Pour ajouter votre marque à l’annuaire :**</span><span class="sxs-lookup"><span data-stu-id="6ac1e-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="6ac1e-119">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="6ac1e-120">Sélectionnez **Plus de services**, saisissez **Utilisateurs et groupes** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="6ac1e-122">Sur le panneau **Utilisateurs et groupes** panneau, sélectionnez **Personnalisation de société**.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="6ac1e-123">Sur le panneau **Utilisateurs et groupes - Personnalisation de la société**, sélectionnez la commande **Ajouter une langue**.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![Ajouter des éléments spécifiques à une langue](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="6ac1e-125">Modifiez les éléments que vous voulez personnaliser.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="6ac1e-126">Tous ces éléments sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-126">All elements are optional.</span></span>
6. <span data-ttu-id="6ac1e-127">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-127">Click **Save**.</span></span>

<span data-ttu-id="6ac1e-128">Il peut s’écouler jusqu’à une heure avant que les modifications que vous avez apportées à la page de connexion soient visibles.</span><span class="sxs-lookup"><span data-stu-id="6ac1e-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ac1e-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ac1e-129">Next steps</span></span>
[<span data-ttu-id="6ac1e-130">Ajouter votre marque à votre page de connexion</span><span class="sxs-lookup"><span data-stu-id="6ac1e-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
