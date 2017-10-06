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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Activer la synchronisation de mot de passe tooAzure les Services de domaine Active Directory
Dans les tâches précédentes, vous avez activé Azure Active Directory Domain Services pour votre locataire Azure Active Directory (Azure AD). la tâche suivante Hello est synchronisation tooenable des hachages d’informations d’identification requises pour tooAzure de l’authentification NT LAN Manager (NTLM) et Kerberos, les Services de domaine Active Directory. Une fois que vous avez configuré la synchronisation des informations d’identification, les utilisateurs peuvent se connecter dans toohello le domaine géré avec leurs informations d’identification d’entreprise.

Hello différentes étapes sont différents pour les comptes d’utilisateur utilisateur cloud uniquement les comptes Visual Studio qui sont synchronisés à partir de votre annuaire local à l’aide d’Azure AD Connect. Si votre client Azure AD a une combinaison de cloud uniquement les utilisateurs et les utilisateurs de votre service Active Directory, vous devez tooperform les deux étapes.

<br>

> [!div class="op_single_selector"]
> * **Comptes d’utilisateur uniquement dans le cloud**: [synchroniser les mots de passe pour le domaine géré de tooyour des comptes d’utilisateurs uniquement dans le cloud](active-directory-ds-getting-started-password-sync.md)
> * **Comptes d’utilisateur locaux**: [synchroniser les mots de passe des comptes d’utilisateur synchronisés à partir de votre site AD tooyour gérés domaine](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Tâche 5 : activer le mot de passe tooyour managé domaine de synchronisation des comptes d’utilisateur synchronisé avec votre service Active Directory
A été synchronisés à Azure client AD a la valeur toosynchronize avec l’annuaire local de votre organisation à l’aide d’Azure AD Connect. Par défaut, Azure AD Connect ne synchronise pas NTLM et Kerberos tooAzure hachages d’informations d’identification Active Directory. toouse les Services de domaine Active Directory de Azure, vous devez les hachages d’informations d’identification tooconfigure Azure AD Connect toosynchronize requis pour l’authentification NTLM et Kerberos. Hello suit activer la synchronisation des hachages d’informations d’identification hello requis du locataire Azure AD tooyour de votre répertoire local.

> [!NOTE]
> Si votre organisation a des comptes d’utilisateur qui sont synchronisés à partir de votre annuaire local, vous devez activer la synchronisation des hachages NTLM et Kerberos dans un domaine géré de commande toouse hello. Un compte d’utilisateur synchronisé est un compte qui a été créé dans votre annuaire local et synchronisés tooyour client de Azure AD à l’aide d’Azure AD Connect.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Installer ou mettre à jour Azure AD Connect
Installer hello recommandé de la dernière version d’Azure AD Connect sur un domaine joint l’ordinateur. Si vous avez une instance existante de l’installation d’Azure AD Connect, vous devez tooupdate il toouse hello dernière version d’Azure AD Connect. tooavoid problèmes/bogues qui peuvent avoir déjà été résolu, vérifiez que vous utilisez toujours la version la plus récente d’Azure AD Connect hello.

**[Télécharger Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

Version minimale recommandée : **1.1.553.0** - publiée le 27 juin 2017.

> [!WARNING]
> Vous devez installer hello plus tard recommandé de mise en production de Azure AD Connect tooenable hello hérité de mot de passe les informations d’identification (requises pour l’authentification NTLM et Kerberos) toosynchronize tooyour Azure AD client. Cette fonctionnalité n’est pas disponible dans les versions antérieures d’Azure AD Connect ou avec l’outil de synchronisation d’annuaire hello hérité.
>
>

Instructions d’installation de Azure AD Connect sont disponibles dans les éléments suivants de hello article - [prise en main d’Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>Activer la synchronisation de NTLM et Kerberos tooAzure hachages d’informations d’identification Active Directory
Exécutez hello suivant de script PowerShell de chaque forêt Active Directory, synchronisation de mot de passe complète tooforce et activer le client de tous les utilisateurs locaux d’informations d’identification hachages toosync tooyour Azure AD. Ce script permet de hachages des informations d’identification hello requises pour le client NTLM/Kerberos authentication toobe tooyour synchronisé Azure AD.

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

Selon la taille de hello de votre annuaire (nombre d’utilisateurs, groupes etc.), la synchronisation des informations d’identification hache tooAzure AD du temps. les mots de passe Hello seront utilisable sur le domaine géré de Services de domaine Active Directory de Azure hello peu de temps après que les hachages d’informations d’identification hello ont synchronisé tooAzure AD.

<br>

## <a name="related-content"></a>Contenu connexe
* [Activer la synchronisation de mot de passe tooAAD des Services de domaine pour un Azure cloud uniquement annuaire AD](active-directory-ds-getting-started-password-sync.md)
* [Administrer un domaine géré par les services de domaine Azure Active Directory](active-directory-ds-admin-guide-administer-domain.md)
* [Joindre un domaine géré Windows machine virtuelle tooan des Services de domaine Active Directory de Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Red Hat Enterprise Linux](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
