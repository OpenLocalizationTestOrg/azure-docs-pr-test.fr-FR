---
title: Personnaliser votre page de connexion dans Azure Active Directory | Microsoft Docs
description: "Découvrir comment ajouter une société à la page de connexion Azure"
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
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="5d4af-103">Ajouter la personnalisation de votre société à votre page de connexion dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d4af-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="5d4af-104">Pour éviter toute confusion, de nombreuses entreprises veulent que tous les sites Web et services qu’elles gèrent aient un aspect similaire.</span><span class="sxs-lookup"><span data-stu-id="5d4af-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="5d4af-105">Azure Active Directory offre cette possibilité en vous permettant de personnaliser l’apparence la page de connexion pour qu’elle affiche le logo de votre société et sa palette de couleurs personnalisée.</span><span class="sxs-lookup"><span data-stu-id="5d4af-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="5d4af-106">La page de connexion s’affiche lorsque vous vous connectez à Office 365 ou à d’autres applications Web qui utilisent Azure AD comme fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="5d4af-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="5d4af-107">Vous interagissez avec cette page pour saisir vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="5d4af-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="5d4af-108">Si vous souhaitez afficher la marque, la palette de couleurs de votre société ou tout autre élément personnalisable sur cette page, reportez-vous aux images qui suivent pour comprendre la différence entre les deux.</span><span class="sxs-lookup"><span data-stu-id="5d4af-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="5d4af-109">La capture d’écran suivante montre un exemple de la page de connexion Office 365 sur un ordinateur de bureau **avant** une personnalisation :</span><span class="sxs-lookup"><span data-stu-id="5d4af-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Page de connexion Office 365 avant la personnalisation](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="5d4af-111">La capture d’écran suivante affiche l’exemple de la page de connexion Office 365 sur un ordinateur de bureau **après** une personnalisation :</span><span class="sxs-lookup"><span data-stu-id="5d4af-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Page de connexion d’Office 365 après la personnalisation](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="5d4af-113">Personnalisation de la page de connexion</span><span class="sxs-lookup"><span data-stu-id="5d4af-113">Customizing the sign-in page</span></span>
<span data-ttu-id="5d4af-114">En règle générale, vous utilisez la page de connexion pour accéder à l’aide d’un navigateur à vos applications et services cloud auxquels votre organisation est abonnée.</span><span class="sxs-lookup"><span data-stu-id="5d4af-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="5d4af-115">Lorsque vous apportez des modifications à votre page de connexion, un délai pouvant atteindre une heure peut être nécessaire pour qu’elles apparaissent.</span><span class="sxs-lookup"><span data-stu-id="5d4af-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="5d4af-116">Une page de connexion personnalisée s’affiche uniquement lorsque vous accédez à un service avec une URL spécifique au client, telle que https://outlook.com/**contoso**.com, ou https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="5d4af-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="5d4af-117">Lorsque vous visitez un service avec une URL non spécifique au client (par exemple : https://mail.office365.com), une page de connexion non personnalisée s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5d4af-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="5d4af-118">Dans ce cas, votre marque apparaît une fois que vous avez entré votre ID d’utilisateur ou que vous avez sélectionné une vignette utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5d4af-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="5d4af-119">Votre nom de domaine doit apparaître comme étant « Actif » dans la partie **Domaines** du portail Azure dans lequel vous avez effectué la personnalisation de société.</span><span class="sxs-lookup"><span data-stu-id="5d4af-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="5d4af-120">Pour plus d’informations, consultez [Ajouter des noms de domaine personnalisés](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5d4af-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="5d4af-121">La personnalisation de la page de connexion ne s’étend pas à la page de connexion client de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5d4af-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="5d4af-122">Si vous vous connectez avec un compte Microsoft, vous pouvez voir une liste personnalisée de vignettes utilisateur générées par Azure AD, mais la marque de votre organisation ne s’applique pas à la page de connexion du compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5d4af-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="5d4af-123">Sur votre page de connexion, la case à cocher **Maintenir la connexion** permet à un utilisateur de rester connecté lorsqu’il ferme, puis rouvre son navigateur.</span><span class="sxs-lookup"><span data-stu-id="5d4af-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![Maintenir la connexion](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="5d4af-125">Elle n’a pas d’effet sur la durée de vie de session.</span><span class="sxs-lookup"><span data-stu-id="5d4af-125">It does not effect session lifetime.</span></span> <span data-ttu-id="5d4af-126">Vous pouvez masquer la case à cocher sur la page de connexion Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d4af-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="5d4af-127">L’affichage de la case à cocher dépend du réglage du paramètre **Maintien de la connexion désactivé**.</span><span class="sxs-lookup"><span data-stu-id="5d4af-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![Maintenir la connexion](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="5d4af-129">Pour masquer la case à cocher, configurez ce paramètre sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="5d4af-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="5d4af-130">Certaines fonctionnalités de SharePoint Online et Office 2010 dépendent de la capacité des utilisateurs à sélectionner cette case à cocher.</span><span class="sxs-lookup"><span data-stu-id="5d4af-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="5d4af-131">Si vous configurez ce paramètre sur Masqué, il se peut que vos utilisateurs voient des invites de connexion supplémentaires et inattendues.</span><span class="sxs-lookup"><span data-stu-id="5d4af-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="5d4af-132">**Pour ajouter votre marque à l’annuaire :**</span><span class="sxs-lookup"><span data-stu-id="5d4af-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="5d4af-133">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="5d4af-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="5d4af-134">Sélectionnez **Plus de services**, saisissez **Utilisateurs et groupes** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="5d4af-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="5d4af-136">Sur le panneau **Utilisateurs et groupes** panneau, sélectionnez **Personnalisation de société**.</span><span class="sxs-lookup"><span data-stu-id="5d4af-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="5d4af-137">Sur le panneau **Utilisateurs et groupes - Personnalisation de la société**, sélectionnez la commande **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="5d4af-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![Modifier la personnalisation de société](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="5d4af-139">Modifiez les éléments que vous voulez personnaliser.</span><span class="sxs-lookup"><span data-stu-id="5d4af-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="5d4af-140">Tous ces éléments sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="5d4af-140">All elements are optional.</span></span>
6. <span data-ttu-id="5d4af-141">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="5d4af-141">Click **Save**.</span></span>

<span data-ttu-id="5d4af-142">Il peut s’écouler jusqu’à une heure avant que les modifications que vous avez apportées à la page de connexion soient visibles.</span><span class="sxs-lookup"><span data-stu-id="5d4af-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d4af-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5d4af-143">Next steps</span></span>
[<span data-ttu-id="5d4af-144">Ajouter la marque de l’entreprise spécifique à une langue</span><span class="sxs-lookup"><span data-stu-id="5d4af-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
