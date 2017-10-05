---
title: "Gérer les paramètres de la vérification en deux étapes | Microsoft Docs"
description: "Gérez l’utilisation d’Azure Multi-Factor Authentication, notamment la modification des informations de contact ou la configuration des appareils."
services: multi-factor-authentication
keywords: "client de l'authentification multifacteur, problème d'authentification, ID de corrélation"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="424f9-104">Gérer les paramètres de la vérification en deux étapes</span><span class="sxs-lookup"><span data-stu-id="424f9-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="424f9-105">Cet article répond aux questions en rapport avec la mise à jour des paramètres de Multi-Factor Authentication ou de la vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="424f9-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="424f9-106">Si vous rencontrez des problèmes de connexion à votre compte, consultez [Problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md) pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="424f9-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="424f9-107">Où trouver la page des paramètres</span><span class="sxs-lookup"><span data-stu-id="424f9-107">Where to find the settings page</span></span>
<span data-ttu-id="424f9-108">Selon la façon dont vous utilisez Azure Multi-Factor Authentication, vous pouvez modifier vos paramètres (comme votre numéro de téléphone) de différentes manières.</span><span class="sxs-lookup"><span data-stu-id="424f9-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="424f9-109">Si votre administrateur informatique vous a envoyé une URL spécifique ou des étapes pour gérer la vérification en deux étapes, suivez ces instructions.</span><span class="sxs-lookup"><span data-stu-id="424f9-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="424f9-110">Dans le cas contraire, suivez celles indiquées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="424f9-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="424f9-111">Si vous effectuez ces étapes et que vous ne voyez pas les mêmes options, cela signifie que votre entreprise ou établissement scolaire a personnalisé le portail.</span><span class="sxs-lookup"><span data-stu-id="424f9-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="424f9-112">Demandez à l’administrateur de vous donner le lien à votre portail Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="424f9-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="424f9-113">Connectez-vous à [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="424f9-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="424f9-114">Sélectionnez votre nom de compte dans la partie supérieure droite, puis sélectionnez **profil**.</span><span class="sxs-lookup"><span data-stu-id="424f9-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="424f9-115">Sélectionnez **Vérification de sécurité supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="424f9-115">Select **Additional security verification**.</span></span>  

    ![MyApps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="424f9-117">La page Vérification de sécurité supplémentaire se charge avec vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="424f9-117">The Additional security verification page loads with your settings.</span></span>

    ![Vérification](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="424f9-119">Je souhaite modifier mon numéro de téléphone ou ajouter un numéro secondaire</span><span class="sxs-lookup"><span data-stu-id="424f9-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="424f9-120">Il est important de configurer un numéro de téléphone d’authentification secondaire.</span><span class="sxs-lookup"><span data-stu-id="424f9-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="424f9-121">Étant donné que vous utilisez probablement le même téléphone pour votre numéro de téléphone principal et votre application mobile, le numéro de téléphone secondaire est le seul moyen dont vous disposez pour revenir à votre compte en cas de perte ou de vol de votre téléphone.</span><span class="sxs-lookup"><span data-stu-id="424f9-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="424f9-122">Si vous n’avez pas accès à votre numéro de téléphone principal et que vous avez besoin d’aide pour accéder à votre compte, consultez nos rubriques d’aide dans [Problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="424f9-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="424f9-123">**Pour modifier votre numéro de téléphone principal :**</span><span class="sxs-lookup"><span data-stu-id="424f9-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="424f9-124">Dans la page Vérification de sécurité supplémentaire, sélectionnez la zone de texte contenant votre numéro de téléphone et tapez votre nouveau numéro.</span><span class="sxs-lookup"><span data-stu-id="424f9-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="424f9-125">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="424f9-125">Select **Save**.</span></span>  
3. <span data-ttu-id="424f9-126">Si ce numéro constitue votre option de vérification préférée, vous devez vérifier le nouveau numéro avant de pouvoir l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="424f9-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="424f9-127">**Pour ajouter un numéro de téléphone secondaire :**</span><span class="sxs-lookup"><span data-stu-id="424f9-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="424f9-128">Dans la page Vérification de sécurité supplémentaire, cochez la case **Autre téléphone d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="424f9-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="424f9-129">Entrez votre numéro de téléphone secondaire dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="424f9-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="424f9-130">Sélectionnez **Enregistrer**. Vos modifications sont apportées.</span><span class="sxs-lookup"><span data-stu-id="424f9-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="424f9-131">Exiger une nouvelle vérification en deux étapes sur un appareil marqué comme approuvé</span><span class="sxs-lookup"><span data-stu-id="424f9-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="424f9-132">Selon les paramètres de votre organisation, vous pouvez disposer d’une case à cocher libellée « Ne plus me le demander pendant **X** jours » lorsque vous effectuez une vérification en deux étapes sur votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="424f9-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="424f9-133">Si vous cochez cette case, puis que vous perdez votre appareil ou que vous pensez que l’intégrité de votre compte est compromise, vous devez restaurer la vérification en deux étapes pour tous vos appareils.</span><span class="sxs-lookup"><span data-stu-id="424f9-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="424f9-134">Sur la page de vérification de sécurité supplémentaire, sélectionnez l’option **Restaurer Multi-Factor Authentication sur des appareils précédemment définis comme étant de confiance**.</span><span class="sxs-lookup"><span data-stu-id="424f9-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="424f9-135">La prochaine fois que vous vous connecterez sur l’un des appareils, vous serez invité à effectuer une vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="424f9-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="424f9-136">Comment nettoyer Microsoft Authenticator sur mon ancien appareil et le transférer vers un autre ?</span><span class="sxs-lookup"><span data-stu-id="424f9-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="424f9-137">Quand vous désinstallez l’application de votre appareil ou que vous réinitialisez ce dernier, l’application n’est pas désactivée sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="424f9-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="424f9-138">Pour plus d’informations, consultez [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="424f9-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="424f9-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="424f9-139">Next steps</span></span>
* <span data-ttu-id="424f9-140">Obtenir des conseils de dépannage et de l’aide dans [Problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="424f9-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="424f9-141">Configurer des [mots de passe d’application](multi-factor-authentication-end-user-app-passwords.md) pour les applications qui ne prennent pas en charge la vérification en deux étapes</span><span class="sxs-lookup"><span data-stu-id="424f9-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
