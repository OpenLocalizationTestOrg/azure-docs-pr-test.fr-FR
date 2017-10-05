---
title: 'Azure AD Connect : authentification directe - Verrouillage intelligent | Documents Microsoft'
description: "Cet article décrit comment l’authentification directe Azure Active Directory (Azure AD) protège vos comptes locaux contre les attaques de mot de passe par recherche exhaustive dans le cloud."
services: active-directory
keywords: Authentification directe Azure AD Connect, installer Active Directory, composants requis pour Azure AD, SSO, Authentification unique
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
ms.openlocfilehash: c84b2406e6373701c83c509342129bd6d7d4034b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="03a24-104">Authentification directe Azure Active Directory : Verrouillage intelligent</span><span class="sxs-lookup"><span data-stu-id="03a24-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="03a24-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="03a24-105">Overview</span></span>

<span data-ttu-id="03a24-106">Azure AD protège contre les attaques de mot de passe par recherche exhaustive et empêche le verrouillage des utilisateurs authentiques sur leurs applications Office 365 et SaaS.</span><span class="sxs-lookup"><span data-stu-id="03a24-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="03a24-107">Cette fonctionnalité, appelée **Verrouillage intelligent**, est pris en charge lorsque vous utilisez l’authentification directe en tant que méthode de connexion.</span><span class="sxs-lookup"><span data-stu-id="03a24-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="03a24-108">Le verrouillage intelligent est activé par défaut pour tous les clients et protège vos comptes d’utilisateur en permanence ; Il n’est pas nécessaire pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="03a24-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all the time; there is no need to turn it on.</span></span>

<span data-ttu-id="03a24-109">Le verrouillage intelligent fonctionne en conservant la trace des tentatives de connexion ayant échoué et après un certain **Seuil de verrouillage**, en démarrant une **Durée de verrouillage**.</span><span class="sxs-lookup"><span data-stu-id="03a24-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="03a24-110">Toutes les tentatives de connexion de l’attaquant pendant la durée de verrouillage sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="03a24-110">Any sign-in attempts from the attacker during the Lockout Duration are rejected.</span></span> <span data-ttu-id="03a24-111">Si l’attaque se poursuit, une fois la durée de verrouillage terminée, les durées de verrouillage pour les tentatives de connexion ayant échoué suivantes sont plus longues.</span><span class="sxs-lookup"><span data-stu-id="03a24-111">If the attack continues, the subsequent failed sign-in attempts after the Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="03a24-112">Le seuil de verrouillage par défaut est de 10 tentatives ayant échoué et la durée de verrouillage par défaut est de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="03a24-112">The default Lockout Threshold is 10 failed attempts, and the default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="03a24-113">Le verrouillage intelligent fait également la distinction entre les connexions d’utilisateurs authentiques et des attaquants et ne verrouille que les attaquants dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="03a24-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out the attackers in most cases.</span></span> <span data-ttu-id="03a24-114">Cette fonctionnalité empêche les attaquants de verrouiller à des fins malveillantes des utilisateurs authentiques.</span><span class="sxs-lookup"><span data-stu-id="03a24-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="03a24-115">Nous utilisons l’ancien comportement de connexion, les appareils et les navigateurs utilisateurs et d’autres signaux pour faire la distinction entre les attaquants et les utilisateurs authentiques.</span><span class="sxs-lookup"><span data-stu-id="03a24-115">We use past sign-in behavior, users’ devices & browsers and other signals to distinguish between genuine users and attackers.</span></span> <span data-ttu-id="03a24-116">Nous améliorons constamment nos algorithmes.</span><span class="sxs-lookup"><span data-stu-id="03a24-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="03a24-117">Étant donné que l’authentification directe transfère les requêtes de validation de mot de passe sur votre Active Directory (AD) local, vous devez empêcher les attaquants de verrouiller les comptes de vos utilisateurs AD.</span><span class="sxs-lookup"><span data-stu-id="03a24-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need to prevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="03a24-118">Étant donné que vous avez vos propres stratégies de verrouillage de compte Active Directory (en particulier, les stratégies[**Seuil de verrouillage de compte** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) et [ **Réinitialiser le compteur de verrouillage du compte après**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), vous devez configurer correctement les valeurs de seuil de verrouillage et de durée de verrouillage d’Azure AD pour filtrer les attaques dans le cloud avant qu’elles n’atteignent votre AD local.</span><span class="sxs-lookup"><span data-stu-id="03a24-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need to configure Azure AD’s Lockout Threshold and Lockout Duration values appropriately to filter out attacks in the cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="03a24-119">La fonctionnalité Smart Lockout est gratuite et _activée_ par défaut pour tous les clients.</span><span class="sxs-lookup"><span data-stu-id="03a24-119">The Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="03a24-120">Toutefois, la modification du seuil de verrouillage et des valeurs de durée de verrouillage d’Azure AD à l’aide de l’API Graph oblige votre locataire à avoir au moins une licence Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="03a24-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant to have at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="03a24-121">Vous n’avez pas besoin d’une licence Azure AD Premium P2 _par utilisateur_ pour obtenir la fonctionnalité de verrouillage intelligent avec une authentification directe.</span><span class="sxs-lookup"><span data-stu-id="03a24-121">You don't need an Azure AD Premium P2 license _per user_ to get the Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="03a24-122">Pour vous assurer que les comptes AD locaux de vos utilisateurs sont correctement protégés, vous devez vérifier que :</span><span class="sxs-lookup"><span data-stu-id="03a24-122">To ensure that your users’ on-premises AD accounts are well protected, you need to ensure that:</span></span>

