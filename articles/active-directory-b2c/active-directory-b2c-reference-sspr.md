---
title: "Azure Active Directory B2C : réinitialisation de mot de passe libre-service | Microsoft Docs"
description: "Rubrique montrant comment configurer une réinitialisation de mot de passe libre-service pour vos consommateurs dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="bdb0e-103">Azure Active Directory B2C : configuration de la réinitialisation du mot de passe libre-service pour vos consommateurs</span><span class="sxs-lookup"><span data-stu-id="bdb0e-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="bdb0e-104">La fonctionnalité de réinitialisation du mot de passe en libre-service permet à vos consommateurs (qui ont souscrit des comptes locaux) de réinitialiser eux-mêmes leurs mots de passe.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="bdb0e-105">Cela réduit considérablement la charge pesant sur votre personnel de support, surtout si votre application est utilisée régulièrement par des millions de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="bdb0e-106">Actuellement, nous prenons uniquement en charge l’utilisation d’une adresse électronique vérifiée comme méthode de récupération.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="bdb0e-107">Nous allons ajouter des méthodes de récupération supplémentaires (numéro de téléphone vérifié, questions de sécurité, etc.) à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb0e-108">Cet article s’applique à un mot de passe libre-service utilisé dans le contexte d’une stratégie de connexion.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="bdb0e-109">Si vous avez besoin de stratégies de réinitialisation de mot de passe entièrement personnalisables appelées à partir de votre application, consultez [cet article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="bdb0e-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="bdb0e-110">Par défaut, la réinitialisation de mot de passe libre-service ne sera pas activée pour votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="bdb0e-111">Pour l’activer, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bdb0e-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="bdb0e-112">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com/) en tant qu’administrateur d’abonnements.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="bdb0e-113">Il s’agit du compte professionnel ou scolaire, ou du compte Microsoft que vous avez utilisé pour créer votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="bdb0e-114">Accédez à l’extension Active Directory dans la barre de navigation sur le côté gauche.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="bdb0e-115">Recherchez votre répertoire sous l’onglet **Répertoire** , puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="bdb0e-116">Cliquez sur l'onglet **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="bdb0e-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="bdb0e-117">Faites défiler jusqu’à la section **Stratégie de réinitialisation du mot de passe utilisateur**, puis définissez l’option **Utilisateurs autorisés à réinitialiser leur mot de passe** sur **OUI**.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="bdb0e-118">Notez que l’option **Autre adresse de messagerie** est activée ; laissez-la telle quelle.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Réinitialisation de mot de passe libre-service](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="bdb0e-120">Cliquez sur **Enregistrer** au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="bdb0e-121">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="bdb0e-121">You're done!</span></span>

<span data-ttu-id="bdb0e-122">Pour tester, utilisez la fonctionnalité « Exécuter maintenant » sur une stratégie de connexion (qui comporte des comptes locaux en tant que fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="bdb0e-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="bdb0e-123">Sur la page de connexion au compte local (où vous entrez une adresse e-mail et un mot de passe, ou un nom d’utilisateur et un mot de passe), cliquez sur **Votre compte n’est pas accessible ?** pour vérifier l’expérience du consommateur.</span><span class="sxs-lookup"><span data-stu-id="bdb0e-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb0e-124">Les pages de réinitialisation de mot de passe libre-service sont personnalisables à l’aide de la [fonctionnalité de personnalisation de la société](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="bdb0e-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

