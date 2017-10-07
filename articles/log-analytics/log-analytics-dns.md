---
title: aaaDNS solution Analytique dans Analytique de journal Azure | Documents Microsoft
description: "Configurer et utiliser des solutions de DNS Analytique hello dans insights de toogather Analytique de journal dans l’infrastructure DNS sur la sécurité, les performances et les opérations."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>Collecter des informations sur votre infrastructure DNS avec hello solution d’aperçu Analytique de DNS

![Symbole DNS Analytics](./media/log-analytics-dns/dns-analytics-symbol.png)

Cet article décrit comment tooset configuration et utilisation hello solution Azure DNS Analytique dans insights de toogather Analytique de journal Azure dans l’infrastructure DNS sur la sécurité, les performances et les opérations.

DNS Analytics vous aide à effectuer les tâches suivantes :

- Identifier les clients qui tentent de noms de domaine malveillant tooresolve.
- Identifier les enregistrements de ressources obsolètes
- Identifier les noms de domaine fréquemment interrogés et les clients DNS communiquant
- Afficher la charge de la demande sur les serveurs DNS
- Afficher les échecs d’inscription DNS dynamique

solution de Hello collecte, analyse et met en corrélation le DNS Windows analytique et les journaux d’audit et les autres données connexes à partir de vos serveurs DNS.

## <a name="connected-sources"></a>Sources connectées

Hello tableau suivant décrit les sources de hello connecté sont pris en charge par cette solution :

| **Source connectée** | **Support** | **Description** |
| --- | --- | --- |
| [Agents Windows](log-analytics-windows-agents.md) | Oui | solution de Hello collecte des informations de DNS à partir d’agents Windows. |
| [Agents Linux](log-analytics-linux-agents.md) | Non | solution de Hello ne collecte pas les informations DNS depuis les agents Linux directes. |
| [Groupe d’administration de Microsoft System Center Operations Manager](log-analytics-om-agents.md) | Oui | solution de Hello collecte des informations de DNS à partir des agents dans un groupe d’administration Operations Manager connecté. Une connexion directe à partir de toohello de l’agent Operations Manager hello Operations Management Suite n’est pas nécessaire. Données sont transférées à partir du référentiel de hello gestion groupe toohello Operations Management Suite. |
| [Compte Azure Storage](log-analytics-azure-storage.md) | Non | Le stockage Azure n’est pas utilisé par la solution de hello. |

### <a name="data-collection-details"></a>Détails sur la collecte de données

solution de Hello collecte l’inventaire DNS et les données liées aux événements DNS auprès des serveurs DNS de hello où est installé un agent Analytique de journal. Ces données sont ensuite téléchargement tooLog Analytique et affichés dans le tableau de bord de solution hello. Les données liées au stock, telles que nombre de hello de serveurs DNS, les zones et les enregistrements de ressource, sont collectées en exécutant les applets de commande PowerShell pour DNS hello. les données de salutation sont mis à jour tous les deux jours. Hello liées aux événements collectées quasiment en temps réel à partir de hello [analytique et les journaux d’audit](https://technet.microsoft.com/library/dn800669.aspx#enhanc) fournie par enregistrement DNS et des diagnostics dans Windows Server 2012 R2 améliorées.

## <a name="configuration"></a>Configuration

Utilisez hello suivant la solution de hello tooconfigure informations :

- Vous devez avoir un [Windows](log-analytics-windows-agents.md) ou [Operations Manager](log-analytics-om-agents.md) agent sur chaque serveur DNS que vous souhaitez toomonitor.
- Vous pouvez ajouter l’espace de travail hello DNS Analytique solution tooyour Operations Management Suite de hello [Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace). Vous pouvez également utiliser hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).

solution de Hello commence à collecter des données sans avoir besoin de hello de configuration supplémentaire. Toutefois, vous pouvez utiliser hello suivant de collecte de données de configuration toocustomize.

### <a name="configure-hello-solution"></a>Configurer une solution de hello

Dans le tableau de bord hello solution, cliquez sur **Configuration** page de Configuration de DNS Analytique tooopen hello. Voici les deux types de modification de configuration que vous pouvez effectuer :

