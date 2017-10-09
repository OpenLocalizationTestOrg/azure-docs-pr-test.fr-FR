---
title: "Azure AD Connect : Comment limiter toorecover à partir de la base de données locale 10 Go problème | Documents Microsoft"
description: "Cette rubrique décrit comment toorecover synchronisation d’Azure AD Connect de Service lorsqu’il rencontre LocalDB 10 Go limiter le problème."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Azure AD Connect : Comment toorecover à partir de la limite de 10 Go de base de données locale
Azure AD Connect requiert une données d’identité de base de données SQL Server toostore. Vous pouvez utiliser SQL Server 2012 Express LocalDB installé avec Azure AD Connect de la valeur par défaut hello ou utiliser votre propre SQL complète. SQL Server Express impose une limite de taille de 10 Go. Lorsque vous utilisez la base de données locale et que cette limite est atteinte, le service de synchronisation Azure AD Connect ne peut plus démarrer ou se synchroniser correctement. Cet article fournit des étapes de récupération hello.

## <a name="symptoms"></a>Symptômes
Il existe deux symptômes courants :

* Service Azure AD Connect synchronisation **est en cours d’exécution** , mais échoue toosynchronize avec *« s’est arrêté-base de données-disque plein »* erreur.

* Service Azure AD Connect synchronisation **est impossible de toostart**. Lorsque vous essayez de service de hello toostart, elle échoue avec l’événement 6323 et le message d’erreur *« hello serveur a rencontré une erreur, car SQL Server est en dehors de l’espace disque. »*

