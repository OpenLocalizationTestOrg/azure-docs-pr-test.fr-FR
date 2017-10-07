---
title: "Exigences en matière de données Azure AD SSPR | Microsoft Docs"
description: "Réinitialiser des spécifications de données pour le mot de passe libre-service Azure AD et comment toosatisfy les"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="c694c-103">Déployer la réinitialisation du mot de passe sans demander l’inscription de l’utilisateur final</span><span class="sxs-lookup"><span data-stu-id="c694c-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="c694c-104">Déploiement de réinitialisation de mot de passe libre-service (SSPR) requiert l’authentification toobe de données présente.</span><span class="sxs-lookup"><span data-stu-id="c694c-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="c694c-105">Certaines organisations ont leurs utilisateurs d’entrer leurs données d’authentification eux-mêmes, mais de nombreuses organisations préfèrent toosynchronize avec des données existantes dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c694c-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="c694c-106">Si vous avez correctement renseigné des données dans votre annuaire local et configurez [Azure AD Connect à l’aide de la configuration rapide](./connect/active-directory-aadconnect-get-started-express.md), que les données sont rendues disponible tooAzure AD et SSPR sans aucune interaction utilisateur requis.</span><span class="sxs-lookup"><span data-stu-id="c694c-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="c694c-107">Les numéros de téléphone doivent être dans un format de hello + CountryCode PhoneNumber exemple : + 1 4255551234 toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="c694c-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="c694c-108">La réinitialisation du mot de passe ne prend pas en charge les extensions de téléphone.</span><span class="sxs-lookup"><span data-stu-id="c694c-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="c694c-109">Même au format 12345 de + 1 4255551234 X hello, les extensions sont supprimées avant hello.</span><span class="sxs-lookup"><span data-stu-id="c694c-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="c694c-110">Champs renseignés</span><span class="sxs-lookup"><span data-stu-id="c694c-110">Fields populated</span></span>

<span data-ttu-id="c694c-111">Si vous utilisez des paramètres par défaut de hello Bonjour Azure AD Connect suivant les mappages sont effectuées.</span><span class="sxs-lookup"><span data-stu-id="c694c-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="c694c-112">AD local</span><span class="sxs-lookup"><span data-stu-id="c694c-112">On-premises AD</span></span> | <span data-ttu-id="c694c-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="c694c-113">Azure AD</span></span> | <span data-ttu-id="c694c-114">Informations de contact de l’authentification AD Azure</span><span class="sxs-lookup"><span data-stu-id="c694c-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c694c-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="c694c-115">telephoneNumber</span></span> | <span data-ttu-id="c694c-116">Téléphone de bureau</span><span class="sxs-lookup"><span data-stu-id="c694c-116">Office phone</span></span> | <span data-ttu-id="c694c-117">Autre téléphone</span><span class="sxs-lookup"><span data-stu-id="c694c-117">Alternate phone</span></span> |
| <span data-ttu-id="c694c-118">mobile</span><span class="sxs-lookup"><span data-stu-id="c694c-118">mobile</span></span> | <span data-ttu-id="c694c-119">Téléphone mobile</span><span class="sxs-lookup"><span data-stu-id="c694c-119">Mobile phone</span></span> | <span data-ttu-id="c694c-120">Téléphone</span><span class="sxs-lookup"><span data-stu-id="c694c-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="c694c-121">Questions et réponses de sécurité</span><span class="sxs-lookup"><span data-stu-id="c694c-121">Security questions and answers</span></span>

