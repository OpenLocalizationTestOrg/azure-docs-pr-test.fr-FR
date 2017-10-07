---
title: Planificateur Azure AD Connect Sync | Microsoft Docs
description: "Cette rubrique décrit la fonctionnalité Planificateur intégré hello de synchronisation Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Planificateur Azure AD Connect Sync
Cette rubrique décrit le Planificateur intégré de hello dans la synchronisation Azure AD Connect (aussi appelé) moteur de synchronisation).

Cette fonctionnalité a été introduite avec la version 1.1.105.0 (publiée en février 2016).

## <a name="overview"></a>Vue d’ensemble
La synchronisation Azure AD Connect synchronise les modifications dans votre répertoire local à l’aide d’un planificateur. Il existe deux processus de planificateur, l’un pour la synchronisation de mot de passe et l’autre pour la synchronisation d’attribut/d’objet, ainsi que des tâches de maintenance. Cette rubrique couvre hello ce dernier.

Dans les versions antérieures, le planificateur hello pour les objets et attributs a été moteur de synchronisation toohello externe. Il utilisé le Planificateur de tâches Windows ou un processus de synchronisation hello distinct Windows service tootrigger. Planificateur de Hello est avec hello du moteur de synchronisation intégré toohello les versions 1.1 et n’autorisent pas les personnaliser. fréquence de synchronisation Hello nouvelle valeur par défaut est 30 minutes.

Hello planificateur est chargé de deux tâches :

* **Cycle de synchronisation**. Hello processus tooimport, synchronisation et les modifications de l’exportation.
* **Tâches de maintenance**. Renouvelle les clés et les certificats pour la réinitialisation de mot de passe et le service DRS (Device Registration Service). Purger les anciennes entrées dans le journal des opérations hello.

Planificateur Hello elle-même est toujours en cours d’exécution, mais il peut être configuré tooonly exécuter un ou aucun de ces tâches. Par exemple, si vous devez toohave votre propre processus de cycle de synchronisation, vous pouvez désactiver cette tâche dans le Planificateur de hello, mais la tâche de maintenance toujours exécution hello.

## <a name="scheduler-configuration"></a>Configuration du planificateur
toosee vos paramètres de configuration en cours, accédez tooPowerShell et exécutez `Get-ADSyncScheduler`. Vous obtenez un écran semblable à celui-ci :

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

Si vous voyez **commande de synchronisation hello ou l’applet de commande n’est pas disponible** lorsque vous exécutez cette applet de commande, puis module PowerShell de hello n'est pas chargé. Ce problème peut se produire si vous exécutez Azure AD Connect sur un contrôleur de domaine ou sur un serveur avec des niveaux de restriction PowerShell plus élevés que les paramètres par défaut de hello. Si vous voyez cette erreur, puis exécutez `Import-Module ADSync` cmdlet de hello toomake disponible.

