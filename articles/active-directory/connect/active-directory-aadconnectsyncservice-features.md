---
title: "Fonctionnalités et configuration du service Azure AD Connect | Microsoft Docs"
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
ms.openlocfilehash: c2873510c280a2683c235cfdce3d2617c3b665cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="419b5-103">Fonctionnalités de service de synchronisation d’Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="419b5-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="419b5-104">La fonctionnalité de synchronisation d’Azure AD Connect comprend deux composants :</span><span class="sxs-lookup"><span data-stu-id="419b5-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="419b5-105">Le composant local nommé **Azure AD Connect sync**, également appelé **moteur de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="419b5-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="419b5-106">Le service résidant dans Azure AD, également appelé **service de synchronisation Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="419b5-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="419b5-107">Cette rubrique explique comment les fonctionnalités suivantes du **service de synchronisation Azure AD Connect** opèrent et comment les configurer à l’aide de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="419b5-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="419b5-108">Ces paramètres sont configurés à partir du [module Azure Active Directory pour Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="419b5-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="419b5-109">Téléchargez et installez-le séparément à partir d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="419b5-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="419b5-110">Les applets de commande documentées dans cette rubrique ont été introduites dans la [version de mars 2016 (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="419b5-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="419b5-111">Si vous n’avez pas les applets de commande documentées dans cette rubrique, ou que vous n’obtenez pas le même résultat, vérifiez que vous exécutez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="419b5-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="419b5-112">Pour afficher la configuration de votre répertoire Azure AD, exécutez `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="419b5-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="419b5-113">![Résultat de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="419b5-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="419b5-114">Plusieurs de ces paramètres peuvent uniquement être modifiés par Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="419b5-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="419b5-115">Les paramètres suivants peuvent être configurés par `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="419b5-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="419b5-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="419b5-116">DirSyncFeature</span></span> | <span data-ttu-id="419b5-117">Commentaire</span><span class="sxs-lookup"><span data-stu-id="419b5-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="419b5-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="419b5-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="419b5-119">Permet aux objets d’être joints sur userPrincipalName en plus de l’adresse SMTP principale.</span><span class="sxs-lookup"><span data-stu-id="419b5-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="419b5-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="419b5-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="419b5-121">Permet au moteur de synchronisation de mettre à jour l’attribut userPrincipalName pour les utilisateurs gérés/licenciés(non fédérés).</span><span class="sxs-lookup"><span data-stu-id="419b5-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="419b5-122">Lorsqu’une fonctionnalité a été activée, vous ne pouvez plus la désactiver.</span><span class="sxs-lookup"><span data-stu-id="419b5-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="419b5-123">Depuis le 24 août 2016, la fonctionnalité *Résilience d’attribut en double* est activée par défaut pour les nouveaux répertoires Azure AD.</span><span class="sxs-lookup"><span data-stu-id="419b5-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="419b5-124">Cette fonctionnalité sera également déployée et activée sur les répertoires créés avant cette date.</span><span class="sxs-lookup"><span data-stu-id="419b5-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="419b5-125">Vous recevrez une notification par courrier électronique lorsque l’activation de cette fonctionnalité pour votre répertoire sera imminente .</span><span class="sxs-lookup"><span data-stu-id="419b5-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="419b5-126">Les paramètres suivants sont configurés par Azure AD Connect et ne peuvent pas être modifiés par `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="419b5-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="419b5-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="419b5-127">DirSyncFeature</span></span> | <span data-ttu-id="419b5-128">Commentaire</span><span class="sxs-lookup"><span data-stu-id="419b5-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="419b5-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="419b5-129">DeviceWriteback</span></span> |[<span data-ttu-id="419b5-130">Azure AD Connect : Activation de l’écriture différée des appareils</span><span class="sxs-lookup"><span data-stu-id="419b5-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="419b5-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="419b5-131">DirectoryExtensions</span></span> |[<span data-ttu-id="419b5-132">Azure AD Connect Sync : extensions d’annuaire</span><span class="sxs-lookup"><span data-stu-id="419b5-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="419b5-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="419b5-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="419b5-134">Permet à un attribut d’être mis en quarantaine lorsqu’il est un doublon d’un autre objet, plutôt que mettre en échec l’objet entier lors de l’exportation.</span><span class="sxs-lookup"><span data-stu-id="419b5-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="419b5-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="419b5-135">PasswordSync</span></span> |[<span data-ttu-id="419b5-136">Implémentation de la synchronisation de mot de passe avec Azure AD Connect Sync</span><span class="sxs-lookup"><span data-stu-id="419b5-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="419b5-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="419b5-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="419b5-138">Version préliminaire : Écriture différée de groupe</span><span class="sxs-lookup"><span data-stu-id="419b5-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="419b5-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="419b5-139">UserWriteback</span></span> |<span data-ttu-id="419b5-140">Non pris en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="419b5-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="419b5-141">Résilience d’attribut en double</span><span class="sxs-lookup"><span data-stu-id="419b5-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="419b5-142">Au lieu de rencontrer des problèmes lors de l’approvisionnement des UPN/proxyAddresses en double, l’attribut en double est « mis en quarantaine » et une valeur temporaire lui est attribuée.</span><span class="sxs-lookup"><span data-stu-id="419b5-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="419b5-143">Lorsque le conflit est résolu, l’UPN temporaire est automatiquement converti dans la valeur correcte.</span><span class="sxs-lookup"><span data-stu-id="419b5-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="419b5-144">Pour plus d’informations, voir [Synchronisation des identités et résilience d’attribut en double](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="419b5-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="419b5-145">Correspondance souple UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="419b5-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="419b5-146">Lorsque cette fonctionnalité est activée, la correspondance souple est activée pour l’UPN ainsi que pour l’ [adresse SMTP principale](https://support.microsoft.com/kb/2641663), qui est toujours activée.</span><span class="sxs-lookup"><span data-stu-id="419b5-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="419b5-147">La correspondance souple est utilisée pour faire correspondre les utilisateurs existants du cloud dans Azure AD avec les utilisateurs locaux.</span><span class="sxs-lookup"><span data-stu-id="419b5-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="419b5-148">Cette fonctionnalité est utile lorsque vous mettez en correspondance des comptes AD locaux avec des comptes existants créés dans le cloud, et que vous n’utilisez pas Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="419b5-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="419b5-149">Dans ce scénario, vous n’avez généralement pas de raison pour définir l’attribut SMTP dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="419b5-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="419b5-150">Cette fonctionnalité est activée par défaut pour les répertoires Azure AD nouvellement créés.</span><span class="sxs-lookup"><span data-stu-id="419b5-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="419b5-151">Vous pouvez voir si cette fonctionnalité est activée en exécutant :</span><span class="sxs-lookup"><span data-stu-id="419b5-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="419b5-152">Si cette fonctionnalité n’est pas activée pour votre répertoire Azure AD, vous pouvez l’activer en exécutant :</span><span class="sxs-lookup"><span data-stu-id="419b5-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="419b5-153">Synchroniser les mises à jour userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="419b5-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="419b5-154">Historiquement, les mises à jour de l’attribut UserPrincipalName à l’aide du service de synchronisation du site ont été bloquées, sauf si les deux conditions suivantes sont remplies :</span><span class="sxs-lookup"><span data-stu-id="419b5-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="419b5-155">L’utilisateur est géré (non fédéré).</span><span class="sxs-lookup"><span data-stu-id="419b5-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="419b5-156">Aucune licence n’a été attribuée à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="419b5-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="419b5-157">Pour plus d’informations, voir [Les noms d’utilisateur dans Office 365, Azure ou Intune ne correspondent pas à l’UPN local ou à l’ID de connexion secondaire](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="419b5-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="419b5-158">L’activation de cette fonctionnalité permet au moteur de synchronisation de mettre à jour l’attribut userPrincipalName lorsqu’il est modifié en local et que vous utilisez la synchronisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="419b5-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync.</span></span> <span data-ttu-id="419b5-159">Si vous utilisez la fédération, cette fonctionnalité n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="419b5-159">If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="419b5-160">Cette fonctionnalité est activée par défaut pour les répertoires Azure AD nouvellement créés.</span><span class="sxs-lookup"><span data-stu-id="419b5-160">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="419b5-161">Vous pouvez voir si cette fonctionnalité est activée en exécutant :</span><span class="sxs-lookup"><span data-stu-id="419b5-161">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="419b5-162">Si cette fonctionnalité n’est pas activée pour votre répertoire Azure AD, vous pouvez l’activer en exécutant :</span><span class="sxs-lookup"><span data-stu-id="419b5-162">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="419b5-163">Après avoir activé cette fonctionnalité, les valeurs existantes userPrincipalName demeurent telles quelles.</span><span class="sxs-lookup"><span data-stu-id="419b5-163">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="419b5-164">Lors de la prochaine modification de l’attribut userPrincipalName en local, la synchronisation delta normale sur les utilisateurs met à jour l’UPN.</span><span class="sxs-lookup"><span data-stu-id="419b5-164">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="419b5-165">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="419b5-165">See also</span></span>
* [<span data-ttu-id="419b5-166">Synchronisation d’Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="419b5-166">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="419b5-167">[Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="419b5-167">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

