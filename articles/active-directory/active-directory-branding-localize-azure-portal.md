---
title: "aaaAdd spécifiques au langage logos de la société tooyour-page de connexion Bonjour Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooadd une langue spécifique et entreprise images marque la page de texte tooan signe dans Azure"
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
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="c08ba-103">Ajouter la marque tooyour-page de connexion Bonjour Azure Active Directory de l’entreprise spécifiques au langage</span><span class="sxs-lookup"><span data-stu-id="c08ba-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="c08ba-104">tooavoid confusion, de nombreuses sociétés souhaitent tooapply une apparence cohérente sur tous les sites Web de hello et services qu’ils gèrent.</span><span class="sxs-lookup"><span data-stu-id="c08ba-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="c08ba-105">Azure Active Directory offre cette possibilité en vous donnant l’apparence de hello toocustomize de hello-page de connexion avec votre logo de l’entreprise et les jeux de couleurs personnalisées.</span><span class="sxs-lookup"><span data-stu-id="c08ba-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="c08ba-106">page de connexion Hello est page hello qui s’affiche lorsque vous vous connectez tooOffice 365 ou autres applications web qui utilisent Azure AD comme fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="c08ba-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="c08ba-107">Vous interagissez avec cette tooenter page vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="c08ba-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="c08ba-108">Personnalisation de hello-page de connexion pour une autre langue</span><span class="sxs-lookup"><span data-stu-id="c08ba-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="c08ba-109">Vous pouvez ajouter des éléments spécifiques au langage tooyour personnalisé-page de connexion uniquement si vous avez déjà créé une page de connexion personnalisée comme décrit dans [ajouter marque tooyour-page de connexion de l’entreprise](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c08ba-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="c08ba-110">Vous pouvez configurer une page de connexion par répertoire avec un jeu d’éléments personnalisables par défaut.</span><span class="sxs-lookup"><span data-stu-id="c08ba-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="c08ba-111">Une fois que vous avez configuré l’ensemble par défaut de hello des éléments de page, vous pouvez configurer plus de versions pour différents paramètres régionaux.</span><span class="sxs-lookup"><span data-stu-id="c08ba-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="c08ba-112">Vous pouvez également combiner différents éléments.</span><span class="sxs-lookup"><span data-stu-id="c08ba-112">You can also mix and match various elements.</span></span> <span data-ttu-id="c08ba-113">Par exemple, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="c08ba-113">For example, you could:</span></span>

* <span data-ttu-id="c08ba-114">Créez une **Image de page de connexion** par défaut adaptée à toutes les cultures, puis créez des versions spécifiques pour l’anglais et le français.</span><span class="sxs-lookup"><span data-stu-id="c08ba-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="c08ba-115">Lorsque vous définissez votre tooone navigateurs de ces deux langues, hello spécifiques au langage image s’affiche, tandis que l’illustration de hello par défaut s’affiche pour tous les autres langages.</span><span class="sxs-lookup"><span data-stu-id="c08ba-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="c08ba-116">Configurez différents logos pour votre organisation (par exemple, des versions en japonais ou en hébreu).</span><span class="sxs-lookup"><span data-stu-id="c08ba-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="c08ba-117">Nous recommandons de conserver plusieurs hello variantes de langage faible, pour des raisons de maintenance et les performances.</span><span class="sxs-lookup"><span data-stu-id="c08ba-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="c08ba-118">**marque active de tooyour de l’entreprise de tooadd :**</span><span class="sxs-lookup"><span data-stu-id="c08ba-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="c08ba-119">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="c08ba-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="c08ba-120">Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="c08ba-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="c08ba-122">Sur hello **utilisateurs et groupes** panneau, sélectionnez **de personnalisation de la société**.</span><span class="sxs-lookup"><span data-stu-id="c08ba-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="c08ba-123">Sur hello **utilisateurs et groupes - personnalisation de la société** panneau, sélectionnez hello **Ajouter langue** commande.</span><span class="sxs-lookup"><span data-stu-id="c08ba-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![Ajouter des éléments spécifiques à une langue](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="c08ba-125">Modifier les éléments hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="c08ba-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="c08ba-126">Tous ces éléments sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="c08ba-126">All elements are optional.</span></span>
6. <span data-ttu-id="c08ba-127">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c08ba-127">Click **Save**.</span></span>

<span data-ttu-id="c08ba-128">Pour les modifications éventuelles apportées toohello connectez-vous page tooappear marque peut prendre jusqu'à tooan heure.</span><span class="sxs-lookup"><span data-stu-id="c08ba-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c08ba-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c08ba-129">Next steps</span></span>
[<span data-ttu-id="c08ba-130">Ajouter des logos tooyour-page de connexion de la société</span><span class="sxs-lookup"><span data-stu-id="c08ba-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