## <a name="short-term-recovery-steps"></a>Étapes de récupération à court terme
Cette section fournit un espace de tooreclaim DB hello étapes requise pour l’opération de Service Azure AD Connect synchronisation tooresume. Hello étapes :
1. [Déterminer l’état du Service de synchronisation hello](#determine-the-synchronization-service-status)
2. [Réduire la base de données hello](#shrink-the-database)
3. [Supprimer les données d’historique d’exécution](#delete-run-history-data)
4. [Réduire la période de rétention des données d’historique d’exécution](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Déterminer l’état du Service de synchronisation hello
Tout d’abord, déterminez si hello Service de synchronisation est en cours d’exécution ou non :

1. Ouvrez une session dans tooyour Azure AD Connect serveur en tant qu’administrateur.

2. Accédez trop**Service Control Manager**.

3. Vérifier l’état de hello de **Microsoft Azure AD Sync**.


4. Si elle est en cours d’exécution, arrêter ou redémarrer le service de hello. Ignorer [base de données réduction hello](#shrink-the-database) étape et passez trop[supprimer exécuter les données d’historique](#delete-run-history-data) étape.

5. Si elle n’est pas en cours d’exécution, essayez de service de hello toostart. Si hello service démarre correctement, passez [base de données réduction hello](#shrink-the-database) étape et passez trop[supprimer exécuter les données d’historique](#delete-run-history-data) étape. Sinon, continuez [base de données réduction hello](#shrink-the-database) étape.

### <a name="shrink-hello-database"></a>Réduire la base de données hello
Utilisez toofree d’opération de réduction hello des suffisamment hello de toostart DB espace Service de synchronisation. Elle libère de l’espace de base de données en supprimant les espaces blancs dans la base de données hello. Il s’agit de l’étape recommandée, mais elle ne constitue pas la garantie que vous pouvez toujours récupérer de l’espace. toolearn en savoir plus sur l’opération de réduction, lisez cet article [réduire une base de données](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Ignorez cette étape si vous pouvez obtenir toorun du Service de synchronisation hello. Il est déconseillé tooshrink hello base de données SQL car elle peut entraîner des performances toopoor en raison de la fragmentation de tooincreased.

le nom de base de données hello créé pour Azure AD Connect Hello est **ADSync**. tooperform une opération de réduction, vous devez vous connecter en tant que hello sysadmin ou le propriétaire de la base de données hello. Pendant l’installation d’Azure AD Connect, hello suivant comptes bénéficient de droits d’administrateur système :
* Administrateurs locaux
* compte d’utilisateur Hello qui était utilisé toorun Azure AD Connect installation.
* Hello compte de Service de synchronisation qui est utilisé comme hello fonctionne le contexte de Service Azure AD Connect synchronisation.
* groupe local Hello ADSyncAdmins qui a été créé pendant l’installation.

1. Base de données de hello en copiant **ADSync.mdf** et **ADSync_log.ldf** fichiers situés sous `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa les emplacement sûr.

2. Démarrez une nouvelle session PowerShell.

3. Accédez toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Démarrer **sqlcmd** utilitaire en exécutant la commande hello `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, à l’aide des informations d’identification de hello d’un administrateur système ou hello DBO de la base de données.

5. base de données du hello tooshrink, à l’invite de sqlcmd hello (1 >), entrez `DBCC Shrinkdatabase(ADSync,1);`, suivi par `GO` dans la ligne suivante de hello.

6. Si l’opération de hello est réussie, réessayez toostart hello Service de synchronisation. Si vous pouvez démarrer le Service de synchronisation de hello, accédez trop[supprimer exécuter les données d’historique](#delete-run-history-data) étape. Sinon, contactez le support.

### <a name="delete-run-history-data"></a>Supprimer les données d’historique d’exécution
Par défaut, Azure AD Connect conserve des tooseven jours de données de l’historique d’exécution. Dans cette étape, nous supprimons hello espace de tooreclaim base de données de l’historique des données d’exécution afin que le Service Azure AD Connect synchronisation peut démarrer la synchronisation.

1.  Démarrer **Synchronization Service Manager** par → de tooSTART va Service de synchronisation.

2.  Accédez toohello **Operations** onglet.

3.  Sous **Actions**, sélectionnez **Clear Runs... (Effacer les exécutions)**.

4.  Vous pouvez choisir l’option **Clear all runs (Effacer toutes les exécutions)** ou **Clear runs before… (Effacer les exécutions avant)<date>**. Il est recommandé de commencer par désactiver les données d’historique d’exécution présentes depuis plus de deux jours. Si vous continuez toorun problème de taille de base de données, puis choisissez hello **effacer toutes les séries** option.

### <a name="shorten-retention-period-for-run-history-data"></a>Réduire la période de rétention des données d’historique d’exécution
Cette étape est la probabilité de hello tooreduce des problème de limite de 10 Go hello après plusieurs cycles de synchronisation.

1. Ouvrez une nouvelle session PowerShell.

2. Exécutez `Get-ADSyncScheduler` et prenez note de hello propriété PurgeRunHistoryInterval, qui spécifie la période de rétention actuelle hello.

3. Exécutez `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` jours tootwo période de conservation des tooset hello. Ajuster la période de rétention hello comme il convient.

## <a name="long-term-solution--migrate-toofull-sql"></a>Solution à long terme – migration toofull SQL
En règle générale, problème de hello n’indique que la taille de base de données de 10 Go n’est plus suffisante pour Azure AD Connect toosynchronize votre tooAzure d’Active Directory sur site Active Directory. Il est conseillé de passer toousing hello complète de SQL server. Vous ne peut pas remplacer directement hello LocalDB d’un déploiement d’Azure AD Connect existant avec base de données hello de la version complète de hello de SQL. Au lieu de cela, vous devez déployer un nouveau serveur Azure AD Connect avec la version complète de hello de SQL. Il est recommandé d’effectuer une migration de basculement où le nouveau serveur de Azure AD Connect hello (avec la base de données SQL) est déployé comme un serveur de test suivant toohello existant Azure AD Connect serveur (avec LocalDB). 
* Pour obtenir des instructions sur comment tooconfigure SQL à distance avec Azure AD Connect, consultez tooarticle [installation personnalisée d’Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Pour obtenir des instructions sur la migration de basculement pour la mise à niveau Azure AD Connect, consultez tooarticle [Azure AD Connect : mise à niveau à partir d’une précédente toohello de version plus récente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