<span data-ttu-id="c694c-122">Les questions de sécurité et les réponses sont stockées de manière sécurisée dans votre locataire Azure AD et sont uniquement accessibles toousers via hello [portail d’inscription SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="c694c-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="c694c-123">Les administrateurs ne peut pas voir ou modifier du contenu hello des questions des utilisateurs et des réponses un autre.</span><span class="sxs-lookup"><span data-stu-id="c694c-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="c694c-124">Ce qu’il se passe lorsqu'un utilisateur s'inscrit</span><span class="sxs-lookup"><span data-stu-id="c694c-124">What happens when a user registers</span></span>

<span data-ttu-id="c694c-125">Lorsqu’un utilisateur s’inscrit, page d’inscription de hello définit hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="c694c-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="c694c-126">Téléphone d’authentification</span><span class="sxs-lookup"><span data-stu-id="c694c-126">Authentication Phone</span></span>
* <span data-ttu-id="c694c-127">E-mail d’authentification</span><span class="sxs-lookup"><span data-stu-id="c694c-127">Authentication Email</span></span>
* <span data-ttu-id="c694c-128">Questions et réponses de sécurité</span><span class="sxs-lookup"><span data-stu-id="c694c-128">Security Questions and Answers</span></span>

<span data-ttu-id="c694c-129">Si vous avez fourni une valeur pour **téléphone Mobile** ou **autre adresse de messagerie**, les utilisateurs peuvent immédiatement utiliser ces valeurs tooreset leurs mots de passe, même si elles n’ont pas enregistré pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="c694c-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="c694c-130">En outre, les utilisateurs voient les ces valeurs lors de l’inscription pour hello première fois et les modifier s’ils le souhaitent.</span><span class="sxs-lookup"><span data-stu-id="c694c-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="c694c-131">Après leur inscrivent, ces valeurs sont rendues persistantes dans hello **téléphone d’authentification** et **E-mail d’authentification** champs, respectivement.</span><span class="sxs-lookup"><span data-stu-id="c694c-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="c694c-132">Définir et lire les données d’authentification à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c694c-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="c694c-133">Hello suivant les champs peut être définie à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c694c-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="c694c-134">Autre adresse de messagerie</span><span class="sxs-lookup"><span data-stu-id="c694c-134">Alternate Email</span></span>
* <span data-ttu-id="c694c-135">Téléphone mobile</span><span class="sxs-lookup"><span data-stu-id="c694c-135">Mobile Phone</span></span>
* <span data-ttu-id="c694c-136">Téléphone de bureau : ne peut être défini qu’en l’absence de synchronisation avec un répertoire local</span><span class="sxs-lookup"><span data-stu-id="c694c-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="c694c-137">Utiliser PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="c694c-137">Using PowerShell V1</span></span>

<span data-ttu-id="c694c-138">tooget démarré, vous devez trop[télécharger et installer le module PowerShell Azure AD de hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="c694c-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="c694c-139">Une fois que vous avez déjà installé, vous pouvez suivre les étapes de hello qui suivent tooconfigure chaque champ.</span><span class="sxs-lookup"><span data-stu-id="c694c-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="c694c-140">Définir les données d’authentification avec PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="c694c-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="c694c-141">Lire les données d’authentification avec PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="c694c-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="c694c-142">Téléphone d’authentification et E-mail d’authentification peuvent uniquement être lus à l’aide de Powershell V1 hello d’à l’aide des commandes qui suivent</span><span class="sxs-lookup"><span data-stu-id="c694c-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="c694c-143">Utiliser PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="c694c-143">Using PowerShell V2</span></span>

<span data-ttu-id="c694c-144">tooget démarré, vous devez trop[télécharger et installer le module PowerShell de hello Azure AD V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="c694c-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="c694c-145">Une fois que vous avez déjà installé, vous pouvez suivre les étapes de hello qui suivent tooconfigure chaque champ.</span><span class="sxs-lookup"><span data-stu-id="c694c-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="c694c-146">tooinstall rapidement à partir de versions récentes de PowerShell qui prennent en charge d’Install-Module, exécutez ces commandes (première ligne de hello simplement des contrôles toosee s’il est déjà installé) :</span><span class="sxs-lookup"><span data-stu-id="c694c-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="c694c-147">Définir les données d’authentification avec PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="c694c-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="c694c-148">Lire les données d’authentification avec PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="c694c-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="c694c-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c694c-149">Next steps</span></span>

<span data-ttu-id="c694c-150">Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="c694c-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="c694c-151">[**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c694c-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="c694c-152">[**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c694c-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="c694c-153">[**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici</span><span class="sxs-lookup"><span data-stu-id="c694c-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="c694c-154">[**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="c694c-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="c694c-155">[**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="c694c-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="c694c-156">[**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="c694c-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="c694c-157">[**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement</span><span class="sxs-lookup"><span data-stu-id="c694c-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="c694c-158">[**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ?</span><span class="sxs-lookup"><span data-stu-id="c694c-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="c694c-159">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="c694c-159">Why?</span></span> <span data-ttu-id="c694c-160">Quoi ?</span><span class="sxs-lookup"><span data-stu-id="c694c-160">What?</span></span> <span data-ttu-id="c694c-161">Où ?</span><span class="sxs-lookup"><span data-stu-id="c694c-161">Where?</span></span> <span data-ttu-id="c694c-162">Qui ?</span><span class="sxs-lookup"><span data-stu-id="c694c-162">Who?</span></span> <span data-ttu-id="c694c-163">Quand ?</span><span class="sxs-lookup"><span data-stu-id="c694c-163">When?</span></span> <span data-ttu-id="c694c-164">-Réponses tooquestions vous souhaitiez toujours tooask</span><span class="sxs-lookup"><span data-stu-id="c694c-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="c694c-165">[**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR</span><span class="sxs-lookup"><span data-stu-id="c694c-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
