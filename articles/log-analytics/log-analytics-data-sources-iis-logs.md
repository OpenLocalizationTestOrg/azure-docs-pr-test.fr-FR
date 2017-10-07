---
title: aaaIIS consigne dans le journal Analytique | Documents Microsoft
description: "Internet Information Services (IIS) enregistre l'activité des utilisateurs dans des fichiers journaux qui peuvent être collectés par Log Analytics.  Cet article décrit comment collection tooconfigure de journaux IIS et les détails des enregistrements de hello créent dans le référentiel d’OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Journaux IIS dans Log Analytics
Internet Information Services (IIS) enregistre l'activité des utilisateurs dans des fichiers journaux qui peuvent être collectés par Log Analytics.  

![Journaux IIS](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Configuration de journaux IIS
Log Analytics regroupant les entrées des fichiers journaux créés par IIS, vous devez [configurer IIS pour la journalisation](https://technet.microsoft.com/library/hh831775.aspx).

Log Analytics prend en charge uniquement les fichiers journaux IIS stockés au format W3C, et ne prend pas en charge les champs personnalisés ou IIS Advanced Logging.  
Log Analytics ne collecte pas de journaux aux formats natifs NCSA ou IIS.

Configurer les journaux IIS dans le journal Analytique de hello [menu données de paramètres de journal Analytique](log-analytics-data-sources.md#configuring-data-sources).  Aucune configuration n’est requise autre que la sélection de l’option **Collecter les fichiers journaux IIS au format W3C**.

Nous recommandons que, lorsque vous activez la collecte de journaux IIS, vous devez configurer le paramètre de substitution journal hello IIS sur chaque serveur.

## <a name="data-collection"></a>Collecte des données
Log Analytics collecte les entrées du journal IIS de chaque source connectée toutes les 15 minutes environ.  l’agent Hello enregistre sa place dans chaque journal des événements qu’il collecte à partir de.  Si l’agent de hello est mis hors connexion, puis Analytique de journal collecte les événements à partir de l’endroit où il s’était arrêté, même si ces événements ont été créés lors de l’agent de hello est hors connexion.

## <a name="iis-log-record-properties"></a>Propriétés d’enregistrement de journal IIS
Enregistrements de journal IIS ont un type de **W3CIISLog** et ont des propriétés de hello Bonjour tableau suivant :

| Propriété | Description |
|:--- |:--- |
| Ordinateur |Nom de l’ordinateur hello hello événements ont été collectée à partir de. |
| cIP |Adresse IP du client de hello. |
| csMethod |Méthode de demande de hello tels que GET ou POST. |
| csReferer |Site que hello utilisateur cliqué sur le lien de site en cours de toohello. |
| csUserAgent |Type de navigateur du client de hello. |
| csUserName |Nom de hello de l’utilisateur qui a accédé hello serveur authentifié. Les utilisateurs anonymes sont indiqués par un trait d'union. |
| csUriStem |Cible de la demande de hello telle qu’une page web. |
| csUriQuery |La requête, le cas échéant, que le client hello tentait tooperform. |
| ManagementGroupName |Nom du groupe d’administration hello pour les agents d’Operations Manager.  Pour les autres agents, il s’agit d’AOI-\<workspace ID\> |
| RemoteIPCountry |Pays de l’adresse IP de hello du client de hello. |
| RemoteIPLatitude |Latitude de l’adresse IP du client hello. |
| RemoteIPLongitude |Longitude de l’adresse IP du client hello. |
| scStatus |Code d'état HTTP. |
| scSubStatus |Code d'erreur du sous-état. |
| scWin32Status |Code d’état Windows. |
| sIP |Adresse IP du serveur web de hello. |
| SourceSystem |OpsMgr |
| sPort |Hello serveur hello client connecté au port. |
| sSiteName |Nom de site IIS de hello. |
| TimeGenerated |Date et heure hello est consignée. |
| TimeTaken |Demande de longueur de hello tooprocess de temps en millisecondes. |

## <a name="log-searches-with-iis-logs"></a>Recherches de journaux avec les journaux IIS
Hello tableau suivant fournit des exemples de requêtes de journal qui extrait des enregistrements de journal IIS.

| Interroger | Description |
|:--- |:--- |
| Type=W3CIISLog |Tous les enregistrements de journaux IIS. |
| Type=W3CIISLog scStatus=500 |Tous les enregistrements de journaux IIS dont l’état renvoyé est 500. |
| Type=W3CIISLog &#124; Measure count() by cIP |Nombre d’entrées de journaux IIS par adresse IP du client. |
| Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem |Nombre d’IIS entrées du journal par URL pour hello hôte www.contoso.com. |
| Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000 |Nombre total d'octets reçus par chaque ordinateur IIS. |

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivant.

> | Interroger | Description |
|:--- |:--- |
| W3CIISLog |Tous les enregistrements de journaux IIS. |
| W3CIISLog &#124; où scStatus==500 |Tous les enregistrements de journaux IIS dont l’état renvoyé est 500. |
| W3CIISLog &#124; résumer count() par cIP |Nombre d’entrées de journaux IIS par adresse IP du client. |
| W3CIISLog &#124; où csHost==« www.contoso.com » &#124; résumer count() par csUriStem |Nombre d’IIS entrées du journal par URL pour hello hôte www.contoso.com. |
| W3CIISLog &#124; résumer sum(csBytes) par ordinateur &#124; prendre 500000 |Nombre total d'octets reçus par chaque ordinateur IIS. |

## <a name="next-steps"></a>Étapes suivantes
* Configurer le journal Analytique toocollect autres [des sources de données](log-analytics-data-sources.md) pour l’analyse.
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.
* Configurer des alertes Analytique de journal tooproactively vous avertir des conditions importantes trouvées dans les journaux IIS.
