---
title: "aaaManaging les données Azure Automation | Documents Microsoft"
description: "Cet article contient plusieurs rubriques concernant la gestion d’un environnement Azure Automation.  Il inclut actuellement Conservation des données, Sauvegarde Azure Automation et Récupération d'urgence dans Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>Gestion des données Azure Automation
Cet article contient plusieurs rubriques concernant la gestion d’un environnement Azure Automation.

## <a name="data-retention"></a>Conservation des données
Lorsque vous supprimez une ressource dans Azure Automation, elle est conservée pendant 90 jours à des fins d’audit avant d’être supprimée définitivement.  Vous ne peut pas voir ou utiliser les ressources hello pendant ce temps.  Cette stratégie s’applique également à tooresources qui appartient le compte d’automatisation tooan est supprimé.

Azure Automation supprime automatiquement et définitivement les tâches de plus de 90 jours.

Hello tableau suivant résume la stratégie de rétention hello pour différentes ressources.

| Données | Stratégie |
|:--- |:--- |
| Comptes |Supprimés définitivement 90 jours après que le compte de hello est supprimé par un utilisateur. |
| Éléments multimédias |Supprimés définitivement 90 jours après l’élément multimédia de hello est supprimé par un utilisateur ou 90 jours après hello compte qui contient l’élément multimédia de hello est supprimé par un utilisateur. |
| Modules |Supprimés définitivement 90 jours après le module de hello est supprimé par un utilisateur ou 90 jours après hello compte qui contenait le module de hello est supprimé par un utilisateur. |
| Runbooks |Supprimés définitivement 90 jours après la ressource de hello est supprimée par un utilisateur ou 90 jours après hello compte qui contient les ressources hello est supprimé par un utilisateur. |
| Tâches |Effacés et supprimés définitivement 90 jours après la dernière modification. Cela peut être après que le travail de hello, est arrêté ou est interrompu. |
| Configurations de nœud/fichiers MOF |L’ancienne configuration de nœud est supprimée définitivement 90 jours après la génération d'une nouvelle configuration de nœud. |
| Nœuds DSC |Supprimés définitivement 90 jours après le nœud de hello est plus inscrit dans le compte Automation à l’aide du portail Azure ou hello [Unregister-AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) applet de commande dans Windows PowerShell. Nœuds sont supprimés également définitivement 90 jours après compte hello qui contient le nœud de hello est supprimé par un utilisateur. |
| Rapports sur le nœud |Supprimés définitivement 90 jours après la création d'un nouveau rapport pour le nœud en question. |

stratégie de rétention Hello s’applique aux utilisateurs de tooall et ne peut pas être personnalisé.

Toutefois, si vous avez besoin des données de tooretain pour une période plus longue, vous pouvez transférer tooLog de journaux runbook tâche Analytique.  Pour plus d’informations, consultez [transférer tooOMS de données de tâche Azure Automation Analytique de journal](automation-manage-send-joblogs-log-analytics.md).   

## <a name="backing-up-azure-automation"></a>Sauvegarde d’Azure Automation
Lorsque vous supprimez un compte automation dans Microsoft Azure, tous les objets de compte de hello sont supprimées, y compris les runbooks, modules, configurations, paramètres, tâches et actifs. Impossible de récupérer les objets Hello après que hello compte est supprimé.  Vous pouvez utiliser hello suivant le contenu de hello toobackup informations de votre compte automation avant de le supprimer. 

### <a name="runbooks"></a>Runbooks
Vous pouvez exporter vos fichiers tooscript de runbooks à l’aide de hello portail de gestion Azure ou hello [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) applet de commande dans Windows PowerShell.  Ces fichiers de script peuvent être importés dans un autre compte Automation, comme indiqué dans l’article [Création ou importation d'un Runbook](https://msdn.microsoft.com/library/dn643637.aspx).

### <a name="integration-modules"></a>Modules d'intégration
Vous ne pouvez pas exporter les modules d'intégration depuis Azure Automation.  Vous devez vous assurer qu’ils sont disponibles en dehors du compte automation de hello.

### <a name="assets"></a>Éléments multimédias
Vous ne pouvez pas exporter d’ [éléments](https://msdn.microsoft.com/library/dn939988.aspx) depuis Azure Automation.  À l’aide de hello portail de gestion Azure, vous devez noter les détails hello de variables, les informations d’identification, les certificats, les connexions et les planifications.  Vous devez ensuite créer manuellement les ressources qui seront utilisées par les Runbooks que vous importerez dans une autre Automation.

Vous pouvez utiliser [applets de commande Azure](https://msdn.microsoft.com/library/dn690262.aspx) tooretrieve les détails des biens non chiffrés et enregistrer les futur fait référence ou créer des ressources équivalentes dans un autre compte automation.

Vous ne peut pas récupérer la valeur hello pour les variables chiffrées ou un champ de mot de passe hello d’informations d’identification à l’aide des applets de commande.  Si vous ne connaissez pas ces valeurs, vous pouvez les récupérer à partir d’un runbook à l’aide de hello [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) et [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) activités.

Vous ne pouvez pas exporter de certificats depuis Azure Automation.  Vous devez vous assurer que tous les certificats sont disponibles en dehors d'Azure.

### <a name="dsc-configurations"></a>Configurations DSC
Vous pouvez exporter votre tooscript des fichiers de configuration à l’aide de hello portail de gestion Azure ou hello [Export-AzureRmAutomationDscConfiguration](https://msdn.microsoft.com/library/mt603485.aspx) applet de commande dans Windows PowerShell. Ces configurations peuvent être importées et utilisées dans un autre compte Automation.

## <a name="geo-replication-in-azure-automation"></a>Géo-réplication dans Azure Automation
Géo-réplication, standard dans les comptes Azure Automation, sauvegarde de la région géographique différente tooa compte données pour assurer la redondance. Lors de la configuration de votre compte, vous pouvez choisir une région primaire, puis une région secondaire est attribuée automatiquement tooit. données secondaires Hello, copiées à partir de la région principale de hello, sont régulièrement mis à jour en cas de perte de données.  

Hello tableau suivant montre les couplages de la région primaire et secondaire disponible hello.

| Primaire | Secondaire |
| --- | --- |
| Sud du centre des États-Unis |Nord du centre des États-Unis |
| Est des États-Unis 2 |Centre des États-Unis |
| Europe de l'Ouest |Europe du Nord |
| Asie du Sud-Est |Asie de l'Est |
| Est du Japon |Ouest du Japon |

Hello improbable qu’une donnée de la région principale est perdue, Microsoft tente toorecover il. Si les données principales hello ne peut pas être récupérées, puis basculement géographique est effectué et hello clients concernés seront notifiées à ce sujet via leur abonnement.

