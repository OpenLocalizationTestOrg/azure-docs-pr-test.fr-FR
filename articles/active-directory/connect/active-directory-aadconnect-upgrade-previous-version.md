---
title: "Azure AD Connect : effectuer une mise à niveau depuis une version précédente | Microsoft Docs"
description: "Explique hello différentes méthodes tooupgrade toohello version la plus récente d’Azure Active Directory Connect, y compris une mise à niveau sur place et une migration de basculement."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>Azure AD Connect : Mise à niveau à partir d’une précédente toohello de version plus récente
Cette rubrique décrit hello différentes méthodes que vous pouvez utiliser tooupgrade votre version la plus récente toohello installation Connect de Azure Active Directory (Azure AD). Nous vous recommandons de conserver vous-même actuel avec les versions hello d’Azure AD Connect. Vous également utilisez les étapes de hello Bonjour [OSCILLANT migration](#swing-migration) section lorsque vous modifiez une configuration substantielle.

Si vous souhaitez tooupgrade de DirSync, consultez [mise à niveau à partir de l’outil de synchronisation AD Azure (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md) à la place.

Il existe quelques stratégies différentes que vous pouvez utiliser tooupgrade Azure AD Connect.

| Méthode | Description |
| --- | --- |
| [Mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) |Il s’agit de méthode la plus simple hello pour les clients avec une installation rapide. |
| [Mise à niveau sur place](#in-place-upgrade) |Si vous avez un seul serveur, vous pouvez mettre à niveau hello installation in situ hello le même serveur. |
| [Migration « swing »](#swing-migration) |Avec deux serveurs, vous pouvez préparer un des serveurs hello avec la nouvelle version de hello ou la configuration et modifier le serveur active hello lorsque vous êtes prêt. |

Pour plus d’informations d’autorisations, consultez hello [autorisations requises pour une mise à niveau](active-directory-aadconnect-accounts-permissions.md#upgrade).

> [!NOTE]
> Une fois que vous avez activé votre nouvelle Azure AD Connect server toostart synchronisation modifications tooAzure AD, vous devez restaure pas toousing DirSync ou Azure AD Sync. La rétrogradation à partir d’Azure AD Connect toolegacy clients, y compris le nom de DirSync et Azure AD Sync, n’est pas pris en charge et peut entraîner des tooissues telles qu’une perte de données dans Azure AD.

## <a name="in-place-upgrade"></a>Mise à niveau sur place
Une mise à niveau sur place fonctionne à partir d’Azure AD Sync ou d’Azure AD Connect, Elle ne fonctionne pas pour la migration à partir de DirSync ou pour une solution avec Forefront Identity Manager (FIM) + connecteur Azure AD.

Nous vous recommandons cette méthode si vous avez un seul serveur et moins de 100 000 objets environ. S’il existe des modifications de règles de synchronisation d’out-of-box toohello, une importation intégrale et une synchronisation complète se produisent après la mise à niveau hello. Cette méthode garantit que la configuration du nouveau hello tooall appliqué des objets existants dans le système de hello. Cette exécution peut prendre quelques heures, en fonction du nombre de hello d’objets qui sont dans la portée du moteur de synchronisation hello. Planificateur de synchronisation delta normal Hello (qui synchronise toutes les 30 minutes par défaut) est suspendu, mais continue de la synchronisation de mot de passe. Vous pouvez envisager la mise à niveau in situ de hello pendant le week-end. S’il n’y a aucune configuration d’out-of-box toohello modifications avec mise en production de hello nouveau Azure AD Connect, puis un delta normal importation/synchronisation démarre à la place.  
![Mise à niveau sur place](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

Si vous avez apporté des modifications des règles de synchronisation d’out-of-box toohello, puis ces règles sont définies dans configuration par défaut de toohello sur la mise à niveau. toomake sûr que votre configuration est conservée entre les mises à niveau, assurez-vous que vous apportez des modifications qu’ils sont décrits dans [meilleures pratiques pour la modification de configuration par défaut de hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md).

Au cours de la mise à niveau, il peut y avoir des modifications introduites nécessitant toobe (y compris les étapes d’importation complète et synchronisation complète) des activités de synchronisation spécifique exécuté après la mise à niveau terminée. toodefer ces activités, consultez toosection [comment la synchronisation après mise à niveau de complète toodefer](#how-to-defer-full-synchronization-after-upgrade).

## <a name="swing-migration"></a>Migration « swing »
Si vous avez un déploiement complexe ou nombreux objets, il peut être peu pratique toodo une mise à niveau sur place sur le système hello. Pour certains clients, ce processus peut prendre plusieurs jours pendant lesquels aucune modification différentielle n’est traitée. Vous pouvez également utiliser cette méthode lorsque vous envisagez de configuration de tooyour toomake des modifications importantes et que vous souhaitez tootry les extraire avant qu’ils sont envoyées toohello cloud.

méthode recommandée de ces scénarios de Hello est toouse une migration de basculement. Vous devez avoir (au moins) deux serveurs : un serveur actif et un serveur intermédiaire. ASP Hello (indiquée avec des lignes bleues pleines Bonjour suivant image) est chargé de la charge de production actif hello. Hello (indiquée avec des lignes violets en pointillés) de serveur de test est préparée avec la nouvelle version de hello ou la configuration. Lorsqu’il est prêt, ce serveur devient actif. Hello précédent serveur actif, qui a une ancienne version de hello ou de configuration installée, est transformé en hello serveur intermédiaire et est mis à niveau maintenant.

deux serveurs de Hello peuvent utiliser différentes versions. Par exemple, que vous envisagez de toodecommission ASP hello permettre utiliser Azure AD Sync et nouveau serveur de mise en lots hello permettre utiliser Azure AD Connect. Si vous utilisez basculement migration toodevelop une nouvelle configuration, il une bonne idée toohave hello les mêmes versions sur hello deux serveurs.  
![Serveur de test](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> Certains clients préfèrent toohave trois ou quatre des serveurs pour ce scénario. Lorsque hello serveur intermédiaire est mis à niveau, vous n’avez pas un serveur de sauvegarde [la récupération d’urgence](active-directory-aadconnectsync-operations.md#disaster-recovery). Avec trois ou quatre serveurs, vous pouvez préparer un ensemble de serveurs principal/secondaire avec hello nouvelle version, ce qui garantit qu’il existe toujours un serveur intermédiaire est prêt tootake sur.

Ces étapes fonctionnent également toomove à partir d’Azure AD Sync ou d’une solution avec FIM + connecteur Azure AD. Ces étapes ne fonctionnent pas pour la synchronisation d’annuaire, mais hello même basculement migration (méthode) (également appelé déploiement parallèle) avec les étapes de synchronisation d’annuaire est en [synchronisation de mise à niveau Azure Active Directory (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md).

### <a name="use-a-swing-migration-tooupgrade"></a>Utilisez un tooupgrade de migration de basculement
1. Si vous utilisez Azure AD Connect sur les serveurs et assurez-vous de tooonly plan une modification de configuration, assurez-vous que votre serveur actif et le serveur de test sont à l’aide de hello même version. Qui rend plus facile toocompare différences ultérieurement. Si vous effectuez une mise à niveau à partir d’Azure AD Sync, ces serveurs auront des versions différentes. Si vous mettez à niveau à partir d’une version antérieure d’Azure AD Connect, il est un toostart recommandé avec les serveurs de hello deux qui sont à l’aide de hello même version, mais il n’est pas nécessaire.
2. Si vous avez apportées à une configuration personnalisée et il n’est utilisé pour votre serveur de test, suivez les étapes de hello sous [déplacer une configuration personnalisée à partir de toohello du serveur actif hello serveur intermédiaire](#move-custom-configuration-from-active-to-staging-server).
3. Si vous mettez à niveau à partir d’une version antérieure d’Azure AD Connect, mettez à niveau hello server toohello dernière version de la mise en lots. Si vous migrez à partir d’Azure AD Sync, installez Azure AD Connect sur votre serveur intermédiaire.
4. Permettent d’importation intégrale du moteur d’exécution de synchronisation hello et une synchronisation complète sur votre serveur de test.
5. Vérifiez que la configuration du nouveau hello n’a pas été entraîne des modifications inattendues à l’aide des étapes hello sous « Vérifier » dans [configuration hello de vérification d’un serveur](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server). Si un élément n’est pas comme prévu, correct, exécuter l’importation de hello et de synchronisation et vérifier les données de hello jusqu'à ce qu’il semble correct, en suivant les étapes de hello.
6. Basculez hello server toobe hello active serveur intermédiaire. Il s’agit étape finale de hello « Commutateur active server » dans [configuration hello de vérification d’un serveur](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server).
7. Si vous mettez à niveau Azure AD Connect, mettez à niveau le serveur hello est intermédiaire maintenant dans la version la plus récente en mode toohello. Suivez hello même procédure qu’avant tooget hello configuration des données et mis à niveau. Si vous avez effectué une mise à niveau à partir d’Azure AD Sync, vous pouvez maintenant désactiver et retirer votre ancien serveur.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>Déplacer une configuration personnalisée hello active toohello intermédiaire serveur
Si vous avez effectué le serveur de configuration modifications toohello active, vous devez toomake sûr qui hello même les modifications sont appliquée toohello serveur intermédiaire. toohelp avec ce déplacement, vous pouvez utiliser hello [documentation de configuration Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

Vous pouvez déplacer les règles de synchronisation hello que vous avez créé à l’aide de PowerShell. Vous devez appliquer d’autres hello modifications identique sur les deux systèmes et vous ne pouvez pas migrer les modifications hello. Hello [documentation de configuration](https://github.com/Microsoft/AADConnectConfigDocumenter) peut vous aider à comparer toomake de systèmes hello deux assurer qu’ils sont identiques. outil de Hello peut également aider à automatiser les étapes hello trouvés dans cette section.

Vous devez suivant de hello tooconfigure choses hello même manière sur les deux serveurs :

* Connexion toohello mêmes forêts
* Tout filtrage de domaine et d’unité organisationnelle
* Hello mêmes fonctionnalités facultatives, telles que la synchronisation de mot de passe et d’écriture différée de mot de passe

**Migrer les règles de synchronisation personnalisées**  
règles de synchronisation personnalisées toomove, hello suivant :

1. Ouvrez l’ **Éditeur de règles de synchronisation** sur votre serveur actif.
2. Sélectionnez une règle personnalisée. Cliquez sur **Exporter**. Une fenêtre Bloc-notes apparaît. Enregistrer le fichier temporaire de hello avec l’extension PS1. Le fichier devient un script PowerShell. Copiez toohello de fichier PS1 hello serveur intermédiaire.  
   ![Exportation des règles de synchronisation](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. Hello GUID de connecteur est différente sur hello serveur intermédiaire, et vous devez le modifier. tooget hello GUID, démarrer **Éditeur des règles de synchronisation**, sélectionnez une des règles d’out-of-box hello que hello représentent même connecté système, puis cliquez sur **exporter**. Remplacez hello GUID dans votre fichier PS1 hello GUID à partir de hello serveur intermédiaire.
4. Ouvrez une invite de PowerShell, exécutez le fichier de la hello PS1. Cela crée un règle de synchronisation personnalisée hello sur hello serveur intermédiaire.
5. Répétez cette procédure pour toutes vos règles personnalisées.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Comment toodefer complète synchronisation après mise à niveau
Au cours de la mise à niveau, il peut y avoir des modifications introduites nécessitant toobe (y compris les étapes d’importation complète et synchronisation complète) des activités de synchronisation spécifique exécutée. Par exemple, requièrent des modifications de schéma de connecteur **importation intégrale** nécessitent des modifications de règle de synchronisation étape et out-of-box **synchronisation complète** étape toobe exécutée sur les connecteurs affectés. Pendant la mise à niveau, Azure AD Connect détermine les activités de synchronisation requises et les enregistre en tant qu’*actions prioritaires*. Bonjour suivant le cycle de synchronisation, le Planificateur de synchronisation hello récupère ces remplacements et les exécute. Dès qu’une action prioritaire a été exécutée avec succès, elle est supprimée.

Il peut arriver dans lequel vous ne souhaitez pas ces tootake de remplacements sur place immédiatement après la mise à niveau. Par exemple, vous avez de nombreux objets synchronisés et vous souhaitez que ces toooccur d’étapes de synchronisation après les heures de bureau. tooremove ces remplacements :

1. Au cours de la mise à niveau, **Décochez** hello option **démarrer le processus de synchronisation hello lors de la fin de la configuration**. Cela désactive le Planificateur de synchronisation hello et empêche cycle de synchronisation ayant lieu automatiquement avant que les remplacements hello soient supprimés.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. Une fois la mise à niveau terminée, exécutez hello suivant toofind d’applet de commande out les remplacements ont été ajoutés :`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > remplacements de Hello sont spécifiques au connecteur. Bonjour exemple suivant, importation complète et synchronisation complètes ont été ajoutés tooboth hello le connecteur Active Directory sur site et le connecteur Azure AD.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Notez les remplacements hello existants qui ont été ajoutés.
   
4. tooremove hello les remplacements d’importation intégrale et une synchronisation complète sur un connecteur arbitraire, exécutez hello suivant l’applet de commande :`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   remplacements de hello tooremove sur tous les connecteurs, exécutez hello PowerShell script suivant :

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. Planificateur de hello tooresume, exécutez hello suivant l’applet de commande :`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > N’oubliez pas d’étapes de synchronisation tooexecute hello requis aussitôt. Vous pouvez manuellement exécuter ces étapes à l’aide de hello Synchronization Service Manager ou ajouter des substitutions hello à l’aide d’applet de commande Set-ADSyncSchedulerConnectorOverride hello.

tooadd hello les remplacements d’importation intégrale et une synchronisation complète sur un connecteur arbitraire, exécutez hello suivant l’applet de commande :`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [l’intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
