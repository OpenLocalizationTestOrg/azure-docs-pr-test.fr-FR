---
title: "fonctionnalités et la configuration de service aaaAzure AD Connect synchronisation | Documents Microsoft"
description: "Décrit les fonctionnalités côté service du service de synchronisation Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="597b8-103">Fonctionnalités de service de synchronisation d’Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="597b8-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="597b8-104">fonctionnalité de synchronisation Hello d’Azure AD Connect comporte deux composants :</span><span class="sxs-lookup"><span data-stu-id="597b8-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="597b8-105">composant de local Hello nommé **synchronisation Azure AD Connect**, également appelé **moteur de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="597b8-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="597b8-106">service Hello résidant dans Azure AD, également appelé **service de synchronisation Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="597b8-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="597b8-107">Cette rubrique explique comment les fonctionnalités hello suivant de hello **service de synchronisation Azure AD Connect** travail et comment vous pouvez les configurer à l’aide de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="597b8-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="597b8-108">Ces paramètres sont configurés par hello [Azure Module Active Directory pour Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="597b8-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="597b8-109">Téléchargez et installez-le séparément à partir d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="597b8-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="597b8-110">applets de commande Hello documentées dans cette rubrique ont été introduits dans hello [version de mars 2016 (version 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="597b8-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="597b8-111">Si vous n’avez pas les applets de commande hello documentées dans cette rubrique, ou ils ne produisent pas hello même résultat, puis vérifiez que vous exécutez la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="597b8-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="597b8-112">configuration de hello toosee dans votre annuaire Azure AD, exécutez `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="597b8-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="597b8-113">![Résultat de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="597b8-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="597b8-114">Plusieurs de ces paramètres peuvent uniquement être modifiés par Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="597b8-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="597b8-115">Hello paramètres suivants peuvent être configurés par `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="597b8-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="597b8-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="597b8-116">DirSyncFeature</span></span> | <span data-ttu-id="597b8-117">Commentaire</span><span class="sxs-lookup"><span data-stu-id="597b8-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="597b8-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="597b8-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="597b8-119">Permet de toojoin d’objets sur userPrincipalName dans adresse de tooprimary SMTP d’addition.</span><span class="sxs-lookup"><span data-stu-id="597b8-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="597b8-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="597b8-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="597b8-121">Permet attribut userPrincipalName de hello synchronisation moteur tooupdate hello gérés/de licence (non fédérés) aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="597b8-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="597b8-122">Lorsqu’une fonctionnalité a été activée, vous ne pouvez plus la désactiver.</span><span class="sxs-lookup"><span data-stu-id="597b8-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="597b8-123">À partir du 24 août 2016 hello fonctionnalité *dupliquer la résilience de l’attribut* est activée par défaut pour nouveau Azure annuaires AD.</span><span class="sxs-lookup"><span data-stu-id="597b8-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="597b8-124">Cette fonctionnalité sera également déployée et activée sur les répertoires créés avant cette date.</span><span class="sxs-lookup"><span data-stu-id="597b8-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="597b8-125">Vous recevrez une notification par courrier électronique lorsque votre répertoire est sur tooget cette fonctionnalité est activée.</span><span class="sxs-lookup"><span data-stu-id="597b8-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="597b8-126">Hello les paramètres suivants sont configurés par Azure AD Connect et ne peut pas être modifiées par `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="597b8-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="597b8-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="597b8-127">DirSyncFeature</span></span> | <span data-ttu-id="597b8-128">Commentaire</span><span class="sxs-lookup"><span data-stu-id="597b8-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="597b8-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="597b8-129">DeviceWriteback</span></span> |[<span data-ttu-id="597b8-130">Azure AD Connect : Activation de l’écriture différée des appareils</span><span class="sxs-lookup"><span data-stu-id="597b8-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="597b8-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="597b8-131">DirectoryExtensions</span></span> |[<span data-ttu-id="597b8-132">Azure AD Connect Sync : extensions d’annuaire</span><span class="sxs-lookup"><span data-stu-id="597b8-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="597b8-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="597b8-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="597b8-134">Permet une toobe de l’attribut mis en quarantaine lorsqu’il est un doublon d’un autre objet plutôt que d’échec de l’objet complet hello lors de l’exportation.</span><span class="sxs-lookup"><span data-stu-id="597b8-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="597b8-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="597b8-135">PasswordSync</span></span> |[<span data-ttu-id="597b8-136">Implémentation de la synchronisation de mot de passe avec Azure AD Connect Sync</span><span class="sxs-lookup"><span data-stu-id="597b8-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="597b8-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="597b8-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="597b8-138">Version préliminaire : Écriture différée de groupe</span><span class="sxs-lookup"><span data-stu-id="597b8-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="597b8-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="597b8-139">UserWriteback</span></span> |<span data-ttu-id="597b8-140">Non pris en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="597b8-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="597b8-141">Résilience d’attribut en double</span><span class="sxs-lookup"><span data-stu-id="597b8-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="597b8-142">Au lieu d’échouer tooprovision objets avec les noms UPN en double / proxyAddresses, attribut dupliqué de hello est « mis en quarantaine » et une valeur temporaire est attribuée.</span><span class="sxs-lookup"><span data-stu-id="597b8-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="597b8-143">Lorsque les conflits hello sont résolu, hello temporaire UPN est modifié automatiquement de valeur correcte de toohello.</span><span class="sxs-lookup"><span data-stu-id="597b8-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="597b8-144">Pour plus d’informations, voir [Synchronisation des identités et résilience d’attribut en double](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="597b8-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="597b8-145">Correspondance souple UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="597b8-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="597b8-146">Lorsque cette fonctionnalité est activée, soft-match est activée pour l’UPN dans Ajout toohello [adresse SMTP principale](https://support.microsoft.com/kb/2641663), qui est toujours activé.</span><span class="sxs-lookup"><span data-stu-id="597b8-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="597b8-147">Soft-match est toomatch utilisé les utilisateurs existants de cloud dans Azure AD avec les utilisateurs locaux.</span><span class="sxs-lookup"><span data-stu-id="597b8-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="597b8-148">Si vous avez besoin toomatch AD comptes locaux avec les comptes existants créés dans le cloud de hello et vous n’utilisez pas Exchange Online, puis cette fonctionnalité est utile.</span><span class="sxs-lookup"><span data-stu-id="597b8-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="597b8-149">Dans ce scénario, vous ne généralement avez un attribut de raison tooset hello SMTP dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="597b8-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="597b8-150">Cette fonctionnalité est activée par défaut pour les répertoires Azure AD nouvellement créés.</span><span class="sxs-lookup"><span data-stu-id="597b8-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="597b8-151">Vous pouvez voir si cette fonctionnalité est activée en exécutant :</span><span class="sxs-lookup"><span data-stu-id="597b8-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="597b8-152">Si cette fonctionnalité n’est pas activée pour votre répertoire Azure AD, vous pouvez l’activer en exécutant :</span><span class="sxs-lookup"><span data-stu-id="597b8-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="597b8-153">Synchroniser les mises à jour userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="597b8-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="597b8-154">Historiquement, attribut UserPrincipalName de mises à jour toohello à l’aide du service de synchronisation hello du site a été bloqué, sauf si ces deux conditions sont remplies :</span><span class="sxs-lookup"><span data-stu-id="597b8-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="597b8-155">utilisateur de Hello est géré (non fédérés).</span><span class="sxs-lookup"><span data-stu-id="597b8-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="597b8-156">une licence n’a pas été affecté à l’utilisateur de Hello.</span><span class="sxs-lookup"><span data-stu-id="597b8-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="597b8-157">Pour plus d’informations, consultez [utilisateur noms dans Office 365, Azure ou Intune ne correspondent pas hello UPN local ou l’ID de connexion de remplacement](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="597b8-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="597b8-158">L’activation de cette fonctionnalité permet de hello synchronisation moteur tooupdate hello userPrincipalName quand il est modifié localement et vous utilisez la synchronisation de mot de passe. Si vous utilisez la fédération, cette fonctionnalité n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="597b8-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="597b8-159">Cette fonctionnalité est activée par défaut pour les répertoires Azure AD nouvellement créés.</span><span class="sxs-lookup"><span data-stu-id="597b8-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="597b8-160">Vous pouvez voir si cette fonctionnalité est activée en exécutant :</span><span class="sxs-lookup"><span data-stu-id="597b8-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="597b8-161">Si cette fonctionnalité n’est pas activée pour votre répertoire Azure AD, vous pouvez l’activer en exécutant :</span><span class="sxs-lookup"><span data-stu-id="597b8-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="597b8-162">Après avoir activé cette fonctionnalité, les valeurs existantes userPrincipalName demeurent telles quelles.</span><span class="sxs-lookup"><span data-stu-id="597b8-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="597b8-163">Sur la prochaine modification de hello userPrincipalName attribut locale, la synchronisation delta normal hello sur les utilisateurs mettent à jour hello UPN.</span><span class="sxs-lookup"><span data-stu-id="597b8-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="597b8-164">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="597b8-164">See also</span></span>
* [<span data-ttu-id="597b8-165">Synchronisation d’Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="597b8-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="597b8-166">[Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="597b8-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