- **Noms de domaine de la liste verte**. solution de Hello ne traite pas de toutes les requêtes de recherche hello. Elle gère une liste verte des suffixes de nom de domaine. les requêtes de recherche Hello résoudre les noms de domaine toohello qui correspondent à des suffixes de noms de domaine dans cette liste d’autorisation ne sont pas traités par les solutions hello. Ne traite ne pas les noms de domaine dans la liste approuvée permet les données de salutation toooptimize envoyées tooLog Analytique. liste blanche d’adresses Hello par défaut inclut les noms de domaine public populaires tels que les www.google.com et www.facebook.com. Vous pouvez afficher la liste par défaut complète de hello faisant défiler l’écran.

 Vous pouvez modifier hello liste tooadd n’importe quel suffixe de nom de domaine insights de recherche tooview pour souhaitées. Vous pouvez également supprimer n’importe quel suffixe de nom de domaine que vous ne souhaitez pas insights de recherche tooview pour.

- **Seuil de clients communiquant**. Les clients DNS qui dépassent le seuil de hello pour nombre hello de demandes de recherche est mis en surbrillance dans hello **Clients DNS** panneau. seuil de Hello par défaut est 1 000. Vous pouvez modifier le seuil de hello.

    ![Noms de domaine de la liste verte](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>Packs d’administration

Si vous utilisez l’espace de travail hello Microsoft Monitoring Agent tooconnect tooyour Operations Management Suite, hello Pack d’administration suivant est installé :

- Microsoft DNS Data Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)

Si votre groupe d’administration Operations Manager est un espace de travail Operations Management Suite tooyour connecté, hello packs d’administration suivants sont installés dans Operations Manager lorsque vous ajoutez cette solution. Ces packs d’administration ne nécessitent aucune opération de configuration ou de maintenance :

- Microsoft DNS Data Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)
- Microsoft System Center Advisor DNS Analytics Configuration (Microsoft.IntelligencePack.Dns.Configuration)

Pour plus d’informations sur la façon dont les packs d’administration de solution sont mises à jour, consultez [connecter Operations Manager tooLog Analytique](log-analytics-om-agents.md).

## <a name="use-hello-dns-analytics-solution"></a>Utiliser la solution de DNS Analytique hello

Cette section décrit toutes les fonctions de tableau de bord hello et comment toouse les.

Une fois que vous avez ajouté l’espace de travail hello solution tooyour, vignette de solution hello sur la page de vue d’ensemble de Operations Management Suite hello fournit un résumé de votre infrastructure DNS. Il inclut le nombre hello des serveurs DNS dans lequel les données de salutation sont recueillies. Il inclut également le nombre de hello de demandes effectuées par les clients tooresolve malveillant domaines hello dernières 24 heures. Lorsque vous cliquez sur la vignette de hello, tableau de bord hello solution s’ouvre.

