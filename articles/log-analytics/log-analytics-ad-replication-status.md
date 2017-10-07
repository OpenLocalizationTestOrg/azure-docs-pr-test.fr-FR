---
title: "état de réplication d’Active Directory avec Azure journal Analytique d’aaaMonitor | Documents Microsoft"
description: "Hello pack de solution d’état de réplication Active Directory régulièrement surveille votre environnement Active Directory pour les échecs de réplication et signale les résultats hello sur votre tableau de bord OMS."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Surveiller l’état de la réplication Active Directory avec Log Analytics

![Symbole de l’état de la réplication AD](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Active Directory est un composant clé de l’environnement informatique d’une entreprise. tooensure haute disponibilité et hautes performances, chaque contrôleur de domaine possède sa propre copie de base de données Active Directory hello. Contrôleurs de domaine répliquent entre eux dans classer les modifications de toopropagate dans toute entreprise de hello. Échecs de ce processus de réplication peuvent provoquer de nombreux problèmes dans toute entreprise de hello.

Hello pack de solution d’état de la réplication AD surveille votre environnement Active Directory pour les échecs de réplication régulièrement et signale les résultats hello sur votre tableau de bord OMS.

## <a name="installing-and-configuring-hello-solution"></a>L’installation et la configuration de solution de hello
Utilisez hello suivant tooinstall des informations et configurer une solution de hello.

* Vous devez installer des agents sur les contrôleurs de domaine qui sont membres de hello domaine toobe est évaluée. Ou bien, vous devez installer des agents sur les serveurs membres et configurer hello agents toosend AD réplication données tooOMS. toounderstand tooconnect tooOMS d’ordinateurs Windows, voir [tooLog d’ordinateurs Windows de se connecter Analytique](log-analytics-windows-agents.md). Si votre contrôleur de domaine fait déjà partie d’un environnement System Center Operations Manager existant que vous souhaitez tooconnect tooOMS, consultez [connecter Operations Manager tooLog Analytique](log-analytics-om-agents.md).
* Ajouter hello état de réplication Active Directory solution tooyour espace de travail OMS à l’aide du processus de hello décrit dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).  Aucune configuration supplémentaire n’est requise.

## <a name="ad-replication-status-data-collection-details"></a>Détails de la collecte des données pour la solution État de la réplication AD
Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour l’état de la réplication AD.

| plateforme | Agent direct | Agent SCOM | Stockage Azure | SCOM requis ? | Données de l’agent SCOM envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |tous les cinq jours |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>Si vous le souhaitez, activer un tooOMS de données toosend AD non-contrôleurs de domaine
Si vous ne souhaitez tooconnect un de vos contrôleurs de domaine directement tooOMS, vous pouvez utiliser n’importe quel autre ordinateur connecté à OMS dans votre toocollect de domaine, les données pour hello solution de l’état de la réplication AD pack et qu’il envoie des données de salutation.

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>tooenable un tooOMS de données toosend AD non-contrôleurs de domaine
1. Vérifiez que hello de l’ordinateur est membre du domaine hello que vous souhaitez toomonitor à l’aide de la solution d’état de réplication hello AD.
2. [Se connecter hello Windows ordinateur tooOMS](log-analytics-windows-agents.md) ou [se connecter à l’aide de votre tooOMS d’environnement Operations Manager existant](log-analytics-om-agents.md), s’il n’est pas déjà connecté.
3. Sur cet ordinateur, définissez hello clé de Registre suivante :

   * Clé : **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**
   * Valeur : **IsTarget**
   * Données de la valeur : **true**

   > [!NOTE]
   > Ces modifications ne prennent pas d’effet jusqu'à ce que votre hello de redémarrer le service Microsoft Monitoring Agent (HealthService.exe).
   >
   >