1.  <span data-ttu-id="03a24-123">le seuil de verrouillage d’Azure AD est _inférieur_ au seuil de verrouillage du compte AD.</span><span class="sxs-lookup"><span data-stu-id="03a24-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="03a24-124">Nous vous recommandons de définir les valeurs de sorte que le seuil de verrouillage du compte AD soit au moins deux ou trois fois égal au seuil de verrouillage d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03a24-124">We recommend that you set the values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="03a24-125">La durée de verrouillage d’Azure AD (représentée en secondes) est _plus longue_ que Réinitialiser le compteur de verrouillage du compte après (exprimée en minutes) d’AD.</span><span class="sxs-lookup"><span data-stu-id="03a24-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="03a24-126">Vérifiez vos stratégies de verrouillage de compte AD</span><span class="sxs-lookup"><span data-stu-id="03a24-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="03a24-127">Utilisez les instructions suivantes pour vérifier vos stratégies de verrouillage de compte AD :</span><span class="sxs-lookup"><span data-stu-id="03a24-127">Use the following instructions to verify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="03a24-128">Ouvrez l’outil de gestion de stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="03a24-128">Open the Group Policy Management tool.</span></span>
2.  <span data-ttu-id="03a24-129">Modifiez la stratégie de groupe appliquée à tous les utilisateurs, par exemple la stratégie de domaine par défaut.</span><span class="sxs-lookup"><span data-stu-id="03a24-129">Edit the group policy that is applied to all users, for example, the Default Domain Policy.</span></span>
3.  <span data-ttu-id="03a24-130">Accédez à Configuration de l’ordinateur\Stratégie\Paramètres Windows\Paramètres de sécurité\Stratégies de compte\Stratégie de verrouillage du compte.</span><span class="sxs-lookup"><span data-stu-id="03a24-130">Navigate to Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="03a24-131">Vérifiez vos valeurs de Seuil de verrouillage de compte et Réinitialiser le compteur de verrouillage du compte après.</span><span class="sxs-lookup"><span data-stu-id="03a24-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Stratégies de verrouillage de compte AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-the-graph-api-to-manage-your-tenants-smart-lockout-values"></a><span data-ttu-id="03a24-133">Utilisez l’API Graph pour gérer les valeurs de verrouillage intelligent de votre client</span><span class="sxs-lookup"><span data-stu-id="03a24-133">Use the Graph API to manage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="03a24-134">Modifier les valeurs du seuil de verrouillage et de la durée de verrouillage d’Azure AD à l’aide de l’API Graph est une fonctionnalité d’Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="03a24-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="03a24-135">Vous devez également être un Administrateur global sur votre client.</span><span class="sxs-lookup"><span data-stu-id="03a24-135">It also needs you to be a Global Administrator on your tenant.</span></span>

