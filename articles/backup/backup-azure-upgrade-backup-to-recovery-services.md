---
title: "aaaUpgrade un coffre de Services de récupération sauvegarde coffre tooa (version préliminaire) | Documents Microsoft"
description: Instructions et tooupgrade des informations de prise en charge de la sauvegarde Azure coffre tooa de coffre Recovery Services.
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>Mise à niveau d’un coffre de sauvegarde coffre tooa Services de récupération

Cet article explique comment tooupgrade un coffre de sauvegarde des Services de récupération tooa coffre. mise à niveau de Hello n’affecte pas les tâches de sauvegarde en cours d’exécution et les données de sauvegarde ne sont perdues. Hello principal raisons pour tooupgrade un tooa de coffre de sauvegarde de coffre de Services de récupération :
- Toutes les fonctionnalités d’un coffre de sauvegarde sont conservées dans un coffre Recovery Services.
- Les coffres Recovery Services offrent davantage de fonctionnalités que les coffres de sauvegarde, dont une meilleure sécurité, une surveillance intégrée, des restaurations plus rapides et des restaurations au niveau élément.
- Gérez les éléments de sauvegarde à partir d’un portail amélioré et simplifié.
- Nouvelles fonctionnalités s’appliquent uniquement à tooRecovery coffres des Services.

## <a name="impact-toooperations-during-upgrade"></a>Toooperations impact pendant la mise à niveau

Lors de la mise à niveau d’un coffre de sauvegarde coffre tooa Services de récupération, aucun impact n’est tooyour les opérations de plan de données. Tous les travaux de sauvegarde continuent à se dérouler normalement, et tous les travaux de restauration actifs se poursuivent sans interruption. Au cours de la mise à niveau de hello, les opérations de gestion entraînent une interruption de courte durée, et vous ne peut pas protéger de nouveaux éléments ou créer des travaux de sauvegarde ad hoc. Travaux de restauration pour les machines virtuelles IaaS ne s’exécutent pendant la mise à niveau hello. mise à niveau du coffre Hello prend moins d’une toocomplete d’heure. Une fois que vous avez terminé, un coffre Recovery Services remplace le coffre de sauvegarde hello.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>Outil après la mise à niveau et les modifications tooyour automation

Lors de la préparation de votre infrastructure de mise à niveau du coffre hello, vous devez mettre à jour votre automatisation existante ou tooensure des outils qu’elle continue toowork après la mise à niveau hello.
Consultez les références d’applets de commande PowerShell hello pour hello [modèle de déploiement de Service Manager](backup-client-automation-classic.md) et hello [modèle de déploiement de gestionnaire de ressources](backup-client-automation.md).


## <a name="before-you-upgrade"></a>Avant de mettre à niveau

Vérifiez les problèmes hello suivants avant la mise à niveau vos archivages de sauvegarde coffres de Service tooRecovery.

- **Version minimale de l’agent**: tooupgrade votre archivage, vérifiez que hello Microsoft Azure Recovery Services (MARS) agent est au moins la version 2.0.9070.0. Si l’agent de MARS hello est antérieure à 2.0.9070.0, mettre à jour l’agent de hello avant de démarrer le processus de mise à niveau hello.
- **Modèle de facturation basée sur l’instance**: Service de récupération coffres prennent uniquement en charge le modèle de facturation basé sur une Instance hello. Si vous avez un coffre de sauvegarde qui est à l’aide de hello plus anciens en fonction de stockage modèle de facturation, convertir en modèle de facturation hello pendant la mise à niveau.
- **Aucune opération de configuration de la sauvegarde en cours**: pendant la mise à niveau, le plan de gestion des accès toohello est limité. Effectuer toutes les actions de plan de gestion, puis démarrez la mise à niveau de hello.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>À l’aide de PowerShell scripts tooupgrade vos archivages

Vous pouvez utiliser PowerShell scripts tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde. Vérifiez que vous avez hello requis de mise à niveau de PowerShell composants tootrigger hello coffre. Les scripts PowerShell pour les coffres de sauvegarde ne fonctionnent pas pour les coffres Recovery Services. Préparer votre environnement de coffres de hello tooupgrade :

