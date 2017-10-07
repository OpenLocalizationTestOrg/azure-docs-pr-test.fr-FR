---
title: "les sauvegardes déployées par le Gestionnaire de ressources des machines virtuelles aaaMonitor | Documents Microsoft"
description: "Suivre les événements et les alertes des sauvegardes d’une machine virtuelle déployée via Resource Manager. Envoyer un e-mail en fonction des alertes."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a>Suivez les alertes des sauvegardes de machines virtuelles Azure
Les alertes sont des réponses du service hello qu’un seuil d’événement a été atteint ou dépassé. Si vous savez lorsque des problèmes de début peuvent être tookeeping critiques des frais de gestion vers le bas. Les alertes ne se produisent généralement pas selon une planification, et il est donc utile tooknow dès que possible après que des alertes se produisent. Par exemple, lorsqu’une tâche de sauvegarde ou de restauration échoue, une alerte se produit dans les cinq minutes de défaillance de hello. Dans le tableau de bord du coffre hello, hello vignette alertes de sauvegarde affiche les événements critiques et de niveau d’avertissement. Dans les paramètres des alertes de sauvegarde hello, vous pouvez afficher tous les événements. Mais que faire si une alerte se produit lorsque vous travaillez sur un autre problème ? Si vous ne connaissez pas lors de l’alerte de hello se produit, elle peut être un inconvénient secondaire, ou il pourrait compromettre les données. Lorsqu’il se produit, toomake que hello personnes autorisées sont prenant en charge d’une alerte - configurer hello service toosend des notifications d’alerte par courrier électronique. Pour plus d’informations sur la configuration des notifications par e-mail, consultez [Configurer les notifications](backup-azure-monitor-vms.md#configure-notifications).

## <a name="how-do-i-find-information-about-hello-alerts"></a>Comment trouver des informations sur les alertes de hello ?
tooview plus d’informations sur l’événement hello qui a généré une alerte, vous devez ouvrir le panneau des alertes de sauvegarde hello. Il existe panneau alertes de sauvegarde de deux façons tooopen hello : hello vignette d’alertes de sauvegarde dans le tableau de bord coffre hello ou à partir du panneau des alertes et événements hello.

vignette du panneau des alertes de sauvegarde tooopen hello à partir d’alertes de sauvegarde :

* Sur hello **les alertes de sauvegarde** vignette sur le tableau de bord coffre hello, cliquez sur **critique** ou **avertissement** tooview hello les événements opérationnels pour ce niveau de gravité.

    ![Vignette Alertes de sauvegarde](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

panneau des alertes de sauvegarde hello tooopen à partir du panneau des alertes et événements hello :

1. À partir du tableau de bord du coffre hello, cliquez sur **tous les paramètres**. ![Bouton Tous les paramètres](./media/backup-azure-monitor-vms/all-settings-button.png)
2. Sur hello **paramètres** panneau, cliquez sur **alertes et événements**. ![Bouton Alertes et événements](./media/backup-azure-monitor-vms/alerts-and-events-button.png)
3. Sur hello **alertes et événements** panneau, cliquez sur **les alertes de sauvegarde**. ![Bouton Alertes de sauvegarde](./media/backup-azure-monitor-vms/backup-alerts.png)

    Hello **les alertes de sauvegarde** panneau s’ouvre et affiche hello alertes filtrés.

    ![Vignette Alertes de sauvegarde](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. tooview des informations détaillées sur une alerte donnée, à partir de la liste de hello des événements, cliquez sur tooopen d’alerte hello son **détails** panneau.

    ![Détail sur l’événement](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    les attributs de hello toocustomize affichés dans la liste hello, consultez [afficher les attributs d’événement supplémentaires](backup-azure-monitor-vms.md#view-additional-event-attributes)

## <a name="configure-notifications"></a>Configurer les notifications
 Vous pouvez configurer hello service toosend par courrier électronique des alertes hello qui se sont produites sur hello après les heures, ou lorsque des types particuliers d’événements se produisent.

tooset des notifications par courrier électronique pour les alertes

1. Cliquez sur alertes de sauvegarde hello, **configurer des notifications**

    ![Menu Alertes de sauvegarde](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    Panneau de Hello configurer des notifications s’ouvre.

    ![Panneau Configurer les notifications](./media/backup-azure-monitor-vms/configure-notifications.png)
2. Dans le panneau de notifications configurer hello, notifications par courrier électronique, cliquez sur **sur**.

    Hello destinataires et les boîtes de dialogue de gravité ont une étoile toothem suivant, car ces informations sont requises. Fournissez au moins une adresse e-mail et sélectionnez au moins un niveau de gravité.
3. Bonjour **destinataires (courrier électronique)** boîte de dialogue, tapez les adresses de messagerie hello pour qui reçoivent des notifications de hello. Utilisez le format hello : username@domainname.com. Séparez les adresses e-mail par des point-virgule (;).
4. Bonjour **notifier** zone, choisissez **par alerte** toosend notification quand hello spécifié alerte se produit, ou **horaire Digest** toosend un résumé de la dernière heure de hello.
5. Bonjour **gravité** boîte de dialogue, sélectionnez un ou plusieurs niveaux que vous souhaitez tootrigger les notifications par courrier électronique.
6. Cliquez sur **Enregistrer**.

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a>Quels sont les types d’alertes disponibles pour la sauvegarde des machines virtuelles Azure IaaS ?
   | Niveau d’alerte | Alertes envoyées |
   | --- | --- |
   | Critique |Échec de sauvegarde, échec de récupération |
   | Avertissement |Aucun |
   | Informations |Aucun |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a>Existe-t-il des situations lors desquelles un e-mail n’est pas envoyé même si les notifications sont configurées ?
Il existe des situations où une alerte n’est envoyée, même si les notifications hello ont été correctement configurées. Bonjour les notifications de messagerie situations suivantes ne sont pas envoyées tooavoid bruit des alertes :

* Si les notifications sont configurée tooHourly Digest, et une alerte est déclenchée et résolue au sein de l’heure de hello.
* travail de Hello est annulé.
* Si un travail de sauvegarde est déclenché et échoue, et si un autre travail de sauvegarde est en cours.
* Une tâche de sauvegarde planifiée pour un ordinateur virtuel activée de gestionnaire de ressources démarre, mais hello machine virtuelle n’existe plus.

## <a name="customize-your-view-of-events"></a>Personnaliser l’affichage des événements
Hello **journaux d’Audit** paramètre est fourni avec un ensemble prédéfini de filtres et de colonnes affichant des informations d’événement opérationnel. Vous pouvez personnaliser hello affichage afin que lorsque hello **événements** panneau s’ouvre, il affiche hello les informations souhaitées.

1. Bonjour [tableau de bord coffre](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), cliquez sur le tooand Parcourir **les journaux d’Audit** tooopen hello **événements** panneau.

    ![Journaux d’audit](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Hello **événements** panneau s’ouvre les événements opérationnels toohello filtrés pour le coffre hello actuel.

    ![Filtre des journaux d’audit](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    Panneau de Hello répertorie hello critique, erreur, avertissement et les événements d’information qui s’est produite dans hello semaine dernière. intervalle de temps Hello est une valeur par défaut définie dans hello **filtre**. Hello **événements** panneau affiche également un graphique à barres de suivi lorsque les événements hello s’est produite. Si vous ne souhaitez pas toosee hello graphique à barres, hello **événements** menu, cliquez sur **masquer graphique** tootoggle hors graphique de hello. affichage par défaut de Hello d’événements affiche des informations d’opération, niveau, état, ressources et l’heure. Pour plus d’informations sur l’exposition des attributs d’événement supplémentaires, consultez la section de hello [développant des informations sur les événements](backup-azure-monitor-vms.md#view-additional-event-attributes).
2. Pour plus d’informations sur un événement opérationnel, Bonjour **opération** colonne, cliquez sur un événement opérationnel de tooopen son panneau. Panneau de Hello contient des informations détaillées sur les événements de hello. Les événements sont regroupés par leur ID de corrélation et une liste d’événements hello qui s’est produite dans l’intervalle de temps hello.

    ![Détails de l'opération](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. tooview des informations détaillées sur un événement particulier, à partir de la liste de hello des événements, cliquez sur hello événement tooopen son **détails** panneau.

    ![Détail sur l’événement](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    informations de niveau de l’événement Hello soient de détail hello Obtient des informations. Si vous préférez afficher autant d’informations sur chaque événement et que vous aimeriez tooadd cela beaucoup de détail toohello **événements** panneau, consultez la section de hello [développant des informations sur les événements](backup-azure-monitor-vms.md#view-additional-event-attributes).

## <a name="customize-hello-event-filter"></a>Personnaliser le filtre d’événement hello
Hello d’utilisation **filtre** tooadjust ou choisissez les informations de hello qui s’affiche dans un panneau spécifique. informations sur les événements toofilter hello :

1. Bonjour [tableau de bord coffre](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), cliquez sur le tooand Parcourir **les journaux d’Audit** tooopen hello **événements** panneau.

    ![Journaux d’audit](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Hello **événements** panneau s’ouvre les événements opérationnels toohello filtrés pour le coffre hello actuel.

    ![Filtre des journaux d’audit](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. Sur hello **événements** menu, cliquez sur **filtre** tooopen ce panneau.

    ![ouvrir le panneau Filtre](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. Sur hello **filtre** panneau, ajuster hello **niveau**, **intervalle de temps**, et **appelant** filtres. Hello autres filtres ne sont pas disponibles dans la mesure où ils ont été définies plus d’informations en cours tooprovide hello pour les Services de récupération hello coffre.

    ![Détails de la requête de journaux d’audit](./media/backup-azure-monitor-vms/filter-blade.png)

    Vous pouvez spécifier hello **niveau** d’événement : critique, erreur, avertissement ou information. Vous pouvez combiner plusieurs niveaux d’événements, mais vous devez sélectionner au moins un niveau. Activer ou désactiver l’hello niveau. Hello **intervalle de temps** filtre vous permet de durée hello toospecify pour capturer des événements. Si vous utilisez un intervalle de temps personnalisé, vous pouvez définir hello démarrage et l’heure de fin.
4. Une fois que vous êtes prêt tooquery hello journaux des opérations à l’aide de votre filtre, cliquez sur **mise à jour**. les résultats de Hello affichent de hello **événements** panneau.

    ![Détails de l'opération](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a>Afficher les attributs d’événement supplémentaires
À l’aide de hello **colonnes** bouton, vous pouvez activer tooappear d’attributs supplémentaires d’événement dans la liste hello sur hello **événements** panneau. liste des événements par défaut de Hello affiche des informations pour l’opération, niveau, état, ressources et l’heure. tooenable des attributs supplémentaires :

1. Sur hello **événements** panneau, cliquez sur **colonnes**.

    ![Colonnes ouvertes](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    Hello **choisir les colonnes** panneau s’ouvre.

    ![Panneau Colonnes](./media/backup-azure-monitor-vms/columns-blade.png)
2. tooselect hello d’attribut, cliquez sur la case à cocher hello. case à cocher de Hello attribut Active et se désactive.
3. Cliquez sur **réinitialiser** liste de hello tooreset d’attributs Bonjour **événements** panneau. Après l’ajout ou suppression d’attributs à partir de la liste de hello, utilisez **réinitialiser** tooview hello nouvelle liste des attributs d’événement.
4. Cliquez sur **mise à jour** tooupdate les données de hello dans les attributs d’événement hello. Hello tableau suivant fournit des informations sur chaque attribut.

| Nom de la colonne | Description |
| --- | --- |
| Opération |nom Hello d’opération de hello |
| Level |Hello au niveau de l’opération de hello, les valeurs peuvent être : information, avertissement, erreur ou critique |
| État |État descriptif de l’opération de hello |
| Ressource |URL qui identifie la ressource de hello ; également connu sous les ID de ressource hello |
| Temps |Durée, mesurée à partir de hello heure actuelle, lorsque l’événement de hello s’est produite |
| Appelant |Qui ou ce qu’appelée ou a déclenché l’événement de hello ; peut être hello système ou un utilisateur |
| Timestamp |temps de Hello lorsque hello a été déclenché |
| Groupe de ressources |groupe de ressources Hello |
| Type de ressource |type de ressource interne Hello utilisée par le Gestionnaire de ressources |
| Identifiant d’abonnement |Hello associé ID d’abonnement |
| Catégorie |Catégorie d’événement de hello |
| ID de corrélation : |Identifiant courant des événements connexes |

## <a name="use-powershell-toocustomize-alerts"></a>Utiliser les alertes de toocustomize PowerShell
Vous pouvez obtenir des notifications d’alerte personnalisées pour les travaux de hello dans le portail de hello. tooget ces tâches, définir alerte basée sur PowerShell règles sur hello opérationnel journalise les événements. Utilisez *PowerShell version 1.3.0 ou ultérieure*.

toodefine un tooalert de notification personnalisée pour les échecs de sauvegarde, utilisez une commande telle que hello script suivant :

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

**ID de ressource** : vous pouvez obtenir les ID de ressource de hello journaux d’Audit. Hello ResourceId est une URL fournie dans la colonne de ressource hello de journaux des opérations de hello.

**NomOpération** : NomOpération est au format de hello » Microsoft.RecoveryServices/recoveryServicesVault/*EventName*» où *EventName* peut être :<br/>

* S’inscrire <br/>
* Unregister  <br/>
* ConfigureProtection  <br/>
* Backup  <br/>
* Restore  <br/>
* StopProtection  <br/>
* DeleteBackupData  <br/>
* CreateProtectionPolicy  <br/>
* DeleteProtectionPolicy  <br/>
* UpdateProtectionPolicy  <br/>

**État** : les valeurs prises en charge sont Démarré, Réussi ou Échec.

**Le groupe de ressources** : il s’agit de hello groupe de ressources toowhich hello ressource appartient. Vous pouvez ajouter des journaux de toohello généré colonne hello groupe de ressources. Groupe de ressources est un des types disponibles de hello d’informations sur les événements.

**Nom** : nom de la règle d’alerte de hello.

**CustomEmail** : spécifiez toowhich d’adresse de messagerie personnalisés hello souhaité toosend une notification d’alerte

**SendToServiceOwners** : cette option envoie des notifications d’alerte tooall administrateurs et coadministrateurs d’abonnement de hello. Elle peut être utilisée dans l’applet de commande **New-AzureRmAlertRuleEmail** .

### <a name="limitations-on-alerts"></a>Limitations sur les alertes
Alertes basées sur les événements sont toohello sujet limites suivantes :

1. Des alertes sont déclenchées sur tous les ordinateurs virtuels hello de coffre Recovery Services. Vous ne pouvez pas personnaliser alerte hello pour un sous-ensemble d’ordinateurs virtuels dans un coffre Recovery Services.
2. Cette fonctionnalité est en version préliminaire. [En savoir plus](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Les alertes sont envoyées par « alerts-noreply@mail.windowsazure.com ». Actuellement, vous ne pouvez pas modifier expéditeur du courrier électronique hello.

## <a name="next-steps"></a>Étapes suivantes
Journaux des événements d’audit prise en charge des opérations de sauvegarde hello et activer excellent post-mortem. Hello opérations suivantes est enregistré :

* S’inscrire
* Unregister 
* Configurer la protection
* Sauvegarde (sauvegarde planifiée et à la demande)
* Restore 
* Arrêter la protection
* Supprimer les données de sauvegarde
* Add policy
* Supprimer la stratégie
* Mettre à jour la stratégie
* Annuler le travail

Pour obtenir une explication générale des événements, les opérations et les journaux d’audit sur hello services Azure, consultez l’article hello, [afficher les événements et journaux d’audit](../monitoring-and-diagnostics/insights-debugging-with-events.md).

Pour plus d’informations sur la manière de recréer une machine virtuelle à partir d’un point de récupération, consultez [Restauration de machines virtuelles Azure](backup-azure-restore-vms.md). Si vous avez besoin d’informations sur la protection de vos machines virtuelles, consultez [tout d’abord rechercher : sauvegardez tooa de machines virtuelles de coffre Recovery Services](backup-azure-vms-first-look-arm.md). En savoir plus sur les tâches de gestion hello pour les sauvegardes de machine virtuelle dans l’article hello, [les sauvegardes de machines virtuelles Azure de gérer](backup-azure-manage-vms.md).