## <a name="understanding-replication-errors"></a>Présentation des erreurs de réplication
Une fois que vous avez des données d’état de réplication AD envoyées tooOMS, vous voyez un toohello similaire vignette suivant d’image de tableau de bord OMS hello indiquant combien vous avez actuellement des erreurs de réplication.  
![Vignette de l’état de la réplication AD](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**Erreurs de réplication critique** sont des erreurs qui se trouvent dans ou supérieure à 75 % de hello [durée de vie de temporisation](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) pour votre forêt Active Directory.

Lorsque vous cliquez sur la vignette de hello, vous pouvez afficher plus d’informations sur les erreurs de hello.
![Tableau de bord de l’état de la réplication AD](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>Destination Server Status (État du serveur de destination) et Source Server Status (État du serveur source)
Ces colonnes indiquent l’état hello de serveurs de destination et les serveurs sources qui rencontrent des erreurs de réplication. nombre de Hello après que chaque nom de contrôleur de domaine indique le nombre de hello d’erreurs de réplication sur ce contrôleur de domaine.

erreurs de Hello pour les serveurs de destination et source sont affichés, car certains problèmes sont tootroubleshoot plus facile à partir de la perspective de serveur hello source et autres utilisateurs du point de vue serveur de destination hello.

Dans cet exemple, vous pouvez voir que le nombre de serveurs de destination ont à peu près hello même nombre d’erreurs, mais il existe un serveur source (ADDC35) qui a beaucoup d’erreurs plus que hello tous les autres utilisateurs. Il est probable qu’il existe un problème sur ADDC35 qui provoque le partenaires de réplication tooits toofail toosend données. Résoudre les problèmes de hello sur ADDC35 peut résoudre la plupart des erreurs de hello qui s’affichent dans la zone de serveur de destination hello.

### <a name="replication-error-types"></a>Replication Error Types (Types d’erreurs de réplication)
Cette zone fournit des informations sur les types hello d’erreurs détectées au sein de votre entreprise. Chaque erreur possède un code numérique unique et un message qui peut vous aider à déterminer la cause première hello d’erreur de hello.

anneau Hello haut hello vous donne une idée des erreurs s’affichent plus et moins souvent dans votre environnement.

Il vous indique lorsque plusieurs contrôleurs de domaine expérience hello même erreur de réplication. Dans ce cas, vous pouvez être en mesure de toodiscover ou identifier une solution sur un contrôleur de domaine, puis répétez sur d’autres contrôleurs de domaine faisant l’objet hello même erreur.

### <a name="tombstone-lifetime"></a>durée de vie des objets tombstone (TSL)
durée de vie de désactivation Hello détermine la durée pendant laquelle un objet supprimé, appelée tooas un objet tombstone, est conservée dans la base de données Active Directory hello. Lorsqu’une durée de vie des objets supprimés passe hello désactivé (tombstone), un processus de garbage collection supprime automatiquement à partir de la base de données Active Directory hello.

durée de vie de désactivation Hello par défaut est de 180 jours pour les versions les plus récentes de Windows, mais il était 60 jours sur des versions antérieures, et il peut être modifié explicitement par un administrateur Active Directory.

Il est important tooknow si vous rencontrez des erreurs de réplication qui sont presque atteintes ou ont dépassé la durée de vie de désactivation hello. Si les deux contrôleurs de domaine de rencontrer une erreur de réplication qui persiste au-delà de durée de vie de désactivation hello, est désactiver la réplication entre les deux contrôleurs de domaine, même si hello réplication erreur sous-jacent est fixe.

zone de durée de vie de désactivation de Hello vous aide à identifier les endroits où la réplication a été désactivée est risque de se produire. Chaque erreur Bonjour **plus de 100 % TSL** catégorie représente une partition qui n’a pas répliqué entre son serveur source et de destination pour au moins durée de vie de désactivation hello pour la forêt hello.

Dans ce cas, le simplement résolution d’erreur de réplication hello sera pas suffisante. Au minimum, vous devez toomanually examiner tooidentify et nettoyer des objets en attente avant de pouvoir redémarrer la réplication. Vous devrez peut-être même de toodecommission un contrôleur de domaine.

Dans Ajout tooidentifying toutes les erreurs de réplication qui ont conservées au-delà de durée de vie de désactivation hello vous également erreurs de tooany toopay attention relèvent hello **50 à 75 % TSL** ou **75-100 % TSL** catégories.

Ce sont des erreurs qui sont clairement en attente, non temporaire, afin qu’ils probablement besoin de votre tooresolve intervention. excellente Hello est qu’ils n’ont pas encore atteint durée de vie de désactivation hello. Si vous corrigez ces problèmes rapidement et *avant* qu’ils atteignent la durée de vie de désactivation hello, la réplication peut redémarrer avec une intervention manuelle minimale.

Comme indiqué précédemment, vignette de tableau de bord hello pour la solution d’état de réplication hello AD montre le nombre hello de *critique* dans votre environnement, qui est défini en tant qu’erreurs sont plus de 75 % de la durée de vie de désactivation (y compris des erreurs de réplication erreurs sont plus de 100 % de TSL). S’efforcent tookeep ce nombre à 0.

> [!NOTE]
> Tous les calculs de pourcentage de durée de vie hello tombstone reposent sur la durée de vie hello tombstone réelle de votre forêt Active Directory, donc vous pouvez approuver que les pourcentages sont précis, même si vous disposez d’une valeur de durée de vie de temporisation personnalisée définie.
>
>

### <a name="ad-replication-status-details"></a>Détails de l’état de la réplication AD
Lorsque vous cliquez sur n’importe quel élément dans une des listes de hello, vous consultez des informations supplémentaires à l’aide de la recherche de journal. les résultats de Hello sont filtrées tooshow seul hello erreurs connexes toothat élément. Par exemple, si vous cliquez sur premier contrôleur de domaine hello répertoriés sous **état du serveur de Destination (ADDC02)**, vous voyez les résultats de recherche filtrés tooshow erreurs avec ce contrôleur de domaine répertorié comme serveur de destination hello :

![Erreurs de l’état de la réplication AD dans les résultats de la recherche](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

À ce stade, vous pouvez filtrer davantage, modifiez la requête de recherche hello et ainsi de suite. Pour plus d’informations sur l’utilisation de hello recherche de journal, consultez [recherche de journal](log-analytics-log-searches.md).

Hello **HelpLink** champ affiche l’URL de hello d’une page TechNet avec des détails supplémentaires sur cette erreur spécifique. Vous pouvez copier et coller ce lien dans votre navigateur fenêtre toosee d’informations sur la résolution des problèmes et de résolution d’erreur de hello.

Vous pouvez également cliquer sur **exporter** tooexport hello tooExcel des résultats. Exportation de données de hello peut vous aider à visualiser les données d’erreur de réplication de quelque manière que vous souhaitez.

![Erreurs de l’état de réplication AD exportées dans Excel](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>FAQ sur l’état de la réplication AD
**Q : Quelle est la fréquence de la mise à jour de l’état de la réplication AD ?**
R : informations de hello sont mise à jour tous les cinq jours.

**Q : existe-t-il un tooconfigure de façon que la fréquence à laquelle ces données sont mise à jour ?**
R : Pas pour l’instant.

**Q : dois-je tooadd tous de mon domaine contrôleurs toomy OMS espace de travail dans l’état de la réplication toosee ordre ?**
R : Non, un seul contrôleur de domaine doit être ajouté. Si vous avez plusieurs contrôleurs de domaine dans votre espace de travail OMS, toutes les données sont envoyées à tooOMS.

**Q : je ne souhaite pas tooadd n’importe quel espace de travail de domaine contrôleurs toomy OMS. Puis-je continuer à utiliser hello solution de l’état de la réplication Active Directory ?**
R. : Oui. Vous pouvez définir la valeur hello un tooenable de clé de Registre il. Consultez [tooenable un tooOMS de données non contrôleur de domaine toosend AD](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

**Q : qu’est nom hello du processus hello qui hello collecte de données ?**
R : AdvisorAssessment.exe

**Q : combien de temps faut-il pour toobe des données collectée ?**
R : heure de collecte de données de dépend de taille hello d’environnement Active Directory de hello, mais prend généralement moins de 15 minutes.

**Q : Quels types de données sont collectés ?**
R : Les informations de réplication sont recueillies par le biais de LDAP.

**Q : existe-t-il un moyen tooconfigure lorsque les données sont collectées ?**
R : Pas pour l’instant.

**Q : que faire autorisations ai-je besoin toocollect données ?**
A: tooActive d’autorisations utilisateur normal active sont suffisants.

## <a name="troubleshoot-data-collection-problems"></a>Résoudre les problèmes de collecte de données
Dans les données de la commande toocollect pack de solution d’état de réplication hello AD requiert au moins un domaine contrôleur toobe connecté tooyour espace de travail OMS. Un message indiquant que **les données sont toujours en cours de collecte** s’affiche tant que vous n’avez pas connecté de contrôleur de domaine.

Si vous avez besoin d’assistance de connexion d’un de vos contrôleurs de domaine, vous pouvez afficher la documentation à l’adresse [tooLog d’ordinateurs Windows de se connecter Analytique](log-analytics-windows-agents.md). Vous pouvez également, si votre contrôleur de domaine est déjà connecté tooan d’environnement System Center Operations Manager, vous pouvez afficher la documentation à [connecter System Center Operations Manager tooLog Analytique](log-analytics-om-agents.md).

Si vous ne souhaitez tooconnect un de vos contrôleurs de domaine directement tooOMS ou tooSCOM, consultez [tooenable un tooOMS de données non contrôleur de domaine toosend AD](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillé les données d’état de réplication Active Directory.
