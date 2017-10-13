---
title: "Surveiller l’état de la réplication Active Directory avec Azure Log Analytics | Microsoft Docs"
description: "Le pack de solution État de la réplication Active Directory surveille régulièrement votre environnement Active Directory pour déterminer si des échecs de réplication se produisent et indique les résultats dans votre tableau de bord OMS."
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
ms.openlocfilehash: bfe52ef5d9d09ffe179faaf6ffbd90ef964fbda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Surveiller l’état de la réplication Active Directory avec Log Analytics

![Symbole de l’état de la réplication AD](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Active Directory est un composant clé de l’environnement informatique d’une entreprise. Pour garantir une haute disponibilité et des performances élevées, chaque contrôleur de domaine a sa propre copie de la base de données Active Directory. Les contrôleurs de domaine se répliquent entre eux pour propager les modifications dans l’entreprise. L’échec de ce processus de réplication peut entraîner divers problèmes au sein de l’entreprise.

Le pack de solution État de la réplication AD surveille régulièrement votre environnement Active Directory pour déterminer si des échecs de réplication se produisent et indique les résultats dans votre tableau de bord OMS.

## <a name="installing-and-configuring-the-solution"></a>Installation et configuration de la solution
Utilisez les informations suivantes pour installer et configurer la solution.

* Vous devez installer des agents sur les contrôleurs de domaine qui sont membres du domaine à évaluer. Sinon, vous devez installer des agents sur les serveurs membres et les configurer de façon à envoyer des données de réplication AD à OMS. Pour comprendre comment connecter des ordinateurs Windows directement à OMS, consultez [Connecter des ordinateurs Windows à Log Analytics](log-analytics-windows-agents.md). Si votre contrôleur de domaine fait déjà partie d’un environnement System Center Operations Manager existant que vous souhaitez connecter à OMS, consultez la page [Connecter Operations Manager à Log Analytics](log-analytics-om-agents.md).
* Ajoutez la solution État de la réplication Active Directory à votre espace de travail OMS en utilisant le processus décrit dans la rubrique [Ajouter des solutions Log Analytics à partir de la galerie de solutions](log-analytics-add-solutions.md).  Aucune configuration supplémentaire n’est requise.

## <a name="ad-replication-status-data-collection-details"></a>Détails de la collecte des données pour la solution État de la réplication AD
Le tableau suivant présente les méthodes de collecte des données et d’autres informations sur le mode de collecte pour la solution État de la réplication AD.

| plateforme | Agent direct | Agent SCOM | Stockage Azure | SCOM requis ? | Données de l’agent SCOM envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |tous les cinq jours |

## <a name="optionally-enable-a-non-domain-controller-to-send-ad-data-to-oms"></a>Autoriser éventuellement un ordinateur autre qu’un contrôleur de domaine à envoyer les données AD à OMS
Si vous ne souhaitez pas connecter directement un de vos contrôleurs de domaine à OMS, vous pouvez utiliser n’importe quel autre ordinateur connecté à OMS de votre domaine afin de collecter des données pour le pack de solution AD Replication Status et de faire en sorte qu’il les envoie.

### <a name="to-enable-a-non-domain-controller-to-send-ad-data-to-oms"></a>Pour autoriser un ordinateur autre qu’un contrôleur de domaine à envoyer les données AD à OMS
1. Vérifiez que l’ordinateur est membre du domaine que vous souhaitez analyser à l’aide de la solution État de la réplication AD.
2. [Connectez l’ordinateur Windows à OMS](log-analytics-windows-agents.md) ou [connectez-le à l’aide de votre environnement Operations Manager existant à OMS](log-analytics-om-agents.md), s’il n’est pas déjà connecté.
3. Sur cet ordinateur, définissez la clé de Registre suivante :

   * Clé : **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**
   * Valeur : **IsTarget**
   * Données de la valeur : **true**

   > [!NOTE]
   > Ces modifications ne prennent effet qu’une fois que vous avez redémarré le service Microsoft Monitoring Agent (HealthService.exe).
   >
   >

## <a name="understanding-replication-errors"></a>Présentation des erreurs de réplication
Une fois les données AD Replication Status envoyées à OMS, une vignette de ce type apparaît dans le tableau de bord OMS, indiquant le nombre actuel d’erreurs de réplication.  
![Vignette de l’état de la réplication AD](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

Les **erreurs de réplication critiques** sont celles qui se produisent à au moins 75 % de la [durée de vie des objets tombstone](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) de votre forêt Active Directory.

Quand vous cliquez sur la vignette, des informations complémentaires sur les erreurs apparaissent.
![Tableau de bord de l’état de la réplication AD](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>Destination Server Status (État du serveur de destination) et Source Server Status (État du serveur source)
Ces colonnes indiquent l’état des serveurs de destination et sources sur lesquels se produisent des erreurs de réplication. Le nombre après chaque nom de contrôleur de domaine indique le nombre d’erreurs de réplication sur ce contrôleur de domaine.

Les erreurs affichées concernent les serveurs de destination et les serveurs sources, car un problème peut être plus facile à résoudre selon que l’on se place du côté des serveurs sources ou du côté des serveurs de destination.

Dans cet exemple, la plupart des serveurs de destination ont à peu près le même nombre d’erreurs, tandis qu’un serveur source (ADDC35) en a beaucoup plus que tous les autres. Un problème affecte probablement le serveur ADDC35 au point de l’empêcher d’envoyer des données à ses partenaires de réplication. Résoudre les problèmes sur ADDC35 permettra peut-être de résoudre la plupart des erreurs qui s’affichent dans la zone des serveurs de destination.

### <a name="replication-error-types"></a>Replication Error Types (Types d’erreurs de réplication)
Cette zone fournit des informations sur les types d’erreurs détectés au sein de votre entreprise. Chaque erreur a un code numérique unique et un message qui peut vous aider à déterminer sa cause.

L’anneau en haut vous donne une idée de la fréquence des erreurs dans votre environnement.

Il vous indique quand plusieurs contrôleurs de domaine rencontrent la même erreur de réplication. Dans ce cas, vous pourrez peut-être détecter ou identifier une solution sur un contrôleur de domaine, puis la répéter sur les autres contrôleurs de domaine affectés par la même erreur.

### <a name="tombstone-lifetime"></a>durée de vie des objets tombstone (TSL)
La durée de vie des objets tombstone (TSL) détermine la durée pendant laquelle un objet supprimé, appelé objet tombstone, est conservé dans la base de données Active Directory. Quand un objet supprimé dépasse la durée de vie des objets tombstone (TSL), un processus de garbage collection le supprime automatiquement de la base de données Active Directory.

La durée de vie des objets tombstone (TSL) par défaut est de 180 jours pour les versions les plus récentes de Windows, contre 60 jours sur les versions antérieures, et elle peut être modifiée explicitement par un administrateur Active Directory.

Il est important de savoir si certaines erreurs de réplication se produisent près ou au-delà du terme de la durée de vie des objets tombstone. Si deux contrôleurs de domaine rencontrent une erreur de réplication qui persiste au-delà de la durée de vie des objets tombstone, la réplication est désactivée entre ces deux contrôleurs de domaine, même si l’erreur de réplication sous-jacente est corrigée.

La zone Tombstone Lifetime (Durée de vie des objets tombstone) vous aide à identifier les endroits où il risque d’y avoir une réplication désactivée. Chaque erreur de la catégorie **Over 100% TSL** (Plus de 100 % TSL) représente une partition qui n’a pas été répliquée entre ses serveur source et de destination pendant au moins la durée de vie des objets tombstone (TSL) de la forêt.

Dans ce cas, la simple correction de l’erreur de réplication ne suffit pas. Vous devez au minimum effectuer une recherche manuelle pour identifier et nettoyer les objets en attente avant de redémarrer la réplication. Vous pouvez même être amené à mettre hors service un contrôleur de domaine.

Une fois que vous avez identifié les erreurs de réplication qui ont persisté au-delà de la durée de vie des objets tombstone, vous pouvez porter votre attention sur les erreurs des catégories **50-75% TSL** ou **75-100% TSL**.

Il s’agit d’erreurs en attente et non temporaires, dont la résolution nécessite probablement votre intervention. Le point positif est qu’elles n’ont pas encore atteint la durée de vie des objets tombstone (TSL). Si vous résolvez ces problèmes rapidement et *avant* qu’elles atteignent la durée de vie des objets tombstone (TSL), la réplication peut redémarrer avec une intervention manuelle minimale.

Comme indiqué précédemment, la vignette du tableau de bord pour la solution État de la réplication AD affiche le nombre d’erreurs de réplication *critiques* dans votre environnement, à savoir les erreurs présentes au-delà de 75 % de la durée de vie des objets tombstone (TSL) (dont celles au-delà de 100 % de cette durée de vie). Faites en sorte que ce nombre demeure à 0.

> [!NOTE]
> Tous les calculs de pourcentage de la durée de vie des objets tombstone (TSL) reposent sur la durée de vie des objets tombstone (TSL) réelle de votre forêt Active Directory ; ainsi, vous pouvez considérer que ces pourcentages sont exacts, même si une valeur personnalisée est définie pour la durée de vie des objets tombstone (TSL).
>
>

### <a name="ad-replication-status-details"></a>Détails de l’état de la réplication AD
Quand vous cliquez sur un élément d’une liste, des informations supplémentaires le concernant apparaissent grâce à la Recherche dans les journaux. Les résultats sont filtrés pour afficher uniquement les erreurs liées à cet élément. Par exemple, si vous cliquez sur le premier contrôleur de domaine listé sous **Destination Server Status (ADDC02)** (État du serveur de destination (ADDC02)), les résultats de la recherche sont filtrés de manière à présenter les erreurs qui affectent ce contrôleur de domaine en tant que serveur de destination :

![Erreurs de l’état de la réplication AD dans les résultats de la recherche](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

Vous pouvez ensuite affiner le filtrage, modifier la requête de recherche, entre autres. Pour plus d’informations sur l’utilisation de la recherche de journal, consultez [Recherches de journal](log-analytics-log-searches.md).

Le champ **HelpLink** affiche l’URL d’une page TechNet contenant des détails supplémentaires sur l’erreur concernée. Vous pouvez copier et coller ce lien dans la fenêtre du navigateur pour afficher des informations sur le dépannage et la résolution de l’erreur.

Vous pouvez également cliquer sur **Exporter** pour exporter les résultats vers Excel. Exporter les données des erreurs de réplication vous permet de les visualiser comme vous le souhaitez.

![Erreurs de l’état de réplication AD exportées dans Excel](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>FAQ sur l’état de la réplication AD
**Q : Quelle est la fréquence de la mise à jour de l’état de la réplication AD ?**
R : Les informations sont mises à jour tous les cinq jours.

**Q : Est-il possible de configurer la fréquence de la mise à jour de ces données ?**
R : Pas pour l’instant.

**Q : Dois-je ajouter tous mes contrôleurs de domaine à mon espace de travail OMS pour afficher l’état de réplication ?**
R : Non, un seul contrôleur de domaine doit être ajouté. Si vous avez plusieurs contrôleurs de domaine dans votre espace de travail OMS, toutes leurs données sont envoyées à OMS.

**Q : Je ne veux pas ajouter de contrôleurs de domaine à mon espace de travail OMS. Puis-je néanmoins utiliser la solution État de la réplication AD ?**
R. : Oui. Vous pouvez définir la valeur d’une clé de Registre pour l’activer. Voir [Pour autoriser un ordinateur autre qu’un contrôleur de domaine à envoyer les données AD à OMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

**Q : Quel est le nom du processus qui effectue la collecte de données ?**
R : AdvisorAssessment.exe

**Q : Combien de temps la collecte de données prend-elle ?**
R : La durée de la collecte de données dépend de la taille de l’environnement Active Directory, mais est généralement inférieure à 15 minutes.

**Q : Quels types de données sont collectés ?**
R : Les informations de réplication sont recueillies par le biais de LDAP.

**Q : Est-il possible de configurer les périodes de collecte de données ?**
R : Pas pour l’instant.

**Q : Quelles autorisations dois-je avoir pour collecter les données ?**
R : Les autorisations utilisateur normales sur Active Directory sont suffisantes.

## <a name="troubleshoot-data-collection-problems"></a>Résoudre les problèmes de collecte de données
Pour que le pack de solution État de la réplication AD puisse collecter des données, vous devez connecter au moins un contrôleur de domaine à votre espace de travail OMS. Un message indiquant que **les données sont toujours en cours de collecte** s’affiche tant que vous n’avez pas connecté de contrôleur de domaine.

Pour obtenir de l’aide sur la connexion d’un contrôleur de domaine, consultez la documentation [Connecter des ordinateurs Windows à Log Analytics](log-analytics-windows-agents.md). Ou bien, si votre contrôleur de domaine est déjà connecté à un environnement System Center Operations Manager, vous pouvez consulter la documentation [Connexion de System Center Operations Manager à Log Analytics](log-analytics-om-agents.md).

Si vous ne souhaitez connecter aucun de vos contrôleurs de domaine directement à OMS ou à SCOM, consultez la page [Autoriser un ordinateur autre qu’un contrôleur de domaine à envoyer des données AD à OMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [Recherches de journal dans Log Analytics](log-analytics-log-searches.md) pour afficher des données détaillées sur l’état de la réplication Active Directory.