<span data-ttu-id="03a24-136">Vous pouvez utiliser [l’Explorateur graphique](https://developer.microsoft.com/graph/graph-explorer) pour lire, définir et mettre à jour les valeurs de verrouillage intelligent d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03a24-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="03a24-137">Mais vous pouvez également effectuer ces opérations par programme.</span><span class="sxs-lookup"><span data-stu-id="03a24-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="03a24-138">Lire les valeurs de verrouillage intelligent</span><span class="sxs-lookup"><span data-stu-id="03a24-138">Read Smart Lockout values</span></span>

<span data-ttu-id="03a24-139">Suivez ces étapes pour lire les valeurs de verrouillage intelligent de votre client :</span><span class="sxs-lookup"><span data-stu-id="03a24-139">Follow these steps to read your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="03a24-140">Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client.</span><span class="sxs-lookup"><span data-stu-id="03a24-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="03a24-141">Si vous y êtes invité, accordez l’accès pour les autorisations demandées.</span><span class="sxs-lookup"><span data-stu-id="03a24-141">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="03a24-142">Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All ».</span><span class="sxs-lookup"><span data-stu-id="03a24-142">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="03a24-143">Configurez la requête d’API Graph comme suit : définir la version sur « BETA », type de requête sur « GET » et l’URL sur `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="03a24-143">Configure the Graph API request as follows: Set version to “BETA”, request type to “GET” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="03a24-144">Cliquez sur « Exécuter la requête » pour consulter les valeurs de verrouillage intelligent de votre client.</span><span class="sxs-lookup"><span data-stu-id="03a24-144">Click "Run Query" to see your tenant's Smart Lockout values.</span></span> <span data-ttu-id="03a24-145">Si vous n’avez pas défini les valeurs de votre client avant, un ensemble vide s’affiche.</span><span class="sxs-lookup"><span data-stu-id="03a24-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="03a24-146">Définir les valeurs de verrouillage intelligent</span><span class="sxs-lookup"><span data-stu-id="03a24-146">Set Smart Lockout values</span></span>

<span data-ttu-id="03a24-147">Procédez comme suit pour définir les valeurs de verrouillage intelligent de votre client (pour la première fois uniquement) :</span><span class="sxs-lookup"><span data-stu-id="03a24-147">Follow these steps to set your tenant’s Smart Lockout values (for the first time only):</span></span>

1. <span data-ttu-id="03a24-148">Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client.</span><span class="sxs-lookup"><span data-stu-id="03a24-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="03a24-149">Si vous y êtes invité, accordez l’accès pour les autorisations demandées.</span><span class="sxs-lookup"><span data-stu-id="03a24-149">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="03a24-150">Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All ».</span><span class="sxs-lookup"><span data-stu-id="03a24-150">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="03a24-151">Configurez la requête d’API Graph comme suit : définir la version sur « BETA », le type de requête sur « POST » et l’URL sur `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="03a24-151">Configure the Graph API request as follows: Set version to “BETA”, request type to “POST” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="03a24-152">Copiez et collez la requête JSON suivante dans le champ « Corps de la requête ».</span><span class="sxs-lookup"><span data-stu-id="03a24-152">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="03a24-153">Modifiez les valeurs de verrouillage intelligent comme il convient et utilisez un GUID aléatoire pour `templateId`.</span><span class="sxs-lookup"><span data-stu-id="03a24-153">Change the Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="03a24-154">Cliquez sur « Exécuter la requête » pour définir les valeurs de verrouillage intelligent de votre client.</span><span class="sxs-lookup"><span data-stu-id="03a24-154">Click "Run Query" to set your tenant's Smart Lockout values.</span></span>

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
><span data-ttu-id="03a24-155">Si vous ne les utiliser pas, vous pouvez laisser les valeurs **BannedPasswordList** et **EnableBannedPasswordCheck** vides (« ») et « false » respectivement.</span><span class="sxs-lookup"><span data-stu-id="03a24-155">If you are not using them, you can leave the **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="03a24-156">Vérifiez que vous avez défini les valeurs de verrouillage intelligent de votre client correctement à l’aide de [ces étapes](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="03a24-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="03a24-157">Mettre à jour les valeurs de verrouillage intelligent</span><span class="sxs-lookup"><span data-stu-id="03a24-157">Update Smart Lockout values</span></span>

<span data-ttu-id="03a24-158">Suivez ces étapes pour mettre à jour les valeurs de verrouillage intelligent de votre client (si vous les avez déjà définies avant) :</span><span class="sxs-lookup"><span data-stu-id="03a24-158">Follow these steps to update your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="03a24-159">Connectez-vous à l’Explorateur graphique en tant qu’administrateur global de votre client.</span><span class="sxs-lookup"><span data-stu-id="03a24-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="03a24-160">Si vous y êtes invité, accordez l’accès pour les autorisations demandées.</span><span class="sxs-lookup"><span data-stu-id="03a24-160">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="03a24-161">Cliquez sur « Modifier les autorisations » et sélectionnez l’autorisation « Directory.ReadWrite.All ».</span><span class="sxs-lookup"><span data-stu-id="03a24-161">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="03a24-162">[Suivez ces étapes pour lire les valeurs de verrouillage intelligent de votre client](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="03a24-162">[Follow these steps to read your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="03a24-163">Copiez la valeur `id` (un GUID) de l’élément avec « displayName » en tant que « PasswordRuleSettings ».</span><span class="sxs-lookup"><span data-stu-id="03a24-163">Copy the `id` value (a GUID) of the item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="03a24-164">Configurez la requête d’API Graph comme suit : définir la version sur « BETA », le type de requête sur « PATCH » et l’URL sur `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` : utilisez le GUID de l’étape 3 pour `<id>`.</span><span class="sxs-lookup"><span data-stu-id="03a24-164">Configure the Graph API request as follows: Set version to “BETA”, request type to “PATCH” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use the GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="03a24-165">Copiez et collez la requête JSON suivante dans le champ « Corps de la requête ».</span><span class="sxs-lookup"><span data-stu-id="03a24-165">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="03a24-166">Modifiez les valeurs de verrouillage intelligent comme il convient.</span><span class="sxs-lookup"><span data-stu-id="03a24-166">Change the Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="03a24-167">Cliquez sur « Exécuter la requête » pour mettre à jour les valeurs de verrouillage intelligent de votre client.</span><span class="sxs-lookup"><span data-stu-id="03a24-167">Click "Run Query" to update your tenant's Smart Lockout values.</span></span>

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

<span data-ttu-id="03a24-168">Vérifiez que vous avez mis à jour les valeurs de verrouillage intelligent de votre client correctement à l’aide de [ces étapes](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="03a24-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="03a24-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03a24-169">Next steps</span></span>
- <span data-ttu-id="03a24-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des requêtes de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="03a24-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
