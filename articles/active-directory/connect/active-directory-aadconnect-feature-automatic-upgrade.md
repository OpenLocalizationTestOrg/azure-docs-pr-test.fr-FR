---
title: "Azure AD Connect : Mise à niveau automatique | Microsoft Docs"
description: "Cette rubrique décrit hello intégrés mise à niveau automatiques de synchronisation Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect : Mise à niveau automatique
Cette fonctionnalité a été introduite avec la version 1.1.105.0 (publiée en février 2016).

## <a name="overview"></a>Vue d'ensemble
S’assurer que votre installation de Azure AD Connect est toujours opérationnel toodate n’a jamais été plus facile avec hello **mise à niveau automatique** fonctionnalité. Cette fonctionnalité est activée par défaut pour les installations expresses et les mises à niveau de DirSync. Quand une nouvelle version est publiée, votre installation est mise à niveau automatiquement.

Mise à niveau automatique est activée par défaut pour les éléments suivants de hello :

* Installation de la configuration rapide et mises à niveau de DirSync.
* SQL Express LocalDB, toujours utilisée par la configuration rapide. DirSync avec SQL Express utilise également LocalDB.
* Hello compte Active Directory est compte MSOL_ de hello par défaut créé par les paramètres Express et la synchronisation d’annuaire.
* Avoir moins de 100 000 objets hello métaverse.

état actuel de Hello de mise à niveau automatique peut être affiché avec applet de commande PowerShell hello `Get-ADSyncAutoUpgrade`. Elle présente hello suivant les états suivants :

| State | Commentaire |
| --- | --- |
| Activé |La mise à niveau automatique est activée. |
| Interrompu |Définie par le système hello uniquement. Hello système n’est plus éligible tooreceive les mises à niveau automatiques. |
| Désactivé |La mise à niveau automatique est désactivée. |

Vous pouvez passer de **Activé** à **Désactivé** avec `Set-ADSyncAutoUpgrade`. Seul le système de hello doit définir l’état de hello **Suspended**.

