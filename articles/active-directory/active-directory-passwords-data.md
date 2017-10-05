---
title: "Exigences en matière de données Azure AD SSPR | Microsoft Docs"
description: "Exigences en matière de données pour la réinitialisation du mot de passe en libre-service Azure AD et comment les satisfaire"
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
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="fef62-103">Déployer la réinitialisation du mot de passe sans demander l’inscription de l’utilisateur final</span><span class="sxs-lookup"><span data-stu-id="fef62-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="fef62-104">Le déploiement de la réinitialisation de mot du passe en libre-service (SSPR) exige que les données d’authentification soient présentes.</span><span class="sxs-lookup"><span data-stu-id="fef62-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="fef62-105">Certaines organisations demandent à leurs utilisateurs d’entrer leurs données d’authentification eux-mêmes, mais de nombreuses organisations préfèrent se synchroniser avec les données existantes dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fef62-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="fef62-106">Si vous avez correctement mis en forme les données dans votre répertoire local et configurez [Azure AD Connect à l’aide des paramètres express](./connect/active-directory-aadconnect-get-started-express.md), ces données sont rendues disponibles pour Azure AD et SSPR sans aucune interaction utilisateur requise.</span><span class="sxs-lookup"><span data-stu-id="fef62-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="fef62-107">Les numéros de téléphone doivent être au format +CodePays NuméroTéléphone (exemple : +1 4255551234) pour fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="fef62-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="fef62-108">La réinitialisation du mot de passe ne prend pas en charge les extensions de téléphone.</span><span class="sxs-lookup"><span data-stu-id="fef62-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="fef62-109">Même au format +1 4255551234X12345, les extensions sont supprimées avant l’appel.</span><span class="sxs-lookup"><span data-stu-id="fef62-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="fef62-110">Champs renseignés</span><span class="sxs-lookup"><span data-stu-id="fef62-110">Fields populated</span></span>

<span data-ttu-id="fef62-111">Si vous utilisez les paramètres par défaut dans Azure AD Connect, les mappages suivants sont effectués.</span><span class="sxs-lookup"><span data-stu-id="fef62-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="fef62-112">AD local</span><span class="sxs-lookup"><span data-stu-id="fef62-112">On-premises AD</span></span> | <span data-ttu-id="fef62-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef62-113">Azure AD</span></span> | <span data-ttu-id="fef62-114">Informations de contact de l’authentification AD Azure</span><span class="sxs-lookup"><span data-stu-id="fef62-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fef62-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="fef62-115">telephoneNumber</span></span> | <span data-ttu-id="fef62-116">Téléphone de bureau</span><span class="sxs-lookup"><span data-stu-id="fef62-116">Office phone</span></span> | <span data-ttu-id="fef62-117">Autre téléphone</span><span class="sxs-lookup"><span data-stu-id="fef62-117">Alternate phone</span></span> |
| <span data-ttu-id="fef62-118">mobile</span><span class="sxs-lookup"><span data-stu-id="fef62-118">mobile</span></span> | <span data-ttu-id="fef62-119">Téléphone mobile</span><span class="sxs-lookup"><span data-stu-id="fef62-119">Mobile phone</span></span> | <span data-ttu-id="fef62-120">Téléphone</span><span class="sxs-lookup"><span data-stu-id="fef62-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="fef62-121">Questions et réponses de sécurité</span><span class="sxs-lookup"><span data-stu-id="fef62-121">Security questions and answers</span></span>

