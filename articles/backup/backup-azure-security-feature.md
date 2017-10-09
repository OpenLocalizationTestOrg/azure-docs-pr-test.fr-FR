---
title: "protéger les sauvegardes hybride qui utilisent Azure Backup aaaSecurity fonctionnalités toohelp | Documents Microsoft"
description: "Découvrez comment les fonctionnalités de sécurité de toouse dans les sauvegardes de toomake Azure Backup plus sécurisées"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>Toohelp des fonctionnalités de sécurité la protection des sauvegardes de hybride qui utilisent Azure Backup
Les préoccupations en matière de risques de sécurité, comme les logiciels malveillants, le ransomware et les intrusions, sont de plus en plus nombreuses. Ces problèmes de sécurité peuvent coûter cher, à la fois en termes d’argent et de données. tooguard contre ces attaques, Azure Backup maintenant offre une sécurité toohelp de fonctionnalités protection des sauvegardes de hybride. Cet article décrit comment tooenable et utilisez ces fonctionnalités, à l’aide d’un agent Azure Recovery Services et le serveur de sauvegarde Azure. Voici quelques fonctionnalités :

- **Prévention**. Une couche supplémentaire d’authentification est ajoutée à chaque fois qu’une opération critique (par exemple, Modifier la phrase secrète) est effectuée. Cette validation est tooensure ces opérations peuvent être effectuées uniquement par les utilisateurs qui ont des informations d’identification Azure valides.
- **Alertes**. Une notification par courrier électronique est envoyée à toohello abonnement administrateur chaque fois qu’une opération critique, tels que la suppression des données de sauvegarde est effectuée. Cette adresse de messagerie garantit que l’utilisateur hello est informé rapidement ces actions.
- **Récupération**. Supprimé les données de sauvegarde sont conservées pendant 14 jours à partir de la date de hello de suppression de hello. Cela garantit récupérabilité des données de hello pendant une période donnée, par conséquent, il est sans perte de données même si une attaque se produit. En outre, un plus grand nombre de points de récupération minimale est conservé tooguard par rapport à des données endommagées.

> [!NOTE]
> Les fonctionnalités de sécurité ne doivent pas être activées si vous utilisez une sauvegarde de machine virtuelle IaaS (Infrastructure en tant que service). Ces fonctionnalités ne sont pas encore disponibles pour la sauvegarde de machine virtuelle IaaS, donc leur activation n’aura aucun impact. Vous ne devez activer les fonctionnalités de sécurité que si vous utilisez : <br/>
>  * **Agent Azure Backup**. Version minimale de l’agent 2.0.9052. Après avoir activé ces fonctionnalités, vous devez mettre à niveau des opérations critiques toothis agent version tooperform. <br/>
>  * **Serveur de sauvegarde Azure**. Version minimale de l’agent Azure Backup 2.0.9052 avec la mise à jour 1 du serveur de sauvegarde Azure. <br/>
>  * **System Center Data Protection Manager**. Version minimale de l’agent Azure Backup version 2.0.9052 avec Data Protection Manager 2012 R2 UR12 ou Data Protection Manager 2016 UR2. <br/> 


> [!NOTE]
> Ces fonctionnalités ne sont disponibles que pour le coffre Recovery Services. Tous les hello nouvellement créé les coffres des Services de récupération ces fonctionnalités sont activées par défaut. Pour les archivages de Recovery Services existants, les utilisateurs activer ces fonctionnalités à l’aide des étapes hello mentionnés dans hello suivant la section. Après avoir hello fonctionnalités sont activées, elles s’appliquent ordinateurs d’agents tooall hello Recovery Services, les instances de serveur de sauvegarde Azure et les serveurs Data Protection Manager inscrits avec le coffre de hello. L’activation de ce paramètre ne s’effectue qu’une seule fois et il est impossible de désactiver ces fonctionnalités après leur activation.
>

## <a name="enable-security-features"></a>Activer les fonctionnalités de sécurité
Si vous créez un coffre Recovery Services, vous pouvez utiliser toutes les fonctionnalités de sécurité hello. Si vous utilisez un coffre existant, activez les fonctionnalités de sécurité en procédant comme suit :

