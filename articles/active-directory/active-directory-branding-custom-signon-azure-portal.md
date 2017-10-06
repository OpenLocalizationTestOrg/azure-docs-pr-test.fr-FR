---
title: "aaaCustomize vous connecter à la page Bonjour Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooadd une page toohello connectez-vous Azure marque de société"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="19ae0-103">Ajouter des logos tooyour-page de connexion Bonjour Azure Active Directory de la société</span><span class="sxs-lookup"><span data-stu-id="19ae0-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="19ae0-104">tooavoid confusion, de nombreuses sociétés souhaitent tooapply une apparence cohérente sur tous les sites Web de hello et services qu’ils gèrent.</span><span class="sxs-lookup"><span data-stu-id="19ae0-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="19ae0-105">Azure Active Directory offre cette possibilité en vous donnant l’apparence de hello toocustomize de hello-page de connexion avec votre logo de l’entreprise et les jeux de couleurs personnalisées.</span><span class="sxs-lookup"><span data-stu-id="19ae0-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="19ae0-106">page de connexion Hello est page hello qui s’affiche lorsque vous vous connectez tooOffice 365 ou autres applications web qui utilisent Azure AD comme fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="19ae0-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="19ae0-107">Vous interagissez avec cette tooenter page vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="19ae0-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="19ae0-108">Si vous souhaitez tooshow marque de votre société, les couleurs et les autres éléments personnalisables sur cette page, consultez hello suivant images toounderstand hello différence deux expériences de hello.</span><span class="sxs-lookup"><span data-stu-id="19ae0-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="19ae0-109">Hello capture d’écran affiche et l’exemple hello Office 365-page de connexion sur un ordinateur de bureau **avant** une personnalisation :</span><span class="sxs-lookup"><span data-stu-id="19ae0-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Page de connexion Office 365 avant la personnalisation](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="19ae0-111">Hello capture d’écran affiche et l’exemple hello Office 365-page de connexion sur un ordinateur de bureau **après** une personnalisation :</span><span class="sxs-lookup"><span data-stu-id="19ae0-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Page de connexion d’Office 365 après la personnalisation](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="19ae0-113">Personnalisation de hello-page de connexion</span><span class="sxs-lookup"><span data-stu-id="19ae0-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="19ae0-114">En règle générale, si vous avez besoin d’accès basé sur un navigateur tooyour applications et services cloud que votre organisation est abonnée à, vous utilisez hello-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="19ae0-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="19ae0-115">Si vous avez appliqué les modifications tooyour-page de connexion, il peut prendre les horaires de tooan pour tooappear de modifications hello.</span><span class="sxs-lookup"><span data-stu-id="19ae0-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="19ae0-116">Une page de connexion personnalisée s’affiche uniquement lorsque vous accédez à un service avec une URL spécifique au client, telle que https://outlook.com/**contoso**.com, ou https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="19ae0-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="19ae0-117">Lorsque vous visitez un service avec une URL non spécifique au client (par exemple : https://mail.office365.com), une page de connexion non personnalisée s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19ae0-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="19ae0-118">Dans ce cas, votre marque apparaît une fois que vous avez entré votre ID d’utilisateur ou que vous avez sélectionné une vignette utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19ae0-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="19ae0-119">Votre nom de domaine doit être « Actif » dans hello **domaines** partie de hello portail Azure, dans lequel vous avez effectué la personnalisation.</span><span class="sxs-lookup"><span data-stu-id="19ae0-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="19ae0-120">Pour plus d’informations, consultez [Ajouter des noms de domaine personnalisés](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="19ae0-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="19ae0-121">Personnalisation de la page de connexion n’est pas reflétée sur la page de Microsoft de connexion consommateur toohello.</span><span class="sxs-lookup"><span data-stu-id="19ae0-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="19ae0-122">Si vous vous connectez avec un compte Microsoft, vous pouvez voir une liste personnalisée de vignettes utilisateur rendues par Azure AD, mais toohello Microsoft compte-page de connexion ne s’applique pas hello de personnalisation de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="19ae0-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="19ae0-123">Sur votre page de connexion, hello **maintenir la connexion** case à cocher permet un tooremain utilisateur connecté lorsqu’ils ferment et rouvrir leur navigateur.</span><span class="sxs-lookup"><span data-stu-id="19ae0-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![Maintenir la connexion](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="19ae0-125">Elle n’a pas d’effet sur la durée de vie de session.</span><span class="sxs-lookup"><span data-stu-id="19ae0-125">It does not effect session lifetime.</span></span> <span data-ttu-id="19ae0-126">Vous pouvez masquer la case à cocher hello sur hello Azure Active Directory-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="19ae0-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="19ae0-127">Si la case à cocher hello est affiché en fonction de définition de hello de **maintenir la connexion désactivée**.</span><span class="sxs-lookup"><span data-stu-id="19ae0-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![Maintenir la connexion](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="19ae0-129">toohide hello case à cocher, configurez ce paramètre trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="19ae0-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="19ae0-130">Certaines fonctionnalités de SharePoint Online et Office 2010 dépendent des utilisateurs en mesure de toocheck cette case.</span><span class="sxs-lookup"><span data-stu-id="19ae0-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="19ae0-131">Si vous configurez ce paramètre toohidden, vos utilisateurs peuvent voir des invites de supplémentaires et inattendues dans toosign.</span><span class="sxs-lookup"><span data-stu-id="19ae0-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="19ae0-132">**marque active de tooyour de l’entreprise de tooadd :**</span><span class="sxs-lookup"><span data-stu-id="19ae0-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="19ae0-133">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="19ae0-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="19ae0-134">Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="19ae0-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="19ae0-136">Sur hello **utilisateurs et groupes** panneau, sélectionnez **de personnalisation de la société**.</span><span class="sxs-lookup"><span data-stu-id="19ae0-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="19ae0-137">Sur hello **utilisateurs et groupes - personnalisation de la société** panneau, sélectionnez hello **modifier** commande.</span><span class="sxs-lookup"><span data-stu-id="19ae0-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![Modifier la personnalisation de société](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="19ae0-139">Modifier les éléments hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="19ae0-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="19ae0-140">Tous ces éléments sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="19ae0-140">All elements are optional.</span></span>
6. <span data-ttu-id="19ae0-141">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="19ae0-141">Click **Save**.</span></span>

<span data-ttu-id="19ae0-142">Pour les modifications éventuelles apportées toohello connectez-vous page tooappear marque peut prendre jusqu'à tooan heure.</span><span class="sxs-lookup"><span data-stu-id="19ae0-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19ae0-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19ae0-143">Next steps</span></span>
[<span data-ttu-id="19ae0-144">Ajouter la marque de l’entreprise spécifique à une langue</span><span class="sxs-lookup"><span data-stu-id="19ae0-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
