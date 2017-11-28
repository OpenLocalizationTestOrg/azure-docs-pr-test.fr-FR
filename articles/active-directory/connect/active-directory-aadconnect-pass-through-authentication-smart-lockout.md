---
title: 'Azure AD Connect : authentification directe - Verrouillage intelligent | Documents Microsoft'
description: "Cet article décrit comment l’authentification Azure Active Directory (Azure AD) pass-through protège vos comptes locale contre les attaques de mot de passe en force brute dans le cloud de hello."
services: active-directory
keywords: "Authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="d74a3-104">Authentification directe Azure Active Directory : Verrouillage intelligent</span><span class="sxs-lookup"><span data-stu-id="d74a3-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="d74a3-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d74a3-105">Overview</span></span>

<span data-ttu-id="d74a3-106">Azure AD protège contre les attaques de mot de passe par recherche exhaustive et empêche le verrouillage des utilisateurs authentiques sur leurs applications Office 365 et SaaS.</span><span class="sxs-lookup"><span data-stu-id="d74a3-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="d74a3-107">Cette fonctionnalité, appelée **Verrouillage intelligent**, est pris en charge lorsque vous utilisez l’authentification directe en tant que méthode de connexion.</span><span class="sxs-lookup"><span data-stu-id="d74a3-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="d74a3-108">Verrouillage intelligent est activée par défaut pour tous les locataires et protégez vos comptes d’utilisateur de tout temps hello ; Il n’existe aucun besoin tooturn sur.</span><span class="sxs-lookup"><span data-stu-id="d74a3-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="d74a3-109">Le verrouillage intelligent fonctionne en conservant la trace des tentatives de connexion ayant échoué et après un certain **Seuil de verrouillage**, en démarrant une **Durée de verrouillage**.</span><span class="sxs-lookup"><span data-stu-id="d74a3-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="d74a3-110">Toutes les tentatives de connexion à partir de l’attaquant hello pendant hello durée de verrouillage sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="d74a3-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="d74a3-111">Si hello attaque se poursuit, hello suivantes ayant échoué tentatives de connexion hello durée de verrouillage de fin entraîne des durées de verrouillage de plus de temps.</span><span class="sxs-lookup"><span data-stu-id="d74a3-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="d74a3-112">la valeur par défaut de Hello seuil de verrouillage est 10 tentatives ayant échoué et par défaut de hello que durée de verrouillage est de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="d74a3-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="d74a3-113">Verrouillage actif également fait la distinction entre les connexions d’utilisateurs authentiques et contre les personnes malveillantes et des verrous uniquement à des personnes malveillantes hello dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="d74a3-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="d74a3-114">Cette fonctionnalité empêche les attaquants de verrouiller à des fins malveillantes des utilisateurs authentiques.</span><span class="sxs-lookup"><span data-stu-id="d74a3-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="d74a3-115">Nous utilisons au-delà de connexion comportement, les appareils des utilisateurs & navigateurs et autres toodistinguish signaux entre les utilisateurs authentiques et des personnes malveillantes.</span><span class="sxs-lookup"><span data-stu-id="d74a3-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="d74a3-116">Nous améliorons constamment nos algorithmes.</span><span class="sxs-lookup"><span data-stu-id="d74a3-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="d74a3-117">Étant donné que l’authentification directe transfère les demandes de validation de mot de passe sur votre système local Active Directory (AD), vous devez les personnes malveillantes tooprevent de verrouillage des comptes de vos utilisateurs AD.</span><span class="sxs-lookup"><span data-stu-id="d74a3-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="d74a3-118">Étant donné que vous avez vos propres stratégies de verrouillage de compte Active Directory (en particulier, [ **seuil de verrouillage de compte** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) et [ **réinitialiser compte le verrouillage du compteur après stratégies** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), vous devez le seuil de verrouillage tooconfigure d’Azure AD et durée de verrouillage de valeurs correctement toofilter des attaques dans le cloud de hello avant qu’ils atteignent votre service Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d74a3-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="d74a3-119">est gratuite et fonctionnalité de verrouillage actives Hello _sur_ par défaut pour tous les clients.</span><span class="sxs-lookup"><span data-stu-id="d74a3-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="d74a3-120">Toutefois, la modification du seuil de verrouillage d’Azure AD et les valeurs de durée de verrouillage à l’aide de l’API Graph doit votre licence de Premium P2 toohave AD Azure au moins un client.</span><span class="sxs-lookup"><span data-stu-id="d74a3-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="d74a3-121">Vous n’avez pas besoin d’une licence Azure AD Premium P2 _par utilisateur_ fonctionnalité de verrouillage actives hello tooget avec l’authentification directe.</span><span class="sxs-lookup"><span data-stu-id="d74a3-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="d74a3-122">tooensure que vos utilisateurs AD comptes locaux sont correctement protégés, vous devez tooensure qui :</span><span class="sxs-lookup"><span data-stu-id="d74a3-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="d74a3-123">le seuil de verrouillage d’Azure AD est _inférieur_ au seuil de verrouillage du compte AD.</span><span class="sxs-lookup"><span data-stu-id="d74a3-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="d74a3-124">Nous vous recommandons de définir les valeurs hello telles que le seuil de verrouillage de compte de l’annonce est au moins deux ou trois fois le seuil de verrouillage d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d74a3-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="d74a3-125">La durée de verrouillage d’Azure AD (représentée en secondes) est _plus longue_ que Réinitialiser le compteur de verrouillage du compte après (exprimée en minutes) d’AD.</span><span class="sxs-lookup"><span data-stu-id="d74a3-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="d74a3-126">Vérifiez vos stratégies de verrouillage de compte AD</span><span class="sxs-lookup"><span data-stu-id="d74a3-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="d74a3-127">Utilisez hello suivant les instructions tooverify vos stratégies de verrouillage de compte Active Directory :</span><span class="sxs-lookup"><span data-stu-id="d74a3-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="d74a3-128">Ouvrez l’outil de gestion de stratégie de groupe hello.</span><span class="sxs-lookup"><span data-stu-id="d74a3-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="d74a3-129">Modifier hello stratégie de groupe qui est appliqué tooall utilisateurs, par exemple, hello stratégie de domaine par défaut.</span><span class="sxs-lookup"><span data-stu-id="d74a3-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="d74a3-130">Accédez tooComputer stratégie de verrouillage de compte Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres paramètres.</span><span class="sxs-lookup"><span data-stu-id="d74a3-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="d74a3-131">Vérifiez vos valeurs de Seuil de verrouillage de compte et Réinitialiser le compteur de verrouillage du compte après.</span><span class="sxs-lookup"><span data-stu-id="d74a3-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Stratégies de verrouillage de compte AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="d74a3-133">Utiliser des valeurs de verrouillage intelligente de votre locataire hello API Graph toomanage</span><span class="sxs-lookup"><span data-stu-id="d74a3-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="d74a3-134">Modifier les valeurs du seuil de verrouillage et de la durée de verrouillage d’Azure AD à l’aide de l’API Graph est une fonctionnalité d’Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="d74a3-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="d74a3-135">Il doit également toobe un administrateur Global sur votre client.</span><span class="sxs-lookup"><span data-stu-id="d74a3-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="d74a3-136">Vous pouvez utiliser [Explorateur graphique](https://developer.microsoft.com/graph/graph-explorer) tooread, définir et mettre à jour les valeurs de verrouillage actives d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d74a3-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="d74a3-137">Mais vous pouvez également effectuer ces opérations par programme.</span><span class="sxs-lookup"><span data-stu-id="d74a3-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="d74a3-138">Lire les valeurs de verrouillage intelligent</span><span class="sxs-lookup"><span data-stu-id="d74a3-138">Read Smart Lockout values</span></span>

<span data-ttu-id="d74a3-139">Suivez ces étapes tooread valeurs de verrouillage intelligente de votre locataire :</span><span class="sxs-lookup"><span data-stu-id="d74a3-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="d74a3-140">Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client.</span><span class="sxs-lookup"><span data-stu-id="d74a3-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="d74a3-141">Si vous y êtes invité, accordez l’accès hello les autorisations demandées.</span><span class="sxs-lookup"><span data-stu-id="d74a3-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="d74a3-142">Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All » hello.</span><span class="sxs-lookup"><span data-stu-id="d74a3-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="d74a3-143">Demande d’API Graph hello le configurer comme suit : définir la version trop « BETA », type de demande trop « GET » et l’URL trop`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="d74a3-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="d74a3-144">Cliquez sur « Exécuter la requête » toosee de valeurs de verrouillage intelligente de votre locataire.</span><span class="sxs-lookup"><span data-stu-id="d74a3-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="d74a3-145">Si vous n’avez pas défini les valeurs de votre client avant, un ensemble vide s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d74a3-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="d74a3-146">Définir les valeurs de verrouillage intelligent</span><span class="sxs-lookup"><span data-stu-id="d74a3-146">Set Smart Lockout values</span></span>

<span data-ttu-id="d74a3-147">Suivez ces étapes tooset valeurs de verrouillage intelligente de votre locataire (pour hello uniquement la première fois) :</span><span class="sxs-lookup"><span data-stu-id="d74a3-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="d74a3-148">Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client.</span><span class="sxs-lookup"><span data-stu-id="d74a3-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="d74a3-149">Si vous y êtes invité, accordez l’accès hello les autorisations demandées.</span><span class="sxs-lookup"><span data-stu-id="d74a3-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="d74a3-150">Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All » hello.</span><span class="sxs-lookup"><span data-stu-id="d74a3-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="d74a3-151">Demande d’API Graph hello le configurer comme suit : définir la version trop « BETA », type de demande trop « POST » et l’URL trop`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="d74a3-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="d74a3-152">Copiez et collez hello suivant de demande JSON dans le champ de « Corps de la demande » hello.</span><span class="sxs-lookup"><span data-stu-id="d74a3-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="d74a3-153">Modifier les valeurs de verrouillage actives hello comme il convient et utiliser un GUID aléatoire pour `templateId`.</span><span class="sxs-lookup"><span data-stu-id="d74a3-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="d74a3-154">Cliquez sur « Exécuter la requête » tooset de valeurs de verrouillage intelligente de votre locataire.</span><span class="sxs-lookup"><span data-stu-id="d74a3-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="d74a3-155">Si vous ne les utilisez pas, vous pouvez laisser hello **BannedPasswordList** et **EnableBannedPasswordCheck** valeurs sous la forme vide (« ») et « false » respectivement.</span><span class="sxs-lookup"><span data-stu-id="d74a3-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="d74a3-156">Vérifiez que vous avez défini les valeurs de verrouillage intelligent de votre client correctement à l’aide de [ces étapes](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="d74a3-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="d74a3-157">Mettre à jour les valeurs de verrouillage intelligent</span><span class="sxs-lookup"><span data-stu-id="d74a3-157">Update Smart Lockout values</span></span>

<span data-ttu-id="d74a3-158">Suivez ces tooupdate étapes valeurs de verrouillage intelligente de votre locataire (si vous avez déjà défini les avant) :</span><span class="sxs-lookup"><span data-stu-id="d74a3-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="d74a3-159">Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client.</span><span class="sxs-lookup"><span data-stu-id="d74a3-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="d74a3-160">Si vous y êtes invité, accordez l’accès hello les autorisations demandées.</span><span class="sxs-lookup"><span data-stu-id="d74a3-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="d74a3-161">Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All » hello.</span><span class="sxs-lookup"><span data-stu-id="d74a3-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="d74a3-162">[Suivez ces étapes tooread valeurs de verrouillage intelligente de votre locataire](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="d74a3-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="d74a3-163">Hello de copie `id` valeur (GUID) de l’élément hello avec « displayName » en tant que « PasswordRuleSettings ».</span><span class="sxs-lookup"><span data-stu-id="d74a3-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="d74a3-164">Demande d’API Graph hello le configurer comme suit : définir la version trop « BETA », type de demande trop « Corriger » et l’URL trop`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -utiliser hello GUID à partir de l’étape 3 pour `<id>`.</span><span class="sxs-lookup"><span data-stu-id="d74a3-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="d74a3-165">Copiez et collez hello suivant de demande JSON dans le champ de « Corps de la demande » hello.</span><span class="sxs-lookup"><span data-stu-id="d74a3-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="d74a3-166">Modifier les valeurs de verrouillage actives hello comme il convient.</span><span class="sxs-lookup"><span data-stu-id="d74a3-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="d74a3-167">Cliquez sur « Exécuter la requête » tooupdate de valeurs de verrouillage intelligente de votre locataire.</span><span class="sxs-lookup"><span data-stu-id="d74a3-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="d74a3-168">Vérifiez que vous avez mis à jour les valeurs de verrouillage intelligent de votre client correctement à l’aide de [ces étapes](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="d74a3-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d74a3-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d74a3-169">Next steps</span></span>
- <span data-ttu-id="d74a3-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des requêtes de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="d74a3-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