1. Se connecter toohello portail Azure à l’aide de vos informations d’identification Azure.
2. Sélectionnez **Parcourir**, puis entrez **Recovery Services**.

    ![Capture d’écran de l’option Parcourir du portail Azure](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    liste de Hello des coffres des services de récupération s’affiche. Dans cette liste, sélectionnez un coffre. tableau de bord Hello coffre-fort sélectionné s’ouvre.
3. À partir de la liste hello des éléments qui s’affiche sous le coffre de hello, sous **paramètres**, cliquez sur **propriétés**.

    ![Capture d’écran des options de coffre Recovery Services](./media/backup-azure-security-feature/vault-list-properties.png)
4. Sous **Paramètres de sécurité**, cliquez sur **Mettre à jour**.

    ![Capture d’écran des propriétés de coffre Recovery Services](./media/backup-azure-security-feature/security-settings-update.png)

    lien de la mise à jour Hello ouvre hello **paramètres de sécurité** panneau, qui fournit un résumé des fonctionnalités de hello et vous permet d’activer les.
5. À partir de la liste déroulante de hello **vous avez configuré l’authentification multifacteur Azure ?**, sélectionnez une valeur tooconfirm si vous avez activé [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md). S’il est activé, vous êtes invité à tooauthenticate à partir d’un autre périphérique (par exemple, un téléphone mobile) lors de la signature dans toohello portail Azure.

   Lorsque vous effectuez des opérations critiques dans la sauvegarde, vous avez tooenter un code confidentiel, disponible sur hello portail Azure de sécurité. L’activation de la fonctionnalité Azure Multi-Factor Authentication offre une couche de sécurité supplémentaire. Uniquement les informations d’identification Azure valides aux utilisateurs autorisés et authentifiés à partir d’un deuxième appareil, vous pouvez accéder à hello portail Azure.
6. paramètres de sécurité toosave, sélectionnez **activer** et cliquez sur **enregistrer**. Vous pouvez sélectionner **activer** uniquement une fois que vous sélectionnez une valeur à partir de hello **vous avez configuré l’authentification multifacteur Azure ?** liste à l’étape précédente de hello.

    ![Capture d’écran des paramètres de sécurité](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>Récupérer les données de sauvegarde supprimées
Sauvegarde conserve les données de sauvegarde supprimées pendant 14 jours supplémentaires et ne la supprime pas immédiatement si hello **arrêter la sauvegarde à supprimer les données de sauvegarde** opération est effectuée. toorestore ces données dans le délai de 14 jours hello, prenez hello comme suit, selon ce que vous utilisez :

Pour les utilisateurs de l’**agent Azure Recovery Services** :

1. Si l’ordinateur hello où les sauvegardes ont été passe est toujours disponible, utilisez [récupérer des données toohello même machine](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) dans Azure Recovery Services toorecover à partir de tous les points de récupération ancien hello.
2. Si cet ordinateur n’est pas disponible, utilisez [récupérer tooan autre machine](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) toouse un autre tooget d’ordinateur des Services de récupération Azure ces données.

Pour les utilisateurs **Serveur de sauvegarde Azure** :

1. Si le serveur hello où les sauvegardes ont été passe est toujours disponible, protégez à nouveau les sources de données hello supprimé et utiliser hello **récupérer les données** fonctionnalité toorecover de tous les points de récupération ancien hello.
2. Si ce serveur n’est pas disponible, utilisez [récupérer des données à partir d’un autre serveur de sauvegarde Azure](backup-azure-alternate-dpm-server.md) toouse un autre serveur de sauvegarde Azure instance tooget ces données.

Pour les utilisateurs de **Data Protection Manager** :

1. Si le serveur hello où les sauvegardes ont été passe est toujours disponible, protégez à nouveau les sources de données hello supprimé et utiliser hello **récupérer les données** fonctionnalité toorecover de tous les points de récupération ancien hello.
2. Si ce serveur n’est pas disponible, utilisez [ajouter un DPM externe](backup-azure-alternate-dpm-server.md) toouse un autre tooget de serveur Data Protection Manager ces données.

## <a name="prevent-attacks"></a>Empêcher les attaques
Vérifications ont été ajoutées toomake que seuls les utilisateurs autorisés peuvent effectuer diverses opérations. Ces vérifications incluent l’ajout d’une couche d’authentification et la conservation d’une durée de rétention minimale pour la récupération.

### <a name="authentication-tooperform-critical-operations"></a>Opérations critiques d’authentification tooperform
Dans le cadre de l’ajout d’une couche supplémentaire d’authentification pour les opérations critiques, vous êtes invité à tooenter un code PIN de sécurité lorsque vous effectuez **arrêter la Protection avec suppression des données** et **modifier le mot de passe** opérations .

tooreceive ce code PIN :

1. Se connecter toohello portail Azure.
2. Parcourir trop**de coffre Recovery Services** > **paramètres** > **propriétés**.
3. Sous **Code PIN de sécurité**, cliquez sur **Générer**. Cette opération ouvre un panneau qui contient hello toobe de code confidentiel entré dans l’interface utilisateur de hello Azure Recovery Services agent.
    Ce code PIN n’est valide que pendant cinq minutes, après quoi il est généré automatiquement.

### <a name="maintain-a-minimum-retention-range"></a>Maintenir la durée de rétention minimale
tooensure il y a toujours un nombre valide de la récupération des points disponibles, hello contrôles ont été ajouté :

- Pour une rétention quotidienne, une rétention de **sept** jours minimum doit être appliquée.
- Pour une rétention hebdomadaire, une rétention de **quatre** semaines minimum doit être appliquée.
- Pour une rétention mensuelle, une rétention de **trois** mois minimum doit être appliquée.
- Pour une rétention annuelle, une rétention d’**un** an minimum doit être appliquée.

## <a name="notifications-for-critical-operations"></a>Notifications pour les opérations critiques
En règle générale, lors de l’exécution d’une opération critique, administrateur des abonnements hello est envoyé une notification par courrier électronique avec des détails sur l’opération de hello. Vous pouvez configurer les destinataires de courrier électronique supplémentaires pour ces notifications à l’aide de hello portail Azure.

les fonctionnalités de sécurité Hello citées dans cet article fournissent des mécanismes de défense contre les attaques ciblées. Plus important encore, si une attaque se produit, ces fonctions vous offrent hello toorecover de capacité de vos données.

## <a name="troubleshooting-errors"></a>Résolution des erreurs
| Opération | Détails de l’erreur | Résolution : |
| --- | --- | --- |
| Modification de la stratégie |stratégie de sauvegarde Hello n’a pas pu être modifié. Erreur : Échec de l’opération hello en raison de l’erreur de service interne tooan [0x29834]. Recommencez l’opération hello plus tard. Si hello problème persiste, contactez le support technique de Microsoft. |**Cause :**<br/>Cette erreur se produit lorsque les paramètres de sécurité sont activés, vous essayez de rétention tooreduce ci-dessous les valeurs minimales hello spécifiées ci-dessus et vous êtes sur une version non prise en charge (les versions prises en charge sont spécifiées dans la première note de cet article). <br/>**Action recommandée :**<br/> Dans ce cas, vous devez définir la période de rétention ci-dessus hello rétention minimale période spécifiée (sept jours pour tous les jours, des quatre dernières semaines pour toutes les semaines, trois semaines pour tous les mois ou une année pour annuelle) tooproceed avec la stratégie liés mises à jour. Si vous le souhaitez, meilleure approche serait tooupdate l’agent de sauvegarde, Azure Backup Server et/ou DPM UR tooleverage tous les hello mises à jour. |
| Modification de la phrase secrète |Le code PIN de sécurité entré est incorrect. (ID : 100130) Fournissez toocomplete de code PIN de sécurité correct hello cette opération. |**Cause :**<br/> Cette erreur se produit lorsque vous entrez un code PIN de sécurité non valide ou qui a expiré lors d’une opération critique (par exemple, la modification de la phrase secrète). <br/>**Action recommandée :**<br/> opération de hello toocomplete, vous devez entrer le code PIN de sécurité valide. tooget hello PIN, connectez-vous au portail de tooAzure et accédez de coffre de Services tooRecovery > Paramètres > Propriétés > Générer un PIN de sécurité. Utilisez cette phrase secrète toochange de code confidentiel. |
| Modification de la phrase secrète |L’opération a échoué. ID : 120002 |**Cause :**<br/>Cette erreur se produit lorsque les paramètres de sécurité sont activés, vous essayez de toochange le mot de passe et vous êtes sur la version non prise en charge (versions valides spécifiées dans la première note de cet article).<br/>**Action recommandée :**<br/> phrase secrète toochange, vous devez tout d’abord mettre à jour version toominimum de l’agent de sauvegarde 2.0.9052 minimal, Azure Backup server toominimum update 1, et/ou DPM toominimum UR12 de DPM 2012 R2 ou DPM 2016 UR2 (liens de téléchargement ci-dessous), puis entrez le code PIN de sécurité valide. tooget hello PIN, connectez-vous au portail de tooAzure et accédez de coffre de Services tooRecovery > Paramètres > Propriétés > Générer un PIN de sécurité. Utilisez cette phrase secrète toochange de code confidentiel. |

## <a name="next-steps"></a>Étapes suivantes
* [Prise en main Azure Recovery Services coffre](backup-azure-vms-first-look-arm.md) tooenable ces fonctionnalités.
* [Télécharger l’agent Azure Recovery Services plus récent hello](http://aka.ms/azurebackup_agent) toohelp protéger des ordinateurs Windows et protéger vos données contre les attaques de sauvegarde.
* [Téléchargement hello dernière Azure Backup Server](https://aka.ms/latest_azurebackupserver) toohelp protéger les charges de travail et de protéger vos données contre les attaques de sauvegarde.
* [Télécharger UR12 pour System Center 2012 R2 Data Protection Manager](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) ou [télécharger UR2 pour System Center 2016 Data Protection Manager](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp protéger les charges de travail et de protéger vos données contre les attaques de sauvegarde.
