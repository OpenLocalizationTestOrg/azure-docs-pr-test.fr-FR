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
# <a name="azure-ad-connect-sync-service-features"></a>Fonctionnalités de service de synchronisation d’Azure AD Connect
fonctionnalité de synchronisation Hello d’Azure AD Connect comporte deux composants :

* composant de local Hello nommé **synchronisation Azure AD Connect**, également appelé **moteur de synchronisation**.
* service Hello résidant dans Azure AD, également appelé **service de synchronisation Azure AD Connect**

Cette rubrique explique comment les fonctionnalités hello suivant de hello **service de synchronisation Azure AD Connect** travail et comment vous pouvez les configurer à l’aide de Windows PowerShell.

Ces paramètres sont configurés par hello [Azure Module Active Directory pour Windows PowerShell](http://aka.ms/aadposh). Téléchargez et installez-le séparément à partir d’Azure AD Connect. applets de commande Hello documentées dans cette rubrique ont été introduits dans hello [version de mars 2016 (version 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Si vous n’avez pas les applets de commande hello documentées dans cette rubrique, ou ils ne produisent pas hello même résultat, puis vérifiez que vous exécutez la version la plus récente hello.

configuration de hello toosee dans votre annuaire Azure AD, exécutez `Get-MsolDirSyncFeatures`.  
![Résultat de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Plusieurs de ces paramètres peuvent uniquement être modifiés par Azure AD Connect.

Hello paramètres suivants peuvent être configurés par `Set-MsolDirSyncFeature`:

| DirSyncFeature | Commentaire |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Permet de toojoin d’objets sur userPrincipalName dans adresse de tooprimary SMTP d’addition. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Permet attribut userPrincipalName de hello synchronisation moteur tooupdate hello gérés/de licence (non fédérés) aux utilisateurs. |

Lorsqu’une fonctionnalité a été activée, vous ne pouvez plus la désactiver.

> [!NOTE]
> À partir du 24 août 2016 hello fonctionnalité *dupliquer la résilience de l’attribut* est activée par défaut pour nouveau Azure annuaires AD. Cette fonctionnalité sera également déployée et activée sur les répertoires créés avant cette date. Vous recevrez une notification par courrier électronique lorsque votre répertoire est sur tooget cette fonctionnalité est activée.
> 
> 

Hello les paramètres suivants sont configurés par Azure AD Connect et ne peut pas être modifiées par `Set-MsolDirSyncFeature`:

| DirSyncFeature | Commentaire |
| --- | --- |
| DeviceWriteback |[Azure AD Connect : Activation de l’écriture différée des appareils](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Azure AD Connect Sync : extensions d’annuaire](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Permet une toobe de l’attribut mis en quarantaine lorsqu’il est un doublon d’un autre objet plutôt que d’échec de l’objet complet hello lors de l’exportation. |
| PasswordSync |[Implémentation de la synchronisation de mot de passe avec Azure AD Connect Sync](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Version préliminaire : Écriture différée de groupe](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |Non pris en charge pour le moment. |

## <a name="duplicate-attribute-resiliency"></a>Résilience d’attribut en double
Au lieu d’échouer tooprovision objets avec les noms UPN en double / proxyAddresses, attribut dupliqué de hello est « mis en quarantaine » et une valeur temporaire est attribuée. Lorsque les conflits hello sont résolu, hello temporaire UPN est modifié automatiquement de valeur correcte de toohello. Pour plus d’informations, voir [Synchronisation des identités et résilience d’attribut en double](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>Correspondance souple UserPrincipalName
Lorsque cette fonctionnalité est activée, soft-match est activée pour l’UPN dans Ajout toohello [adresse SMTP principale](https://support.microsoft.com/kb/2641663), qui est toujours activé. Soft-match est toomatch utilisé les utilisateurs existants de cloud dans Azure AD avec les utilisateurs locaux.

Si vous avez besoin toomatch AD comptes locaux avec les comptes existants créés dans le cloud de hello et vous n’utilisez pas Exchange Online, puis cette fonctionnalité est utile. Dans ce scénario, vous ne généralement avez un attribut de raison tooset hello SMTP dans le cloud de hello.

Cette fonctionnalité est activée par défaut pour les répertoires Azure AD nouvellement créés. Vous pouvez voir si cette fonctionnalité est activée en exécutant :  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Si cette fonctionnalité n’est pas activée pour votre répertoire Azure AD, vous pouvez l’activer en exécutant :  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>Synchroniser les mises à jour userPrincipalName
Historiquement, attribut UserPrincipalName de mises à jour toohello à l’aide du service de synchronisation hello du site a été bloqué, sauf si ces deux conditions sont remplies :

* utilisateur de Hello est géré (non fédérés).
* une licence n’a pas été affecté à l’utilisateur de Hello.

Pour plus d’informations, consultez [utilisateur noms dans Office 365, Azure ou Intune ne correspondent pas hello UPN local ou l’ID de connexion de remplacement](https://support.microsoft.com/kb/2523192).

L’activation de cette fonctionnalité permet de hello synchronisation moteur tooupdate hello userPrincipalName quand il est modifié localement et vous utilisez la synchronisation de mot de passe. Si vous utilisez la fédération, cette fonctionnalité n’est pas prise en charge.

Cette fonctionnalité est activée par défaut pour les répertoires Azure AD nouvellement créés. Vous pouvez voir si cette fonctionnalité est activée en exécutant :  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Si cette fonctionnalité n’est pas activée pour votre répertoire Azure AD, vous pouvez l’activer en exécutant :  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

Après avoir activé cette fonctionnalité, les valeurs existantes userPrincipalName demeurent telles quelles. Sur la prochaine modification de hello userPrincipalName attribut locale, la synchronisation delta normal hello sur les utilisateurs mettent à jour hello UPN.  

## <a name="see-also"></a>Voir aussi
* [Synchronisation d’Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