* **AllowedSyncCycleInterval**. Hello plus court intervalle de temps entre les cycles de synchronisation autorisé par Azure AD. Vous ne pouvez pas synchroniser plus fréquemment que ne le spécifie ce paramètre tout en maintenant la prise en charge.
* **CurrentlyEffectiveSyncCycleInterval**. planification Hello actuellement en vigueur. Il a les mêmes valeurs que CustomizedSyncInterval de hello (si défini) si ce n’est plus fréquent que AllowedSyncInterval. Si vous utilisez une version antérieure à 1.1.281 et que vous modifiez CustomizedSyncCycleInterval, cette modification prendra effet après le prochain cycle de synchronisation. À partir de la build 1.1.281 hello prendra effet immédiatement.
* **CustomizedSyncCycleInterval**. Si vous souhaitez toorun de planificateur hello à n’importe quel autre fréquence par défaut de hello 30 minutes, puis vous configurez ce paramètre. Dans l’image hello ci-dessus, le planificateur hello a été défini toorun toutes les heures à la place. Si vous définissez cette valeur du paramètre tooa inférieur à AllowedSyncInterval, hello ce dernier est utilisé.
* **NextSyncCyclePolicyType**. Delta ou Initial. Définit si hello prochaine exécution doit uniquement les modifications delta processus, ou si hello prochaine exécution doit effectuer un complet importer et synchroniser. Hello ce dernier est également retraiter les règles de nouveaux ou modifiés.
* **NextSyncCycleStartTimeInUTC**. Lors du prochain démarrage du Planificateur de hello hello prochain cycle de synchronisation.
* **PurgeRunHistoryInterval**. Bonjour fonctionnement des temps de journaux doivent être conservés. Ces journaux peuvent être examinés dans le Gestionnaire de service de synchronisation hello. Hello par défaut est tookeep ces journaux pendant 7 jours.
* **SyncCycleEnabled**. Indique si le planificateur hello est en cours d’exécution hello importation, la synchronisation et les processus d’exportation dans le cadre de son fonctionnement.
* **MaintenanceEnabled**. Indique si le processus de maintenance hello est activé. Il met à jour les clés/certificats hello et purge hello journal des opérations.
* **StagingModeEnabled**. Indique si le [mode intermédiaire](active-directory-aadconnectsync-operations.md#staging-mode) est activé. Si ce paramètre est activé, il supprime les exportations hello de s’exécuter, mais toujours exécuter l’importation et la synchronisation.
* **SchedulerSuspended**. Définir à se connecter pendant un planificateur hello du bloc tootemporarily mise à niveau à partir de l’exécution.

Vous pouvez modifier certains de ces paramètres avec `Set-ADSyncScheduler`. Hello paramètres suivants peut être modifié :

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

Dans les versions antérieures d’Azure AD Connect, **isStagingModeEnabled** était exposé dans Set-ADSyncScheduler. Il s’agit de **non pris en charge** tooset cette propriété. Hello propriété **SchedulerSuspended** doit uniquement être modifié par connexion. Il s’agit de **non pris en charge** tooset avec PowerShell directement.

configuration de planification Hello est stockée dans Azure AD. Si vous avez un serveur intermédiaire, toute modification sur le serveur principal de hello affecte également hello serveur (sauf IsStagingModeEnabled) intermédiaire.

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Syntaxe : `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d - jours, HH - heures, mm - minutes, ss - secondes

Exemple : `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Modifications hello planificateur toorun toutes les 3 heures.

Exemple : `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
Les modifications hello planificateur toorun tous les jours.

### <a name="disable-hello-scheduler"></a>Désactiver le Planificateur de hello  
Si vous avez besoin de modifications de configuration toomake, puis vous souhaitez que toodisable hello planificateur. Par exemple, lorsque vous [configurer le filtrage](active-directory-aadconnectsync-configure-filtering.md) ou [apporter des modifications des règles de toosynchronization](active-directory-aadconnectsync-change-the-configuration.md).

Planificateur de hello toodisable, exécutez `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Désactiver le Planificateur de hello](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

Lorsque vous avez effectué vos modifications, n’oubliez pas de planificateur de hello tooenable avec `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-hello-scheduler"></a>Démarrez le Planificateur de hello
Planificateur de Hello est exécutent toutes les 30 minutes par défaut. Dans certains cas, vous pourriez toorun cycle d’une synchronisation entre hello planifiée cycles ou si vous devez toorun un autre type.

**Cycle de synchronisation delta**  
Un cycle de synchronisation delta inclut hello comme suit :

* Importation delta sur tous les connecteurs
* Synchronisation delta sur tous les connecteurs
* Exportation sur tous les connecteurs

Il peut s’agir d’avoir le des modifications qui doivent être synchronisées immédiatement, c’est pourquoi vous devez toomanually exécuter un cycle. Si vous avez besoin de toomanually exécuter un cycle, puis à partir de PowerShell exécuter `Start-ADSyncSyncCycle -PolicyType Delta`.

**Cycle de synchronisation complet**  
Si vous avez effectué une des hello suit les modifications de configuration, vous devez toorun un cycle de synchronisation complète (également appelée) Initial) :

* Ajouté plus toobe objets ou des attributs importée à partir d’un répertoire source
* Modifications de règles de synchronisation toohello
* Le [filtrage](active-directory-aadconnectsync-configure-filtering.md) étant modifié, un nombre différent d’objets doit être inclus

Si vous avez effectué une de ces modifications, vous devez toorun une synchronisation complète cycle de moteur de synchronisation hello a des espaces du connecteur hello opportunité tooreconsolidate hello. Un cycle de synchronisation complète inclut hello comme suit :

* Importation complète sur tous les connecteurs
* Synchronisation complète sur tous les connecteurs
* Exportation sur tous les connecteurs

tooinitiate un cycle de synchronisation complète, exécutez `Start-ADSyncSyncCycle -PolicyType Initial` à partir d’une invite de PowerShell. Cette commande démarre un cycle de synchronisation complet.

## <a name="stop-hello-scheduler"></a>Arrêter le Planificateur de hello
Si le planificateur hello est en cours d’exécution un cycle de synchronisation, vous devrez peut-être toostop il. Par exemple, si vous démarrez l’Assistant installation hello et que vous obtenez cette erreur :

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

Lorsqu’un cycle de synchronisation est en cours d’exécution, vous ne pouvez pas modifier la configuration. Vous pourriez attendre jusqu'à ce que le planificateur hello a terminé le processus de hello, mais vous pouvez également arrêter afin de vérifier vos modifications immédiatement. L’arrêt hello cycle actuel n’est pas dangereux et modifications en attente sont traitées de la prochaine exécution.

1. Commencez par indiquer hello planificateur toostop actuel cycle avec l’applet de commande PowerShell hello `Stop-ADSyncSyncCycle`.
2. Si vous utilisez une build avant 1.1.281, hello actuel ne s’arrête pas l’arrêt du Planificateur de hello connecteur à partir de sa tâche en cours. tooforce hello connecteur toostop, prendre hello suivant actions : ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Démarrer **Service de synchronisation** à partir du menu Démarrer de hello. Accédez trop**connecteurs**, mettez en surbrillance hello connecteur avec l’état de hello **en cours d’exécution**, puis sélectionnez **arrêter** de hello Actions.

Hello est toujours actif et commence à nouveau sur la prochaine occasion.

## <a name="custom-scheduler"></a>Planificateur personnalisé
Hello applets de commande décrites dans cette section sont uniquement disponibles dans la build [1.1.130.0](active-directory-aadconnect-version-history.md#111300) et versions ultérieures.

Si le Planificateur intégré hello ne satisfait pas vos besoins, vous pouvez planifier les connecteurs hello à l’aide de PowerShell.

### <a name="invoke-adsyncrunprofile"></a>Invoke-ADSyncRunProfile
Vous pouvez démarrer un profil pour un connecteur de cette façon :

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

toouse de noms Hello pour [noms de connecteur](active-directory-aadconnectsync-service-manager-ui-connectors.md) et [exécuter les noms de profil](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) se trouvent dans hello [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md).

![Appeler le profil d’exécution](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

Hello `Invoke-ADSyncRunProfile` applet de commande est synchrone, autrement dit, elle ne retourne pas contrôle jusqu'à ce que hello connecteur a terminé l’opération de hello, correctement ou avec une erreur.

Lorsque vous planifiez vos connecteurs, recommandation de hello est tooschedule dans hello suivant l’ordre :

1. (Intégral/Delta) Importation à partir de répertoires locaux, tels qu'Active Directory
2. (Intégral/Delta) Importation à partir d'Azure AD
3. (Intégral/Delta) Synchronisation à partir de répertoires locaux, tels qu'Active Directory
4. (Intégral/Delta) Synchronisation à partir d'Azure AD
5. Exportation tooAzure AD
6. Exporter tooon les annuaires locaux, tels qu’Active Directory

Cet ordre est le mode d’exécution de planificateur intégré de hello hello connecteurs.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
Vous pouvez également surveiller toosee de moteur de synchronisation hello s’il est occupé ou inactif. Cette applet de commande renvoie un résultat vide si le moteur de synchronisation hello est inactif et qu’il ne fonctionne pas un connecteur. Si un connecteur est en cours d’exécution, elle retourne le nom hello Hello connecteur.

```
Get-ADSyncConnectorRunStatus
```

![État d’exécution du connecteur](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
Hello image ci-dessus, la première ligne de hello provient d’un état dans lequel le moteur de synchronisation hello est inactif. Hello deuxième ligne lorsque hello connecteur Azure AD est en cours d’exécution.

## <a name="scheduler-and-installation-wizard"></a>Planificateur et Assistant d’installation
Si vous démarrez l’Assistant installation Bonjour, puis le planificateur hello est temporairement interrompu. Ce comportement est, car il est supposé vous apportez des modifications de configuration et de ces paramètres ne peut pas être appliqués si le moteur de synchronisation hello est activement en cours d’exécution. Pour cette raison, ne laissez pas l’Assistant installation hello ouvert, car il s’arrête le moteur de synchronisation hello d’effectuer toutes les actions de synchronisation.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
