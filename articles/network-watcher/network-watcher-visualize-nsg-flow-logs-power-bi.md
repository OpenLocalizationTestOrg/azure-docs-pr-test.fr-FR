---
title: "aaaVisualizing flux du groupe de sécurité réseau Azure se connecte à Power BI | Documents Microsoft"
description: "Cette page décrit le mode de journalisation des flux de groupe de sécurité réseau toovisualize avec Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Visualisation des journaux de flux des groupes de sécurité réseau Azure avec Power BI

Journaux de flux de groupe de sécurité réseau permettent de tooview informations du trafic IP entrant et sortant sur les groupes de sécurité réseau. Ces journaux flux affiche sortant et les flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur les flux de hello (Source/Destination IP, Port de la Source et de Destination, protocole), et si le trafic de hello a été autorisé ou refusé.

Il peut être difficile toogain connaître de flux de journalisation des données en recherchant manuellement les fichiers journaux de hello. Dans cet article, nous fournissons un toovisualize solution votre flux plus récent consigne et en savoir plus sur le trafic sur votre réseau.

## <a name="scenario"></a>Scénario

Bonjour scénario, nous connecter compte de stockage de bureau toohello Power BI que nous avons configurés en tant que récepteur d’hello pour notre groupe de sécurité réseau de flux de données. Une fois que nous avons connecté compte de stockage tooour, Power BI télécharge et analyse hello journaux tooprovide une représentation visuelle du trafic hello enregistrées par les groupes de sécurité du réseau.

À l’aide d’éléments visuels de hello fournis dans le modèle hello que vous pouvez examiner :

* Principaux consommateurs
* Données de flux chronologiques par direction et par règle de décision
* Flux par adresse MAC d’interface réseau
* Flux par groupe de sécurité réseau et par règle
* Flux par port de destination

modèle Hello fourni est modifiable afin d’en modifier tooadd nouvelles données, des éléments visuels, ou modifier des requêtes toosuit vos besoins.

## <a name="setup"></a>Paramétrage

Avant de commencer, la journalisation des flux de groupe de sécurité réseau doit être activée sur un ou plusieurs groupes de sécurité réseau de votre compte. Pour obtenir des instructions sur l’activation de la sécurité du réseau de flux de journaux, consultez l’article suivant de toohello : [journalisation tooflow de présentation pour les groupes de sécurité réseau](network-watcher-nsg-flow-logging-overview.md).

Vous client devez également être hello Power BI Desktop installé sur votre ordinateur et suffisamment d’espace libre sur votre ordinateur toodownload et charge hello journal des données qui existent dans votre compte de stockage.

![Diagramme Visio][1]

### <a name="steps"></a>Étapes