<span data-ttu-id="fef62-122">Les questions et les réponses de sécurité sont stockées de manière sécurisée sur votre locataire Azure AD et sont uniquement accessibles aux utilisateurs par le biais du [portail d’inscription SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="fef62-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="fef62-123">Les administrateurs ne peuvent pas voir ou modifier le contenu des questions et des réponses des autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fef62-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="fef62-124">Ce qu’il se passe lorsqu'un utilisateur s'inscrit</span><span class="sxs-lookup"><span data-stu-id="fef62-124">What happens when a user registers</span></span>

<span data-ttu-id="fef62-125">Lorsqu’un utilisateur s'inscrit, la page d’inscription définit les champs suivants :</span><span class="sxs-lookup"><span data-stu-id="fef62-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="fef62-126">Téléphone d’authentification</span><span class="sxs-lookup"><span data-stu-id="fef62-126">Authentication Phone</span></span>
* <span data-ttu-id="fef62-127">E-mail d’authentification</span><span class="sxs-lookup"><span data-stu-id="fef62-127">Authentication Email</span></span>
* <span data-ttu-id="fef62-128">Questions et réponses de sécurité</span><span class="sxs-lookup"><span data-stu-id="fef62-128">Security Questions and Answers</span></span>

<span data-ttu-id="fef62-129">Si vous avez fourni une valeur pour **Téléphone mobile** ou **Autre adresse de messagerie**, les utilisateurs peuvent immédiatement l’utiliser pour réinitialiser leur mot de passe, même s’ils ne se sont pas inscrits au service.</span><span class="sxs-lookup"><span data-stu-id="fef62-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="fef62-130">Les utilisateurs voient ces valeurs lorsqu’ils s’inscrivent pour la première fois et ils ont la possibilité de les modifier.</span><span class="sxs-lookup"><span data-stu-id="fef62-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="fef62-131">Une fois les utilisateurs inscrits, ces valeurs sont conservées respectivement dans les champs **Téléphone d’authentification** et **E-mail d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="fef62-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="fef62-132">Définir et lire les données d’authentification à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef62-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="fef62-133">Les champs suivants peuvent être définis à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef62-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="fef62-134">Autre adresse de messagerie</span><span class="sxs-lookup"><span data-stu-id="fef62-134">Alternate Email</span></span>
* <span data-ttu-id="fef62-135">Téléphone mobile</span><span class="sxs-lookup"><span data-stu-id="fef62-135">Mobile Phone</span></span>
* <span data-ttu-id="fef62-136">Téléphone de bureau : ne peut être défini qu’en l’absence de synchronisation avec un répertoire local</span><span class="sxs-lookup"><span data-stu-id="fef62-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="fef62-137">Utiliser PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="fef62-137">Using PowerShell V1</span></span>

<span data-ttu-id="fef62-138">Pour commencer, vous devez [télécharger et installer le module Azure AD PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="fef62-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="fef62-139">Une fois le module installé, vous pouvez suivre les étapes suivantes pour configurer chaque champ.</span><span class="sxs-lookup"><span data-stu-id="fef62-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="fef62-140">Définir les données d’authentification avec PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="fef62-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="fef62-141">Lire les données d’authentification avec PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="fef62-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="fef62-142">Téléphone d’authentification et E-mail d’authentification ne peuvent être lus qu’à l’aide de Powershell V1 en utilisant les commandes qui suivent</span><span class="sxs-lookup"><span data-stu-id="fef62-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="fef62-143">Utiliser PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="fef62-143">Using PowerShell V2</span></span>

<span data-ttu-id="fef62-144">Pour commencer, vous devez [télécharger et installer le module Azure AD PowerShell V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="fef62-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="fef62-145">Une fois le module installé, vous pouvez suivre les étapes suivantes pour configurer chaque champ.</span><span class="sxs-lookup"><span data-stu-id="fef62-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="fef62-146">Pour installer rapidement des versions récentes de PowerShell compatibles avec Install-Module, exécutez ces commandes (la première ligne vérifie simplement si le produit est déjà installé) :</span><span class="sxs-lookup"><span data-stu-id="fef62-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="fef62-147">Définir les données d’authentification avec PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="fef62-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="fef62-148">Lire les données d’authentification avec PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="fef62-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="fef62-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fef62-149">Next steps</span></span>

<span data-ttu-id="fef62-150">Les liens suivants fournissent des informations supplémentaires sur la réinitialisation de mot de passe à l’aide d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fef62-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="fef62-151">[**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fef62-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="fef62-152">[**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fef62-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="fef62-153">[**Déploiement**](active-directory-passwords-best-practices.md) : planifiez et déployez la réinitialisation de mot de passe en libre-service pour vos utilisateurs grâce aux conseils figurant ici.</span><span class="sxs-lookup"><span data-stu-id="fef62-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="fef62-154">[**Personnalisation**](active-directory-passwords-customize.md) : personnalisez l’apparence de l’interface de réinitialisation de mot de passe en libre-service de votre société.</span><span class="sxs-lookup"><span data-stu-id="fef62-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="fef62-155">[**Stratégie**](active-directory-passwords-policy.md) : comprenez mieux et définissez les stratégies de mot de passe d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fef62-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="fef62-156">[**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service.</span><span class="sxs-lookup"><span data-stu-id="fef62-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="fef62-157">[**Présentation technique approfondie**](active-directory-passwords-how-it-works.md) : découvrez ce qui se passe sous le capot pour mieux comprendre le fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="fef62-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="fef62-158">[**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ?</span><span class="sxs-lookup"><span data-stu-id="fef62-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="fef62-159">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="fef62-159">Why?</span></span> <span data-ttu-id="fef62-160">Quoi ?</span><span class="sxs-lookup"><span data-stu-id="fef62-160">What?</span></span> <span data-ttu-id="fef62-161">Où ?</span><span class="sxs-lookup"><span data-stu-id="fef62-161">Where?</span></span> <span data-ttu-id="fef62-162">Qui ?</span><span class="sxs-lookup"><span data-stu-id="fef62-162">Who?</span></span> <span data-ttu-id="fef62-163">Quand ?</span><span class="sxs-lookup"><span data-stu-id="fef62-163">When?</span></span> <span data-ttu-id="fef62-164">- Les réponses aux questions que vous vouliez poser depuis toujours.</span><span class="sxs-lookup"><span data-stu-id="fef62-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="fef62-165">[**Résolution des problèmes**](active-directory-passwords-troubleshoot.md) : découvrez comment résoudre les problèmes courants susceptibles de survenir avec la réinitialisation de mot de passe en libre-service.</span><span class="sxs-lookup"><span data-stu-id="fef62-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
