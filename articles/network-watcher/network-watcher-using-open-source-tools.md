---
title: "modèles de trafic réseau aaaVisualize avec l’Observateur de réseau Azure et d’outils open source | Documents Microsoft"
description: "Cette page décrit comment la capture de paquet de l’Observateur réseau toouse avec tooand de modèles Capanalysis toovisualize le trafic à partir de vos machines virtuelles."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Visualiser tooand de modèles de trafic réseau à partir de vos machines virtuelles à l’aide d’outils open source

Les captures de paquets contiennent des données de réseau qui permettent une analyse de réseau tooperform, l’inspection approfondie des paquets. Il existe s’affiche de nombreux outils source vous pouvez utiliser tooanalyze paquet captures toogain insights sur votre réseau. L’un de ces outils est CapAnalysis, un outil de visualisation de capture de paquets open source. Visualisation des données de capture de paquet est un moyen très utile tooquickly tirer des leçons sur les modèles et les anomalies dans votre réseau. Les visualisations fournissent également un moyen de partager ces informations d’une manière facilement consommable.

Observateur de réseau de Azure fournit que vous hello toocapture possibilité capture de ces données précieuses en vous tooperform paquet sur votre réseau. Dans cet article, nous fournissons une procédure pas à pas comment insights toovisualize et d’accéder à partir du paquet capture à l’aide de CapAnalysis avec l’Observateur réseau.

## <a name="scenario"></a>Scénario

Vous avez une application web simple déployée sur une machine virtuelle dans Azure que vous souhaitez toouse open source outils toovisualize son tooquickly de trafic réseau identifier toute anomalie possibles et les modèles de flux. Avec Network Watcher, vous pouvez obtenir une capture de paquets de votre environnement réseau et la stocker directement dans votre compte de stockage. CapAnalysis ensuite réception hello capture des paquets directement à partir de l’objet blob de stockage hello et visualiser son contenu.

![scénario][1]

## <a name="steps"></a>Étapes

### <a name="install-capanalysis"></a>Installation de CapAnalysis

tooinstall CapAnalysis sur un ordinateur virtuel, vous pouvez faire référence les instructions officiel toohello https://www.capanalysis.net/ca/how-to-install-capanalysis ici.
Accès CapAnalysis à distance, nous devons tooopen port 9877 sur votre machine virtuelle en ajoutant une nouvelle règle de sécurité de trafic entrant. Pour plus d’informations sur la création de règles dans les groupes de sécurité réseau, consultez trop[créer des règles dans un groupe de sécurité réseau existant](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). Une fois que la règle de hello a été ajouté avec succès, vous devez être en mesure de tooaccess CapAnalysis à partir de`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Utilisez toostart l’Observateur réseau Azure un paquet de capture de session

Observateur réseau vous permet de trafic de tootrack toocapture paquets vers et depuis un ordinateur virtuel. Vous pouvez faire référence à des instructions de toohello à [captures de paquets de gérer d’observateur réseau](network-watcher-packet-capture-manage-portal.md) toostart une session de capture de paquet. Cette capture des paquets peut être stockée dans un toobe d’objet blob de stockage accédé par CapAnalysis.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Télécharger un tooCapAnalysis de capture de paquet
Vous pouvez télécharger directement d’une capture de paquets prise par l’Observateur réseau à l’aide d’onglet de « Importation à partir de l’URL » hello et en fournissant un objet blob de lien toohello stockage où la capture des paquets hello est stockée.

Lorsque vous fournissez un lien de tooCapAnalysis, assurez-vous que tooappend une URL de blob de stockage toohello jeton SAS.  toodo, accédez tooShared signature d’accès de compte de stockage hello, désignez hello les autorisations accordée, appuyez sur toocreate de bouton hello SAS de générer un jeton. Vous pouvez ensuite ajouter cette URL de blob de stockage SAS toohello jeton paquet capture.

Hello URL résultante ressemble à ceci : http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Analyse des captures de paquets

CapAnalysis offre différentes options toovisualize la capture des paquets, chaque ainsi que l’analyse à partir d’une perspective différente. Ces synthèses visuelles vous permettent de comprendre les tendances du trafic réseau et d’identifier rapidement les activités inhabituelles. Certaines de ces fonctionnalités sont répertoriées dans hello suivant liste :

1. Tables des flux

    Ce tableau vous propose vous hello liste de flux de données de paquets hello, hello horodatage associé au flux de hello et hello différents protocoles associés aux flux de hello, ainsi que les IP source et de destination.

    ![page de flux capanalysis][5]

1. Vue d’ensemble du protocole

    Ce volet vous permet de tooquickly consultez distribution hello du trafic réseau via hello différents protocoles et des zones géographiques différentes.

    ![vue d’ensemble du protocole capanalysis][6]

1. Statistiques

    Ce volet permet de vous tooview statistiques de trafic réseau-octets envoyés et reçus à partir de la source et les adresses IP, les flux pour chaque source de hello et de destination, des adresses IP de destination de protocole utilisé pour différents flux et la durée de hello de flux.

    ![statistiques de capanalysis][7]

1. Carte des zones géographiques

    Ce volet vous offre une vue de mappage de votre trafic réseau, volume toohello du trafic de chaque pays de mise à l’échelle de couleurs. Vous pouvez sélectionner le pays en surbrillance tooview flux supplémentaires des statistiques telles que proportion hello de données envoyés et reçus à partir d’adresses IP dans ce pays.

    ![carte des zones géographiques][8]

1. Filtres

    CapAnalysis fournit un ensemble de filtres pour l’analyse rapide de paquets spécifiques. Par exemple, vous pouvez choisir les données de salutation toofilter par protocole toogain spécifiques des informations sur ce sous-ensemble de trafic.

    ![filtres][11]

    Visitez [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn plus d’informations sur les fonctionnalités des tous les CapAnalysis.

## <a name="conclusion"></a>Conclusion

Fonctionnalité de capture de paquet de l’Observateur réseau vous permet de post-mortem de données nécessaires tooperform réseau toocapture hello et mieux comprendre votre trafic réseau. Dans ce scénario, nous vous avons montré comment intégrer facilement les captures de paquets de Network Watcher avec des outils de visualisation open source. À l’aide des outils open source tels que les paquets toovisualize CapAnalysis capture, vous pouvez effectuer une inspection approfondie des paquets et identifier rapidement les tendances au sein de votre trafic réseau.

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les journaux de flux de groupe de sécurité réseau, visitez [consigne des flux de groupe de sécurité réseau](network-watcher-nsg-flow-logging-overview.md)

Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
