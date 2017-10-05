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
ms.openlocfilehash: 947ea3c9d789ecf5a754001aafcda6f8bcd41047
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="792df-103">Activer la synchronisation du mot de passe pour Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="792df-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="792df-104">Dans les tâches précédentes, vous avez activé Azure Active Directory Domain Services pour votre locataire Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="792df-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="792df-105">Dans la tâche suivante, vous allez activer la synchronisation des hachages d’informations d’identification requis pour l’authentification NT LAN Manager (NTLM) et Kerberos avec Services de domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="792df-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="792df-106">Une fois la synchronisation des informations d’identification configurée, les utilisateurs peuvent se connecter au domaine managé à l’aide de leurs informations d’identification d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="792df-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="792df-107">Les étapes nécessaires sont différentes pour les comptes d’utilisateurs uniquement dans le cloud par rapport aux comptes d’utilisateurs qui sont synchronisés à partir de votre répertoire local à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="792df-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="792df-108">Si votre locataire Azure AD utilise une combinaison d’utilisateurs dans le cloud uniquement et d’utilisateurs provenant de votre répertoire Active Directory local, vous devez effectuer ces deux étapes.</span><span class="sxs-lookup"><span data-stu-id="792df-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="792df-109">**Comptes d’utilisateurs uniquement dans le cloud** : [synchroniser les mots de passe des comptes d’utilisateurs uniquement dans le cloud avec votre domaine géré](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="792df-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="792df-110">**Comptes d’utilisateurs locaux** : [synchroniser les mots de passe des comptes d’utilisateurs synchronisés à partir de votre répertoire Active Directory local avec votre domaine géré](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="792df-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="792df-111">Tâche 5 : activer la synchronisation de mot de passe avec votre domaine géré pour les comptes d’utilisateurs synchronisés avec votre répertoire Active Directory local</span><span class="sxs-lookup"><span data-stu-id="792df-111">Task 5: enable password synchronization to your managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="792df-112">Un client Azure AD connecté est défini pour se synchroniser avec le répertoire local de votre organisation à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="792df-112">A synced Azure AD tenant is set to synchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="792df-113">Par défaut, Azure AD Connect ne synchronise pas les hachages des informations d’identification NTLM et Kerberos avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="792df-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes to Azure AD.</span></span> <span data-ttu-id="792df-114">Pour utiliser les Services de domaine Azure AD, vous devez configurer Azure AD Connect pour synchroniser les hachages d’informations d’identification requis pour l’authentification NTLM et Kerberos.</span><span class="sxs-lookup"><span data-stu-id="792df-114">To use Azure AD Domain Services, you need to configure Azure AD Connect to synchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="792df-115">Les étapes suivantes permettent la synchronisation des hachages d’informations d’identification avec votre local Azure AD à partir de votre répertoire local.</span><span class="sxs-lookup"><span data-stu-id="792df-115">The following steps enable synchronization of the required credential hashes from your on-premises directory to your Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="792df-116">Si votre organisation utilise des comptes d’utilisateurs qui sont synchronisés à partir de votre répertoire local, vous devez activer la synchronisation des hachages NTLM et Kerberos afin d’utiliser le domaine géré.</span><span class="sxs-lookup"><span data-stu-id="792df-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order to use the managed domain.</span></span> <span data-ttu-id="792df-117">Un compte d’utilisateur synchronisé est un compte qui a été créé dans votre répertoire local puis synchronisé avec votre locataire Azure AD à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="792df-117">A synced user account is an account that was created in your on-premises directory and is synchronized to your Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="792df-118">Installer ou mettre à jour Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="792df-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="792df-119">Installer la dernière version recommandée d’Azure AD Connect sur un ordinateur joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="792df-119">Install the latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="792df-120">Si une instance d’Azure AD Connect est déjà configurée, vous devez la mettre à jour pour utiliser la dernière version d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="792df-120">If you have an existing instance of Azure AD Connect setup, you need to update it to use the latest version of Azure AD Connect.</span></span> <span data-ttu-id="792df-121">Veillez à utiliser la dernière version d’Azure AD Connect afin d’éviter les problèmes/bogues connus déjà corrigés.</span><span class="sxs-lookup"><span data-stu-id="792df-121">To avoid known issues/bugs that may have already been fixed, ensure you always use the latest version of Azure AD Connect.</span></span>

<span data-ttu-id="792df-122">**[Télécharger Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="792df-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="792df-123">Version minimale recommandée : **1.1.553.0** - publiée le 27 juin 2017.</span><span class="sxs-lookup"><span data-stu-id="792df-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="792df-124">Vous DEVEZ installer la dernière version recommandée d’Azure AD Connect pour que les informations d’identification de mot de passe héritées (nécessaires pour l’authentification NTLM et Kerberos) puissent être synchronisées avec votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="792df-124">You MUST install the latest recommended release of Azure AD Connect to enable the legacy password credentials (required for NTLM and Kerberos authentication) to synchronize to your Azure AD tenant.</span></span> <span data-ttu-id="792df-125">Cette fonctionnalité n’est pas disponible dans les versions antérieures d’Azure AD Connect ou avec l’outil DirSync hérité.</span><span class="sxs-lookup"><span data-stu-id="792df-125">This functionality is not available in prior releases of Azure AD Connect or with the legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="792df-126">Les instructions d’installation d’Azure AD Connect sont disponibles dans l’article suivant : [Prise en main d’Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="792df-126">Installation instructions for Azure AD Connect are available in the following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-to-azure-ad"></a><span data-ttu-id="792df-127">Activez la synchronisation des hachages des informations d’identification NTLM et Kerberos avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="792df-127">Enable synchronization of NTLM and Kerberos credential hashes to Azure AD</span></span>
<span data-ttu-id="792df-128">Exécutez le script PowerShell suivant sur chaque forêt AD, pour forcer la synchronisation de mot de passe complète, et permettre à tous les hachages d’informations d’identification des utilisateurs locaux de se synchroniser avec votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="792df-128">Execute the following PowerShell script on each AD forest, to force full password synchronization, and enable all on-premises users’ credential hashes to sync to your Azure AD tenant.</span></span> <span data-ttu-id="792df-129">Ce script permet les hachages d’informations d’identification requis pour que l’authentification NTLM/Kerberos soit synchronisée avec votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="792df-129">This script enables the credential hashes required for NTLM/Kerberos authentication to be synchronized to your Azure AD tenant.</span></span>

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

<span data-ttu-id="792df-130">En fonction de la taille de votre répertoire (nombre d’utilisateurs, de groupes, etc.), la synchronisation des hachages d’informations d’identification avec Azure AD peut prendre du temps.</span><span class="sxs-lookup"><span data-stu-id="792df-130">Depending on the size of your directory (number of users, groups etc.), synchronization of credential hashes to Azure AD takes time.</span></span> <span data-ttu-id="792df-131">Les mots de passe seront utilisables sur le domaine géré de Services de domaine Azure AD peu après la synchronisation des hachages d'informations d'identification avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="792df-131">The passwords will be usable on the Azure AD Domain Services managed domain shortly after the credential hashes have synchronized to Azure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="792df-132">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="792df-132">Related Content</span></span>
* [<span data-ttu-id="792df-133">Activer la synchronisation de mot de passe pour les services de domaine AAD pour un répertoire Azure AD uniquement dans le cloud</span><span class="sxs-lookup"><span data-stu-id="792df-133">Enable password synchronization to AAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="792df-134">Administrer un domaine géré par les services de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="792df-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="792df-135">Joindre une machine virtuelle Windows à un domaine géré par les services de domaine Azure AD</span><span class="sxs-lookup"><span data-stu-id="792df-135">Join a Windows virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="792df-136">Joindre une machine virtuelle Linux Red Hat Enterprise à un domaine géré par les services de domaine Azure AD</span><span class="sxs-lookup"><span data-stu-id="792df-136">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