1. Installer ou mettre à niveau [tooversion de Windows Management Framework (WMF) 5](https://www.microsoft.com/download/details.aspx?id=50395) ou version ultérieure.
2. [Installez Azure PowerShell MSI](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi).
3. Télécharger hello [script PowerShell](https://aka.ms/vaultupgradescript2) tooupgrade vos archivages.

### <a name="run-hello-powershell-script"></a>Exécutez le script PowerShell de hello

Utilisez hello suivant script tooupgrade vos archivages. Hello suivant l’exemple de script a des explications des paramètres de hello.

RecoveryServicesVaultUpgrade-1.0.2.ps1 **-SubscriptionID** `<subscriptionID>` **-VaultName** `<vaultname>` **-Location** `<location>` **-ResourceType** `BackupVault` **-TargetResourceGroupName** `<rgname>`

**ID d’abonnement** -hello numéro ID d’abonnement de coffre hello qui est en cours de mise à niveau.<br/>
**Nom du coffre** hello - nom du coffre de sauvegarde hello qui est en cours de mise à niveau.<br/>
**Emplacement** -emplacement du coffre hello mis à niveau.<br/>
**ResourceType** : utilisez BackupVault.<br/>
**TargetResourceGroupName** - étant donné que vous mettez à niveau hello coffre tooa basée sur le Gestionnaire de ressources du déploiement, spécifiez un groupe de ressources. Vous pouvez utiliser un groupe de ressources existant ou en créez un en fournissant un nouveau nom. Si vous orthographiez mal le nom hello d’un groupe de ressources, vous pouvez créer un nouveau groupe de ressources. toolearn savoir plus sur les groupes de ressources, lire ce [vue d’ensemble des groupes de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups).

>[!NOTE]
> Les noms de groupes de ressources doivent respecter certaines contraintes. Être sûr de conseils de hello toofollow ; Échec toodo pourrait donc toofail de mises à niveau de coffre.
>
>

Hello extrait de code suivant est un exemple de votre commande PowerShell doit ressembler à :

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

Vous pouvez également exécuter le script hello sans aucun paramètre et que vous êtes invité tooprovide entrées pour tous les paramètres requis.

Hello script PowerShell vous invite à entrer vous tooenter vos informations d’identification. Entrez vos informations d’identification à deux reprises : une fois pour le compte de Service Manager hello et une deuxième fois pour hello compte de gestionnaire de ressources.

### <a name="pre-requisites-checking"></a>Vérification des conditions préalables
Une fois que vous avez entré vos informations d’identification Azure, Azure vérifie que votre environnement répond aux hello suivant des conditions préalables :

- **Version minimale de l’agent** -coffres des Services de sauvegarde de la mise à niveau coffres tooRecovery doit posséder au moins hello MARS agent toobe version 2.0.9070. Si vous avez éléments inscrits tooa le coffre de sauvegarde avec un agent antérieures à 2.0.9070, vérification hello échoue. Si la vérification des conditions préalables hello échoue, mettre à jour l’agent de hello et réessayez le coffre tooupgrade hello. Vous pouvez télécharger la version la plus récente de l’agent hello hello [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe).
- **Tâches de configuration en cours**: si une personne est configuration de travail pour un coffre de sauvegarde défini toobe mis à niveau ou l’inscription d’un élément, hello vérification échoue. Terminer la configuration de hello, ou terminer l’inscription d’élément de hello, puis démarrez le processus de mise à niveau de coffre hello.
- **Modèle de facturation basée sur le stockage**: Services de récupération coffres prise en charge hello basé sur une Instance modèle de facturation. Si vous exécutez une mise à niveau du coffre hello sur un coffre de sauvegarde, qu’utilise hello modèle de facturation basée sur le stockage, vous êtes invité à tooupgrade votre modèle de facturation ainsi que de hello coffre. Sinon, vous pouvez mettre à jour votre modèle de facturation tout d’abord, puis exécutez la mise à niveau du coffre hello.
- Identifier un groupe de ressources pour les Services de récupération hello coffre. avantage tootake de hello les fonctionnalités de déploiement de gestionnaire de ressources, vous devez placer un coffre Recovery Services dans un groupe de ressources. Si vous ne savez pas quel toouse groupe de ressources, fournir qu'un nom et un hello de mise à niveau crée hello groupe de ressources pour vous. processus de mise à niveau de Hello associe également le coffre hello avec hello nouveau groupe de ressources.

Une fois le processus de mise à niveau hello a terminé la vérification des conditions préalables hello, processus de hello invite vous toostart hello coffre mise à niveau. Après avoir confirmé, mise à niveau de hello prend généralement autour toocomplete 15 à 20 minutes, selon la taille de hello de votre archivage. Si vous avez un coffre de grande taille, la mise à niveau peut prendre jusqu'à too90 minutes.

## <a name="managing-your-recovery-services-vaults"></a>Accéder à vos coffres Recovery Services

Hello suivant écrans montrent un coffre Recovery Services, mise à niveau à partir du coffre de sauvegarde, hello portail Azure. premier écran de Hello affiche hello coffre tableau de bord affiche les entités clés pour le coffre hello.

![exemple de coffre Recovery Services mis à niveau à partir d’un coffre de sauvegarde](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

deuxième écran de Hello affiche des liens d’aide hello disponible toohelp comment commencer à utiliser les Services de récupération hello coffre.

![aide de liens dans le panneau de démarrage rapide de hello](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>Étapes post-mise à niveau
Les coffres Recovery Services prennent en charge la spécification d’informations de fuseau horaire dans la stratégie de sauvegarde. Une fois le coffre est mis à niveau, accédez tooBackup stratégies à partir du menu Paramètres de coffre et mettre à jour les informations de fuseau horaire hello pour chacune des stratégies de hello configurées dans le coffre de hello. Cet écran montre déjà les temps de planification de sauvegarde hello spécifié par le fuseau horaire local utilisé quand vous avez créé la stratégie. 

## <a name="enhanced-security"></a>Sécurité améliorée

Lorsqu’un coffre de sauvegarde est mise à niveau de coffre de Services de récupération tooa, hello les paramètres de sécurité pour ce coffre sont automatiquement activés. Lorsque les paramètres de sécurité hello sont on, certaines opérations telles que la suppression des sauvegardes, ou la modification d’un mot de passe nécessite une [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) code confidentiel. Pour plus d’informations sur la sécurité de hello amélioré, voir l’article hello [fonctionnalités de sécurité les sauvegardes hybride tooprotect](backup-azure-security-feature.md). 

Lorsque la sécurité de hello renforcée est activée, les données sont conservées too14 jours après que les informations de point de récupération hello a été supprimées du coffre de hello. Les clients sont facturés pour le stockage de ces données de sécurité. Rétention des données de sécurité s’applique à points toorecovery nécessaire pour l’agent de sauvegarde Azure hello, Azure Backup Server et System Center Data Protection Manager. 

## <a name="gather-data-on-your-vault"></a>Collecter des données sur votre coffre

Une fois que vous mettez à niveau le coffre Recovery Services tooa, configurer des rapports pour la sauvegarde Azure (pour les machines virtuelles IaaS et les Services de récupération Microsoft Azure (MARS)) et utiliser les rapports de hello tooaccess Power BI. Pour plus d’informations sur la collecte des données, consultez l’article hello, [configurer Azure Backup signale](backup-azure-configure-reports.md).

## <a name="frequently-asked-questions"></a>Forum Aux Questions

**Plan de mise à niveau hello affecte-t-il mon sauvegardes en cours ?**</br>
Non. Vos sauvegardes en cours se poursuivent sans interruption pendant et après la mise à niveau.

**Si vous ne prévoyez pas de mise à niveau dès, que passe-t-il toomy coffres ?**</br>
Étant donné que toutes les nouvelles fonctionnalités s’appliquent uniquement des coffres de Services tooRecovery, nous conseillons vivement vous tooupgrade vos archivages. Microsoft désapprouve finalement portail classique de hello. En commençant le 1er septembre 2017 Microsoft commence la mise à niveau automatique coffres des Services tooRecovery les coffres de sauvegarde. Par le 1er novembre 2017, Microsoft va terminer les processus de mise à niveau hello. Votre coffre peut être mis à niveau automatiquement à tout moment entre septembre ou octobre. Microsoft vous recommande de mettre à niveau votre coffre dès que possible.

**Quelles sont les implications de cette migration pour mes outils existants ?**</br>
Mettre à jour votre modèle de déploiement du Gestionnaire de ressources de toohello outils. Services de récupération des coffres ont été créés pour les utilisent dans le modèle de déploiement du Gestionnaire de ressources hello. Planification pour le modèle de déploiement du Gestionnaire de ressources hello et tenant compte de la différence de hello dans vos archivages sont important. 

**Au cours de la mise à niveau de hello, existe-t-il un temps d’interruption ?**</br>
Il dépend de nombre hello des ressources qui sont mis à niveau. Pour les déploiements plus petits (quelques dizaines d’instances protégés), toute mise à niveau de hello doit prendre moins de 20 minutes. Pour les déploiements plus importants, il ne devrait pas excéder une heure.

**Puis-je restaurer après la mise à niveau ?**</br>
Non. La restauration n’est pas prise en charge une fois que les ressources hello ont été mis à niveau avec succès.

**Puis-je valider mon toosee abonnement ou de ressources s’ils sont capables de mise à niveau ?**</br>
Oui. Hello première étape de mise à niveau valide que les ressources hello sont capables de mise à niveau. En cas d’échec de la validation de hello de conditions préalables, vous recevez des messages pour les motifs hello mise à niveau hello ne peut pas être effectuée.

**Quelles sont les autorisations dois-je disposer mise à niveau du coffre tootrigger ?**</br>
tooperform hello coffre mise à niveau, vous devez être ajouté en tant que coadministrateur pour l’abonnement hello Bonjour portail Azure classic. Cela est nécessaire même si vous êtes déjà répertorié en tant que propriétaire Bonjour portail Azure. Si vous êtes coadministrateur pour l’abonnement de hello, essayez tooadd un coadministrateur pour l’abonnement hello dans Azure toofind portail classique out. Si vous n’êtes pas en mesure de tooadd un coadministrateur, contactez un administrateur de service ou un coadministrateur pour l’abonnement hello, qui vous ajouter en tant que coadministrateur.

**Puis-je mettre à niveau mon coffre de sauvegarde basé sur un fournisseur de services de chiffrement ?**</br>
Non. Actuellement, vous ne pouvez pas mettre à niveau des coffres de sauvegarde basés sur un fournisseur de services de chiffrement. Nous allons ajouter la prise en charge de la mise à niveau des coffres de sauvegarde basée sur le fournisseur de services cryptographiques dans les versions hello suivantes.

**Puis-je afficher mon coffre Azure Classic après mise à niveau ?**</br>
Non. Vous ne pouvez pas afficher ou gérer votre coffre classique après mise à niveau. Vous ne serez en mesure de toouse hello nouveau portail Azure pour toutes les actions de gestion sur le coffre hello.

**Échec de ma mise à niveau, mais machine hello maintenu agent hello nécessitant une mise à jour, n’existe plus. Que faire dans ce cas ?**</br>
Si vous avez besoin de magasin de hello toouse, hello sauvegardes de cet ordinateur pour la rétention à long terme, vous ne serez pas tooupgrade en mesure du coffre hello. Dans les versions ultérieures, nous ajouterons la prise en charge de la mise à niveau d’un coffre de ce type.
Si vous n’avez pas besoin de sauvegardes de hello toostore de cet ordinateur plus, puis Veuillez annuler l’inscription de cet ordinateur à partir du coffre de hello et recommencez la mise à niveau hello.

**Pourquoi ne peux pas voir des informations sur les tâches hello pour mes ressources local après la mise à niveau**</br>
Surveillance des locaux sauvegardes (agent MARS, DPM et le serveur de sauvegarde Azure) est une nouvelle fonctionnalité que vous obtenez lorsque vous mettez à niveau votre coffre de sauvegarde coffre tooRecovery Services. Hello, informations d’analyse occupe toosync d’heures too12 avec le service de hello.

**Comment signaler un problème ?**</br>
Si une partie du coffre de hello de mise à niveau échoue, hello Remarque OperationId répertorié dans l’erreur de hello. Support technique de Microsoft fonctionnera proactive problème de hello tooresolve. Vous pouvez atteindre les tooSupport ou envoyez-nous un e-mail à rsvaultupgrade@service.microsoft.com avec votre ID d’abonnement, le nom de l’archivage et la OperationId. Nous tenterons d’effectuer aussi rapidement que possible problème de hello tooresolve. Ne pas réessayer les opération hello sauf explicitement instruction toodo c’est le cas par Microsoft.


## <a name="next-steps"></a>Étapes suivantes
Utilisez hello article au suivant :</br>
[Sauvegarder une machine virtuelle IaaS](backup-azure-arm-vms-prepare.md)</br>
[Sauvegarder un serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md)</br>
[Sauvegarder un serveur Windows Server](backup-configure-vault.md)