1. Téléchargez et ouvrez hello suivant le modèle de Power BI Bonjour Power BI Desktop Application [Power BI de l’Observateur réseau flux enregistre le modèle](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Entrez les paramètres de requête hello requis
    1. **StorageAccountName** – Spécifie le nom de compte de stockage hello flux de groupe de sécurité réseau hello contenant les journaux que vous avez toohello serait tels que tooload et visualiser.
    1. **NumberOfLogFiles** – Spécifie le nombre de hello de fichiers journaux que vous souhaitez toodownload et visualiser dans Power BI. Par exemple, si 50 est spécifié, hello 50 fichiers journaux plus récents. FF que nous avons 2 groupes de sécurité réseau activé et configuré de compte de toothis toosend NSG de journaux, puis hello dernières heures 25 des journaux peuvent être affichés.

    ![page d’accueil Power BI][2]

1. Entrez hello clé d’accès pour votre compte de stockage. Vous pouvez trouver les clés d’accès valide en naviguant dans le compte de stockage tooyour Bonjour Azure portail et en sélectionnant **clés d’accès** à partir du menu Paramètres de hello. Cliquez sur **Connecter**, puis appliquez les modifications.

    ![clés d'accès][3]

    ![clé d’accès 2][4]

4.  Les journaux sont télécharger analysé et vous pouvez désormais utiliser des éléments visuels créés au préalable hello.

## <a name="understanding-hello-visuals"></a>Présentation des éléments visuels de hello

Condition Bonjour modèle sont un ensemble d’éléments visuels qui aident à faciliter le décryptage hello données du journal de flux de groupe de sécurité réseau. Hello images suivantes montrent un exemple de quel tableau de bord hello ressemble lorsque rempli avec les données. Nous allons examiner ci-dessous en détail chaque représentation visuelle 

![powerbi][5]
 
Haut Hello consommateurs montre visual hello des adresses IP que vous avez lancé hello la plupart des connexions sur hello période spécifiée. taille de Hello de zones de hello correspond toohello le nombre relatif de connexions. 

![toptalkers][6]

Hello graphiques de série de temps suivants montrent nombre hello de flux période hello. graphique de supérieur Hello est segmentée en direction du flux hello et hello inférieur est segmentée en hello décision (autorisation ou refus). Avec cet élément visuel, vous pouvez examiner les tendances du trafic au fil du temps et repérer les pics ou baisses d’activité anormaux au niveau du trafic ou de la segmentation du trafic.

![flowsoverperiod][7]

Hello graphiques suivants montrent les flux hello par interface réseau, avec hello supérieur segmentées par la direction du flux et hello inférieur segmentées par une décision de. Avec ces informations, vous pouvez obtenir de vos machines virtuelles communiqués hello la plupart des tooothers relatif, et si le trafic tooa machine virtuelle spécifique est en cours d’autorisée ou refusée.

![flowspernic][8]

Hello suivant graphique roue montre une répartition de flux par le Port de Destination. Avec ces informations, vous pouvez afficher les ports de destination de hello les plus courants utilisés dans hello spécifié période.

![donut][9]

Hello graphique à barres suivant montre hello flux par groupe de sécurité réseau et de la règle. Avec ces informations, vous pouvez voir hello NSG responsable hello la plupart des trafic et répartition hello du trafic sur un groupe de sécurité réseau par règle.

![barchart][10]
 
Hello suivantes affichent des informations graphiques d’information sur les groupes de sécurité réseau hello présents dans les journaux de hello, hello nombre de flux capturées sur la période de hello et date hello de hello plus ancien journal est capturé. Ces informations vous donnent une idée de quels groupes de sécurité réseau sont enregistrés et hello la plage de dates de flux.

![infochart1][11]

![infochart2][12]

Ce modèle inclut hello suivants des segments tooallow vous tooview uniquement les données de salutation vous intéressez le plus. Vous pouvez appliquer un filtre sur vos groupes de ressources, sur les groupes de sécurité réseau et sur les règles. Vous pouvez également filtrer sur les informations de 5 tuples, la décision et temps de hello journal de hello a été écrit.

![slicers][13]

## <a name="conclusion"></a>Conclusion

Nous vous avons montré dans ce scénario qu’en utilisant les journaux de flux de groupe de sécurité réseau fournis par l’Observateur réseau et Power BI, nous sont en mesure de toovisualize et comprendre le trafic de hello. À l’aide du modèle de hello fourni, Power BI télécharge les journaux de hello directement à partir du stockage et les traite localement. Modèle de hello tooload durée varie selon le nombre hello de fichiers requis et la taille totale des fichiers téléchargés.

Vous pouvez toocustomize libre ce modèle pour vos besoins. Il existe de nombreuses manières d’utiliser Power BI avec les journaux de flux des groupes de sécurité réseau. 

## <a name="notes"></a>Remarques

* Par défaut, les journaux sont stockés dans `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * Si d’autres données existent dans un autre répertoire ils hello toopull de requêtes et traiter les données hello doivent être modifiées.

* modèle de Hello fourni n’est pas recommandée pour une utilisation avec plus de 1 Go de journaux.

* Si vous disposez d’une grande quantité de journaux, nous vous recommandons de rechercher une solution à l’aide d’un autre magasin de données tel que Data Lake ou SQL Server.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toovisualize votre flux de groupe de sécurité réseau consigne avec hello Elastick pile en vous rendant sur [visualiser tooand de modèles de trafic réseau à partir de vos machines virtuelles à l’aide d’outils open source](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