Mise à niveau automatique est à l’aide de Azure AD Connect Health pour l’infrastructure de mise à niveau hello. Pour toowork de mise à niveau automatique, vérifiez que vous avez ouvert hello URL de votre serveur proxy pour **Azure AD Connect Health** comme documenté dans [plages d’adresses IP et des URL d’Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Si hello **Synchronization Service Manager** l’interface utilisateur est en cours d’exécution sur le serveur de hello, puis hello mise à niveau est interrompue jusqu'à ce que hello l’interface utilisateur est fermée.

## <a name="troubleshooting"></a>Résolution des problèmes
Si votre installation de se connecter ne met pas niveau lui-même comme prévu, suivez ces toofind étapes à ce qui peut être incorrect.

Tout d’abord, vous ne devez pas attendre hello toobe de mise à niveau automatique a tenté de hello premier jour, qu'une nouvelle version est disponible. Toute tentative de mise à niveau a un caractère aléatoire intentionnel. Ne vous inquiétez pas si votre installation n'est pas mise à niveau immédiatement.

Si vous pensez que quelque chose ne répond pas, puis d’abord exécuter `Get-ADSyncAutoUpgrade` tooensure la mise à niveau automatique est activée.

Vérifiez que vous avez ouvert l’URL de hello requis dans votre pare-feu ou un proxy. Mise à jour automatique est à l’aide de Azure AD Connect Health comme décrit dans hello [vue d’ensemble](#overview). Si vous utilisez un proxy, vérifiez que l’intégrité a été configuré toouse un [serveur proxy](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy). Également tester hello [connectivité d’intégrité](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure AD.

TooAzure de connectivité hello AD vérifié, il est toolook de temps dans les journaux d’événements hello. Démarrer l’Observateur d’événements hello et Regarder dans hello **Application** eventlog. Ajouter un filtre de journal des événements pour la source de hello **Azure AD connecter mise à niveau** et la plage d’id événement hello **300-399**.  
![Filtre de journal des événements pour la mise à niveau automatique](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

Vous pouvez maintenant voir les journaux d’événements hello associés au statut hello pour la mise à niveau automatique.  
![Filtre de journal des événements pour la mise à niveau automatique](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

code de résultat Hello possède un préfixe avec une vue d’ensemble de l’état de hello.

| Préfixe du code de résultat | Description |
| --- | --- |
| Succès |installation de Hello a été correctement mis à niveau. |
| UpgradeAborted |Une condition temporaire s’est arrêté de mise à niveau hello. Il va être retentée à nouveau et hello attend qu’il réussit ultérieurement. |
| UpgradeNotSupported |système de Hello possède une configuration qui bloque système hello automatiquement mise à niveau. Il sera retenté toosee si l’état hello est modifié, mais les attentes hello que hello système doit être mis à niveau manuellement. |

Voici une liste de messages les plus courants de hello que vous trouverez. Elle ne répertorie pas tous, mais message de résultat d’appel doit être clairement à quel problème hello est.

| Message de résultat | Description |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |N’a pas pu écrire toohello Registre. |
| UpgradeAbortedInsufficientDatabasePermissions |groupe d’administrateurs intégrés Hello n’a pas de base de données toohello d’autorisations. Mettre à niveau manuellement toohello version la plus récente d’Azure AD Connect tooaddress ce problème. |
| UpgradeAbortedInsufficientDiskSpace |Il n’existe pas assez toosupport d’espace disque pour une mise à niveau. |
| UpgradeAbortedSecurityGroupsNotPresent |Impossible de trouver et de résoudre tous les groupes de sécurité utilisés par le moteur de synchronisation hello. |
| UpgradeAbortedServiceCanNotBeStarted |Hello Service NT **Microsoft Azure AD Sync** échec toostart. |
| UpgradeAbortedServiceCanNotBeStopped |Hello Service NT **Microsoft Azure AD Sync** échec toostop. |
| UpgradeAbortedServiceIsNotRunning |Hello Service NT **Microsoft Azure AD Sync** n’est pas en cours d’exécution. |
| UpgradeAbortedSyncCycleDisabled |Hello option SyncCycle Bonjour [planificateur](active-directory-aadconnectsync-feature-scheduler.md) a été désactivé. |
| UpgradeAbortedSyncExeInUse |Hello [le Gestionnaire de service de synchronisation UI](active-directory-aadconnectsync-service-manager-ui.md) est ouvert sur le serveur de hello. |
| UpgradeAbortedSyncOrConfigurationInProgress |l’Assistant installation Hello est en cours d’exécution ou une synchronisation a été planifiée à l’extérieur du Planificateur de hello. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |Vous avez ajouté vos propres règles personnalisées toohello configuration. |
| UpgradeNotSupportedDeviceWritebackEnabled |Vous avez activé hello [l’écriture différée de l’appareil](active-directory-aadconnect-feature-device-writeback.md) fonctionnalité. |
| UpgradeNotSupportedGroupWritebackEnabled |Vous avez activé hello [l’écriture différée de groupe](active-directory-aadconnect-feature-preview.md#group-writeback) fonctionnalité. |
| UpgradeNotSupportedInvalidPersistedState |installation de Hello n’est pas un paramètres Express ou une mise à niveau de DirSync. |
| UpgradeNotSupportedMetaverseSizeExceeeded |Vous avez plus de 100 000 objets hello métaverse. |
| UpgradeNotSupportedMultiForestSetup |Vous vous connectez toomore qu’une seule forêt. Le programme d’installation Express connecte uniquement à tooone forêt. |
| UpgradeNotSupportedNonLocalDbInstall |Vous n’utilisez pas une base de données LocalDB SQL Server Express. |
| UpgradeNotSupportedNonMsolAccount |Hello [compte de connecteur AD](active-directory-aadconnect-accounts-permissions.md#active-directory-account) n’est pas compte MSOL_ par défaut hello plus. |
| UpgradeNotSupportedStagingModeEnabled |serveur de Hello a toobe [mode de préproduction](active-directory-aadconnectsync-operations.md#staging-mode). |
| UpgradeNotSupportedUserWritebackEnabled |Vous avez activé hello [écriture différée d’utilisateur](active-directory-aadconnect-feature-preview.md#user-writeback) fonctionnalité. |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