![Vignette DNS Analytics](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>Tableau de bord de solution

tableau de bord de solution Hello affiche des informations résumées pour hello diverses fonctionnalités de solution de hello. Il inclut également des liens toohello détaillée d’affichage pour l’analyse d’investigation et de diagnostic. Par défaut, les données de salutation sont indiquées pour hello sept derniers jours. Vous pouvez modifier la plage de date et d’heure hello à l’aide de hello **contrôle de sélection de date et d’heure**, comme indiqué dans hello suivant image :

![Contrôle de sélection de date/heure](./media/log-analytics-dns/dns-time.png)

tableau de bord de solution Hello affiche hello suivant panneaux :

**Sécurité DNS**. Rapports hello les clients DNS qui essaient toocommunicate avec des domaines malveillants. À l’aide de flux de Microsoft threat intelligence DNS Analytique peut détecter les clients qui essaient les domaines malveillants tooaccess des adresses IP. Dans de nombreux cas, les appareils infectés « numéroter » toohello « contrôle et commande » centre de domaine malveillant de hello en résolvant hello nom de domaine contre les programmes malveillants.

![Panneau Sécurité DNS](./media/log-analytics-dns/dns-security-blade.png)

Lorsque vous cliquez sur une adresse IP du client dans la liste de hello, recherche de journal s’ouvre et affiche les détails de la recherche de requête respectifs de hello hello. Dans l’exemple suivant de hello, Analytique de DNS a détecté que la communication de hello a été effectuée avec un [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![Résultats de recherche dans les journaux affichant un ircboot](./media/log-analytics-dns/ircbot.png)

informations de Hello vous aide à tooidentify le :

- Client IP qui a initié la communication de hello.
- Nom de domaine qui résout les adresses IP malveillantes de toohello.
- Résout les adresses IP qui hello du nom de domaine.
- Adresse IP malveillante
- Gravité du problème de hello.
- Raison de l’inscription sur liste noire des adresses IP malveillantes de hello.
- Heure de détection

**Domaines interrogés**. Fournit des hello plus fréquentes des noms de domaine qui est interrogées par les clients DNS de hello dans votre environnement. Vous pouvez afficher la liste hello de tous les noms de domaine hello interrogé. Vous pouvez également descendre dans les détails de la demande hello recherche d’un nom de domaine spécifique dans la recherche de journal.

![Panneau Domaines interrogés](./media/log-analytics-dns/domains-queried-blade.png)

**Clients DNS**. Rapports hello clients *violation de seuil de hello* pour le nombre de requêtes Bonjour choisi laps de temps. Vous pouvez afficher la liste des clients DNS de hello et détails hello de requêtes de hello effectuées par ces derniers dans recherche de journaux hello.

![Panneau Clients DNS](./media/log-analytics-dns/dns-clients-blade.png)

**Inscriptions DNS dynamiques**. Signale les échecs d’inscription de nom. Tous les échecs d’enregistrement d’adresse [enregistrements de ressource](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (Type de A et AAAA) sont mis en surbrillance en même temps que le client hello adresses IP qui a effectué des demandes d’inscription de hello. Vous pouvez ensuite utiliser cette informations toofind hello cause première de l’échec de l’enregistrement hello en procédant comme suit :

1. Rechercher zone hello faisant autorité pour le nom de hello hello client tente de tooupdate.

2. Utilisez hello solution toocheck hello les informations d’inventaire de cette zone.

3. Vérifiez que cette mise à jour dynamique hello de zone de hello est activée.

4. Vérifiez si la zone de hello est configuré pour la mise à jour dynamique sécurisée ou non.

    ![Panneau Inscriptions DNS dynamiques](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**Demandes d’inscriptions de noms**. Vignette supérieure de Hello montre une courbe de tendance des demandes de mise à jour dynamique DNS ayant réussies et ayant échouées. vignette inférieur de Hello répertorie les clients de 10 premiers hello qui envoient des demandes de mise à jour DNS ayant échouées toohello des serveurs DNS, triées par nombre hello d’échecs.

![Panneau Demandes d’inscriptions de noms ](./media/log-analytics-dns/name-reg-req-blade.png)

**Exemples de requêtes DDI Analytics**. Contient une liste de hello courants recherche les requêtes qui extraient les données brutes analytique directement.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Exemples de requêtes](./media/log-analytics-dns/queries.png)

Vous pouvez utiliser ces requêtes comme point de départ pour créer vos propres requêtes de génération de rapports personnalisés. les requêtes Hello lier la page de recherche de journal Analytique DNS toohello où les résultats sont affichés :

- **Liste des serveurs DNS**. Affiche une liste de tous les serveurs DNS avec le nom de domaine complet, le nom de domaine, le nom de la forêt et les adresses IP de serveur associés.
- **Liste des zones DNS**. Affiche une liste de toutes les zones DNS avec le nom de la zone associée hello, l’état de mise à jour dynamique, serveurs de noms et état de signature DNSSEC.
- **Enregistrements de ressources non utilisés**. Affiche une liste de tous les enregistrements d’inutilisé/périmée ressource hello. Cette liste contient le nom d’enregistrement de ressource de hello, type d’enregistrement de ressource, hello associé serveur DNS, les temps de génération d’enregistrement et nom de la zone. Vous pouvez utiliser cette liste tooidentify hello enregistrements DNS qui ne sont plus en cours d’utilisation. En fonction de ces informations, vous pouvez ensuite supprimer ces entrées à partir des serveurs DNS de hello.
- **Charge de requête des serveurs DNS**. Affiche des informations qui vous pouvez d’obtenir une perspective de hello que DNS charger sur vos serveurs DNS. Ces informations peuvent vous aider à planifier la capacité de hello pour les serveurs de hello. Vous pouvez accéder toohello **métriques** onglet Visualisation graphique de toochange hello vue tooa. Cet affichage vous permet de comprendre comment hello DNS charge est répartie entre vos serveurs DNS. Il indique les tendances des taux de requête DNS pour chaque serveur.

    ![Résultats de recherche dans les journaux des requêtes des serveurs DNS](./media/log-analytics-dns/dns-servers-query-load.png)

- **Charge de requête des zones DNS**. Montre hello statistiques de requête zone par seconde DNS de toutes les zones hello sur des serveurs DNS hello gérés par la solution de hello. Cliquez sur hello **métriques** onglet vue de hello toochange de visualisation de graphique tooa les enregistrements détaillés des résultats de hello.
- **Événements de configuration**. Affiche tous les événements de changement de configuration de DNS hello et des messages associés. Vous pouvez ensuite filtrer ces événements selon l’heure du serveur DNS de l’ID d’événement, événement hello, ou la catégorie de tâche. les données de salutation, vous peuvent auditer les serveurs DNS de toospecific modifications apportées à des moments spécifiques.
- **Journal analytique DNS**. Affiche tous les événements analytiques hello sur tous les serveurs DNS de hello gérés par la solution de hello. Vous pouvez ensuite filtrer ces événements basés sur l’heure du serveur DNS de l’ID d’événement, événement hello, adresse IP du client qui a effectué hello de requête de recherche et la catégorie de type de tâche de requête. Les événements analytiques DNS server activer sur le serveur DNS de hello de suivi d’activité. Un événement analytique est enregistré chaque fois que le serveur de hello envoie ou reçoit des informations DNS.

### <a name="search-by-using-dns-analytics-log-search"></a>Rechercher à l’aide de la recherche dans les journaux de DNS Analytics

Sur la page de recherche de journal hello, vous pouvez créer une requête. Vous pouvez filtrer les résultats de la recherche à l’aide des contrôles de facette. Vous pouvez également créer des rapports, le filtrage et des requêtes avancées tootransform sur vos résultats. Démarrer à l’aide de hello requêtes suivantes :

1. Bonjour **zone de requête de recherche**, type `Type=DnsEvents` tooview tous hello événements DNS générés par les serveurs DNS hello gérés par la solution de hello. données du journal hello pour toutes les modifications de configuration, les inscriptions dynamiques et événements connexes toolookup requêtes de liste des résultats de Hello.

    ![Recherche dans les journaux des événements DNS](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. les données de journal tooview hello pour les requêtes de recherche, sélectionnez **LookUpQuery** comme hello **sous-type** filtre du contrôle de code hello facette sur hello gauche. Une table qui répertorie tous les événements de requête de recherche de hello pour hello période sélectionnée s’affiche.

    b. les données de journal tooview hello pour les inscriptions dynamiques, sélectionnez **DynamicRegistration** comme hello **sous-type** filtre du contrôle de code hello facette sur hello gauche. Une table qui répertorie tous les événements de l’enregistrement dynamique hello pour hello période sélectionnée s’affiche.

    c. les données de journal tooview hello pour les modifications de configuration, sélectionnez **ConfigurationChange** comme hello **sous-type** filtre du contrôle de code hello facette sur hello gauche. Une table qui répertorie tous les événements de modification de la configuration hello pour hello période sélectionnée s’affiche.

2. Bonjour **zone de requête de recherche**, type `Type=DnsInventory` tooview tous hello données liées au stock DNS pour les serveurs DNS hello gérés par la solution de hello. données de journal hello pour les serveurs DNS, les zones DNS et les enregistrements de ressource de liste des résultats de Hello.

    ![Recherche dans les journaux des inventaires DNS](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>Commentaires

Vous pouvez créer fournir des commentaires de deux façons :

- **UserVoice**. Publier des idées pour DNS Analytique fonctionnalités toowork sur. Visitez hello [Operations Management Suite UserVoice page](https://aka.ms/dnsanalyticsuservoice).
- **Rejoignez notre cohorte**. Nous sommes toujours intéressés ayant des nouveaux clients joindre notre cohortes tooget anticipée toonew les fonctions d’accès et aidez-nous à améliorer DNS Analytique. Si vous souhaitez rejoindre notre cohorte, répondez à cette [enquête rapide](https://aka.ms/dnsanalyticssurvey).

## <a name="next-steps"></a>Étapes suivantes

[Rechercher des journaux](log-analytics-log-searches.md) tooview détaillées DNS les enregistrements de journal.
