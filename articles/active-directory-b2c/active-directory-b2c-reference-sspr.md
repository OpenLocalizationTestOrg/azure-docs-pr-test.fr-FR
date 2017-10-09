---
title: "Azure Active Directory B2C : réinitialisation de mot de passe libre-service | Microsoft Docs"
description: "Une rubrique illustrant comment réinitialiser les tooset le mot de passe libre-service pour vos consommateurs dans Azure Active Directory B2C"
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
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="acec4-103">Azure Active Directory B2C : configuration de la réinitialisation du mot de passe libre-service pour vos consommateurs</span><span class="sxs-lookup"><span data-stu-id="acec4-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="acec4-104">Avec hello fonctionnalité de réinitialisation de mot de passe libre-service, vos consommateurs (qui se sont inscrites pour les comptes locaux) peuvent réinitialiser leurs mots de passe sur leurs propres.</span><span class="sxs-lookup"><span data-stu-id="acec4-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="acec4-105">Cela réduit considérablement la charge hello votre personnel de prise en charge, en particulier si votre application a des millions de consommateurs en l’utilisant sur une base régulière.</span><span class="sxs-lookup"><span data-stu-id="acec4-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="acec4-106">Actuellement, nous prenons uniquement en charge l’utilisation d’une adresse électronique vérifiée comme méthode de récupération.</span><span class="sxs-lookup"><span data-stu-id="acec4-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="acec4-107">Nous allons ajouter des méthodes de récupération supplémentaires (numéro de téléphone vérifié, les questions de sécurité, etc.) dans les futures hello.</span><span class="sxs-lookup"><span data-stu-id="acec4-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="acec4-108">Cet article s’applique à un mot de passe tooself service utilisée dans le contexte de hello d’une stratégie de réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="acec4-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="acec4-109">Si vous avez besoin de stratégies de réinitialisation de mot de passe entièrement personnalisables appelées à partir de votre application, consultez [cet article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="acec4-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="acec4-110">Par défaut, la réinitialisation de mot de passe libre-service ne sera pas activée pour votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="acec4-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="acec4-111">Utilisez hello suivant les étapes tooturn sur :</span><span class="sxs-lookup"><span data-stu-id="acec4-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="acec4-112">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) comme hello administrateur de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="acec4-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="acec4-113">Il s’agit de hello même travail ou scolaire compte ou hello du même compte Microsoft que vous avez utilisé toocreate votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="acec4-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="acec4-114">Accédez à extension d’Active Directory toohello sur la barre de navigation hello sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="acec4-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="acec4-115">Trouver votre répertoire sous hello **répertoire** onglet et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="acec4-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="acec4-116">Cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="acec4-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="acec4-117">Faites défiler vers le bas toohello **stratégie de réinitialisation du mot de passe utilisateur** hello section et bascule **les utilisateurs activés pour la réinitialisation du mot de passe** option trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="acec4-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="acec4-118">Notez que hello **autre adresse de messagerie** option est activée ; laisser car il s’agit.</span><span class="sxs-lookup"><span data-stu-id="acec4-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Réinitialisation de mot de passe libre-service](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="acec4-120">Cliquez sur **enregistrer** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="acec4-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="acec4-121">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="acec4-121">You're done!</span></span>

<span data-ttu-id="acec4-122">tootest, utiliser la fonctionnalité « Exécuter maintenant » hello sur toute stratégie d’authentification qui a des comptes locaux en tant que fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="acec4-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="acec4-123">Sur la connexion du hello compte local page (où vous entrez une adresse de messagerie et mot de passe, ou un nom d’utilisateur et le mot de passe), cliquez sur **ne peut pas accéder à votre compte ?** expérience du consommateur tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="acec4-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="acec4-124">Hello pages de réinitialisation de mot de passe libre-service peuvent être personnalisés à l’aide de hello [fonctionnalité de marque de société](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="acec4-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

