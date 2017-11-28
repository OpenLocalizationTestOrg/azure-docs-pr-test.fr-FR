---
title: "aaaManage vos paramètres de vérification en deux étapes | Documents Microsoft"
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
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="aeea3-104">Gérer les paramètres de la vérification en deux étapes</span><span class="sxs-lookup"><span data-stu-id="aeea3-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="aeea3-105">Cet article répond aux questions concernant les paramètres de tooupdate pour l’authentification multifacteur ou de vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="aeea3-105">This article answers questions about how tooupdate settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="aeea3-106">Si vous rencontrez des problèmes de connexion tooyour compte, consultez trop[rencontre des problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md) pour la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="aeea3-106">If you are having issues signing in tooyour account, refer too[Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-toofind-hello-settings-page"></a><span data-ttu-id="aeea3-107">Où toofind hello page Paramètres</span><span class="sxs-lookup"><span data-stu-id="aeea3-107">Where toofind hello settings page</span></span>
<span data-ttu-id="aeea3-108">Selon la façon dont vous utilisez Azure Multi-Factor Authentication, vous pouvez modifier vos paramètres (comme votre numéro de téléphone) de différentes manières.</span><span class="sxs-lookup"><span data-stu-id="aeea3-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="aeea3-109">Si votre administrateur informatique envoyé une URL spécifique ou de la vérification en deux étapes de toomanage étapes, suivez ces instructions.</span><span class="sxs-lookup"><span data-stu-id="aeea3-109">If your IT admin sent out a specific URL or steps toomanage two-step verification, follow those instructions.</span></span> <span data-ttu-id="aeea3-110">Dans le cas contraire, suivant les instructions de hello doit fonctionner pour les autres.</span><span class="sxs-lookup"><span data-stu-id="aeea3-110">Otherwise, hello following instructions should work for everybody else.</span></span> <span data-ttu-id="aeea3-111">Si vous suivez ces étapes, mais ne pas afficher hello les mêmes options, ce qui signifie que votre entreprise ou école portail personnalisé de leur propres.</span><span class="sxs-lookup"><span data-stu-id="aeea3-111">If you follow these steps but don't see hello same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="aeea3-112">Demandez à votre administrateur pour le portail de l’authentification multifacteur Azure hello lien tooyour.</span><span class="sxs-lookup"><span data-stu-id="aeea3-112">Ask your admin for hello link tooyour Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="aeea3-113">Connectez-vous trop[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="aeea3-113">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="aeea3-114">Sélectionnez le nom de votre compte dans hello en haut à droite, puis sélectionnez **profil**.</span><span class="sxs-lookup"><span data-stu-id="aeea3-114">Select your account name in hello top right, then select **profile**.</span></span>  
3. <span data-ttu-id="aeea3-115">Sélectionnez **Vérification de sécurité supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="aeea3-115">Select **Additional security verification**.</span></span>  

    ![MyApps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="aeea3-117">charge de la page de vérification de sécurité supplémentaires de Hello avec vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="aeea3-117">hello Additional security verification page loads with your settings.</span></span>

    ![Vérification](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="aeea3-119">Souhaitée toochange mon numéro de téléphone, ou ajouter un numéro secondaire</span><span class="sxs-lookup"><span data-stu-id="aeea3-119">I want toochange my phone number, or add a secondary number</span></span>
<span data-ttu-id="aeea3-120">Il est important tooconfigure un numéro de téléphone d’authentification secondaire.</span><span class="sxs-lookup"><span data-stu-id="aeea3-120">It is important tooconfigure a secondary authentication phone number.</span></span>  <span data-ttu-id="aeea3-121">Étant donné que le nombre et votre application mobile de téléphone de votre serveur principal sont probablement sur hello même de téléphone, numéro de téléphone secondaire de hello est le seul moyen de la hello vous serez en mesure de tooget dans votre compte si votre téléphone est perdu ou volé.</span><span class="sxs-lookup"><span data-stu-id="aeea3-121">Because your primary phone number and your mobile app are probably on hello same phone, hello secondary phone number is hello only way you will be able tooget back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="aeea3-122">Si vous n’ont le numéro de téléphone principal accès tooyour et avez besoin d’aide dans tooyour compte, consultez notre rubriques d’aide dans [rencontre des problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="aeea3-122">If you don't have access tooyour primary phone number, and need help getting in tooyour account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="aeea3-123">**toochange numéro de téléphone de votre serveur principal :**</span><span class="sxs-lookup"><span data-stu-id="aeea3-123">**toochange your primary phone number:**</span></span>  

1. <span data-ttu-id="aeea3-124">Sur la page de vérification de sécurité supplémentaires de hello, sélectionnez la zone de texte hello avec votre numéro de téléphone et le modifier avec votre nouveau numéro de téléphone.</span><span class="sxs-lookup"><span data-stu-id="aeea3-124">On hello Additional security verification page, select hello text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="aeea3-125">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="aeea3-125">Select **Save**.</span></span>  
3. <span data-ttu-id="aeea3-126">Numéro de hello que vous utilisez pour votre option préférée de vérification, vous avez nouveau numéro de tooverify hello avant que vous pouvez l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="aeea3-126">If this is hello number that you use for your preferred verification option, you have tooverify hello new number before you can save it.</span></span>  

<span data-ttu-id="aeea3-127">**tooadd un numéro de téléphone secondaire :**</span><span class="sxs-lookup"><span data-stu-id="aeea3-127">**tooadd a secondary phone number:**</span></span>  

1. <span data-ttu-id="aeea3-128">Sur la page de vérification de sécurité supplémentaires de hello, hello case à cocher ensuite trop**autre téléphone d’authentification.**</span><span class="sxs-lookup"><span data-stu-id="aeea3-128">On hello Additional security verification page, check hello box next too**Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="aeea3-129">Entrez votre numéro de téléphone secondaire dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="aeea3-129">Enter your secondary phone number in hello text box.</span></span>  
3. <span data-ttu-id="aeea3-130">Sélectionnez **Enregistrer**. Vos modifications sont apportées.</span><span class="sxs-lookup"><span data-stu-id="aeea3-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="aeea3-131">Exiger une nouvelle vérification en deux étapes sur un appareil marqué comme approuvé</span><span class="sxs-lookup"><span data-stu-id="aeea3-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="aeea3-132">Selon les paramètres de votre organisation, vous pouvez disposer d’une case à cocher libellée « Ne plus me le demander pendant **X** jours » lorsque vous effectuez une vérification en deux étapes sur votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="aeea3-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="aeea3-133">Si vous activez cette case à cocher et perdez votre appareil ou pensez que votre compte est compromis, vous devez restaurer vos appareils tooall de vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="aeea3-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification tooall your devices.</span></span> 

1. <span data-ttu-id="aeea3-134">Sur la page de vérification de sécurité supplémentaires de hello, sélectionnez **l’authentification multifacteur de restauration sur les appareils déjà de confiance**.</span><span class="sxs-lookup"><span data-stu-id="aeea3-134">On hello Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="aeea3-135">Hello prochaine que connexion sur n’importe quel appareil, vous serez invité à tooperform en deux étapes vérification.</span><span class="sxs-lookup"><span data-stu-id="aeea3-135">hello next time you sign in on any device, you'll be prompted tooperform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a><span data-ttu-id="aeea3-136">Comment nettoyer Microsoft Authenticator à partir de mon appareil ancien et déplacer tooa nouveau ?</span><span class="sxs-lookup"><span data-stu-id="aeea3-136">How do I clean up Microsoft Authenticator from my old device and move tooa new one?</span></span>
<span data-ttu-id="aeea3-137">Lorsque vous désinstallez l’application hello à partir de votre appareil ou un périphérique hello de réinitialisation, elle ne supprime pas l’activation de hello principal hello.</span><span class="sxs-lookup"><span data-stu-id="aeea3-137">When you uninstall hello app from your device or reset hello device, it does not remove hello activation on hello back end.</span></span> <span data-ttu-id="aeea3-138">Pour plus d’informations, consultez [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="aeea3-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeea3-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aeea3-139">Next steps</span></span>
* <span data-ttu-id="aeea3-140">Obtenir des conseils de dépannage et de l’aide dans [Problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="aeea3-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="aeea3-141">Configurer des [mots de passe d’application](multi-factor-authentication-end-user-app-passwords.md) pour les applications qui ne prennent pas en charge la vérification en deux étapes</span><span class="sxs-lookup"><span data-stu-id="aeea3-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
