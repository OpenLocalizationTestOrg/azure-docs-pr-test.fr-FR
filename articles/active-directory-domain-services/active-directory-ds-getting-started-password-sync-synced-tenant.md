---
title: 'Services de domaine Azure AD : Activer la synchronisation de mot de passe | Microsoft Docs'
description: Prise en main des services de domaine Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="1d1b1-103">Activer la synchronisation de mot de passe tooAzure les Services de domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d1b1-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="1d1b1-104">Dans les tâches précédentes, vous avez activé Azure Active Directory Domain Services pour votre locataire Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d1b1-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="1d1b1-105">la tâche suivante Hello est synchronisation tooenable des hachages d’informations d’identification requises pour tooAzure de l’authentification NT LAN Manager (NTLM) et Kerberos, les Services de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="1d1b1-106">Une fois que vous avez configuré la synchronisation des informations d’identification, les utilisateurs peuvent se connecter dans toohello le domaine géré avec leurs informations d’identification d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="1d1b1-107">Hello différentes étapes sont différents pour les comptes d’utilisateur utilisateur cloud uniquement les comptes Visual Studio qui sont synchronisés à partir de votre annuaire local à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="1d1b1-108">Si votre client Azure AD a une combinaison de cloud uniquement les utilisateurs et les utilisateurs de votre service Active Directory, vous devez tooperform les deux étapes.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="1d1b1-109">**Comptes d’utilisateur uniquement dans le cloud**: [synchroniser les mots de passe pour le domaine géré de tooyour des comptes d’utilisateurs uniquement dans le cloud](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="1d1b1-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="1d1b1-110">**Comptes d’utilisateur locaux**: [synchroniser les mots de passe des comptes d’utilisateur synchronisés à partir de votre site AD tooyour gérés domaine](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="1d1b1-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="1d1b1-111">Tâche 5 : activer le mot de passe tooyour managé domaine de synchronisation des comptes d’utilisateur synchronisé avec votre service Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d1b1-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="1d1b1-112">A été synchronisés à Azure client AD a la valeur toosynchronize avec l’annuaire local de votre organisation à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="1d1b1-113">Par défaut, Azure AD Connect ne synchronise pas NTLM et Kerberos tooAzure hachages d’informations d’identification Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="1d1b1-114">toouse les Services de domaine Active Directory de Azure, vous devez les hachages d’informations d’identification tooconfigure Azure AD Connect toosynchronize requis pour l’authentification NTLM et Kerberos.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="1d1b1-115">Hello suit activer la synchronisation des hachages d’informations d’identification hello requis du locataire Azure AD tooyour de votre répertoire local.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="1d1b1-116">Si votre organisation a des comptes d’utilisateur qui sont synchronisés à partir de votre annuaire local, vous devez activer la synchronisation des hachages NTLM et Kerberos dans un domaine géré de commande toouse hello.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="1d1b1-117">Un compte d’utilisateur synchronisé est un compte qui a été créé dans votre annuaire local et synchronisés tooyour client de Azure AD à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="1d1b1-118">Installer ou mettre à jour Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="1d1b1-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="1d1b1-119">Installer hello recommandé de la dernière version d’Azure AD Connect sur un domaine joint l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="1d1b1-120">Si vous avez une instance existante de l’installation d’Azure AD Connect, vous devez tooupdate il toouse hello dernière version d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="1d1b1-121">tooavoid problèmes/bogues qui peuvent avoir déjà été résolu, vérifiez que vous utilisez toujours la version la plus récente d’Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="1d1b1-122">**[Télécharger Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="1d1b1-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="1d1b1-123">Version minimale recommandée : **1.1.553.0** - publiée le 27 juin 2017.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="1d1b1-124">Vous devez installer hello plus tard recommandé de mise en production de Azure AD Connect tooenable hello hérité de mot de passe les informations d’identification (requises pour l’authentification NTLM et Kerberos) toosynchronize tooyour Azure AD client.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="1d1b1-125">Cette fonctionnalité n’est pas disponible dans les versions antérieures d’Azure AD Connect ou avec l’outil de synchronisation d’annuaire hello hérité.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="1d1b1-126">Instructions d’installation de Azure AD Connect sont disponibles dans les éléments suivants de hello article - [prise en main d’Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="1d1b1-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="1d1b1-127">Activer la synchronisation de NTLM et Kerberos tooAzure hachages d’informations d’identification Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d1b1-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="1d1b1-128">Exécutez hello suivant de script PowerShell de chaque forêt Active Directory, synchronisation de mot de passe complète tooforce et activer le client de tous les utilisateurs locaux d’informations d’identification hachages toosync tooyour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="1d1b1-129">Ce script permet de hachages des informations d’identification hello requises pour le client NTLM/Kerberos authentication toobe tooyour synchronisé Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="1d1b1-130">Selon la taille de hello de votre annuaire (nombre d’utilisateurs, groupes etc.), la synchronisation des informations d’identification hache tooAzure AD du temps.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="1d1b1-131">les mots de passe Hello seront utilisable sur le domaine géré de Services de domaine Active Directory de Azure hello peu de temps après que les hachages d’informations d’identification hello ont synchronisé tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="1d1b1-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="1d1b1-132">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="1d1b1-132">Related Content</span></span>
* [<span data-ttu-id="1d1b1-133">Activer la synchronisation de mot de passe tooAAD des Services de domaine pour un Azure cloud uniquement annuaire AD</span><span class="sxs-lookup"><span data-stu-id="1d1b1-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="1d1b1-134">Administrer un domaine géré par les services de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d1b1-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="1d1b1-135">Joindre un domaine géré Windows machine virtuelle tooan des Services de domaine Active Directory de Azure</span><span class="sxs-lookup"><span data-stu-id="1d1b1-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="1d1b1-136">Joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="1d1b1-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
