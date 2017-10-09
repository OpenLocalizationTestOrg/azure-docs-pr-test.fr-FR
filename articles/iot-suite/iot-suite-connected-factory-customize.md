---
title: "aaaCustomize Azure IoT Suite connecté fabrique | Documents Microsoft"
description: "Obtenir une description de l’interconnexion de comportement de hello toocustomize Hello fabrique de solution préconfigurée."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Personnaliser l’interconnexion hello fabrique solution affiche les données à partir de vos serveurs OPC UA

## <a name="introduction"></a>Introduction

Hello fabrique connecté solution rassemble et affiche les données d’hello OPC UA serveurs connectés toohello solution. Vous pouvez parcourir et envoyer des commandes toohello OPC UA serveurs dans votre solution. Pour plus d’informations sur OPC UA, consultez hello [connecté fabrique FAQ](iot-suite-faq-cf.md).

Les exemples de données agrégées en une solution de hello de hello l’efficacité des équipements globale (OEE) et les indicateurs de Performance clés (KPI) que vous pouvez afficher dans le tableau de bord hello à la fabrique de hello, des lignes et des niveaux de la station. Hello capture d’écran suivante affiche hello les valeurs OEE et d’indicateur de performance clé pour hello **Assembly** station sur **Production ligne 1**, Bonjour **Munich** usine :

![Exemple de valeurs OEE et l’indicateur de performance clé dans la solution de hello][img-oee-kpi]

permet de solution Hello vous tooview détaillée des informations à partir d’éléments de données spécifiques à partir de hello serveurs OPC UA, appelés *stations*. Hello capture d’écran suivante montre les tracés de nombre hello des articles fabriqués à partir d’une station de travail spécifique :

![Graphiques du nombre d’éléments fabriqués][img-manufactured-items]

Si vous cliquez sur un des graphiques de hello, vous pouvez explorer les données de hello à l’aide des temps série Insights (STI) :

![Explorer les données à l’aide de Time Series Insights][img-tsi]

Cet article explique :

- Comment les données de salutation sont établie à toohello disponible différentes vues dans la solution de hello.
- Comment vous pouvez personnaliser la solution de hello moyen hello affiche les données de hello.

## <a name="data-sources"></a>Sources de données

Bonjour fabrique connecté solution affiche les données à partir de hello OPC UA serveurs connectés toohello solution. installation par défaut de Hello comprend plusieurs serveurs de OPC UA une simulation de fabrication en cours d’exécution. Vous pouvez ajouter vos propres serveurs OPC UA qui [se connecter via une passerelle] [ lnk-connect-cf] tooyour solution.

Vous pouvez parcourir les éléments de données hello qu’un serveur OPC UA connecté peut envoyer tooyour solution dans le tableau de bord hello :

1. Accédez toohello **, sélectionnez un serveur OPC UA** vue :

    ![Accédez toohello sélectionner une vue du serveur OPC UA][img-select-server]

1. Sélectionnez un serveur et cliquez sur **Connect** (Connexion). Cliquez sur **continuer** lorsque l’avertissement de sécurité hello s’affiche.

    > [!NOTE]
    > Cet avertissement apparaît une fois pour chaque serveur uniquement et établit une relation d’approbation entre le tableau de bord de solution hello et serveur de hello.

1. Vous pouvez parcourir les éléments de données hello qui hello server peuvent envoyer toohello solution. Les éléments qui sont envoyés toohello solution ont une coche verte :

    ![Éléments publiés][img-published]

1. Si vous êtes un *administrateur* dans la solution de hello, vous pouvez choisir toopublish un toomake d’élément de données accessibles dans hello connecté solution de fabrique. En tant qu’administrateur, vous pouvez également modifier la valeur hello d’éléments de données et appeler les méthodes Bonjour server de OPC UA.

## <a name="map-hello-data"></a>Mapper les données de salutation

Hello connecté des mappages de solution de fabrique et hello d’agrégats publié des éléments de données à partir de hello OPC UA server toohello différentes vues dans la solution de hello. Hello fabrique connecté solution déploie tooyour compte Azure lorsque vous configurez la solution de hello. Un fichier JSON Bonjour Visual Studio connecté fabrique solution stocke ces informations de mappage. Vous pouvez afficher et modifier ce fichier de configuration JSON dans la fabrique de hello connecté solution Visual Studio. Vous pouvez redéployer la solution de hello après avoir apporté une modification.

Vous pouvez utiliser le fichier de configuration hello pour :

- Modifier les fabriques simulé existant de hello, les lignes de la production et les stations.
- Mapper des données à partir des serveurs OPC UA réels que vous vous connectez toohello solution.

tooclone une copie de hello connecté solution Visual Studio de fabrique, hello utiliser git commande suivante :

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

fichier de Hello **ContosoTopologyDescription.json** définit hello vues de mappage à partir de hello données du serveur OPC UA éléments toohello tableau de bord de solution hello fabrique connecté. Vous pouvez trouver ce fichier de configuration Bonjour **Contoso\Topology** dossier Bonjour **WebApp** projet Bonjour solution Visual Studio.

le contenu du fichier JSON de hello Hello est organisé comme une hiérarchie de fabrique, ligne de production et les nœuds de station. Cette hiérarchie définit la hiérarchie de navigation hello dans tableau de bord hello fabrique connecté. Valeurs sur chaque nœud de hiérarchie de hello déterminent les informations hello affichées dans le tableau de bord hello. Par exemple, le fichier JSON de hello contient hello valeurs pour hello fabrique de Munich suivantes :

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

emplacement, la description et nom de hello s’affichent dans cette vue dans le tableau de bord hello :

![Données Munich dans le tableau de bord hello][img-munich]

Chaque usine, ligne de production et poste présente une propriété image. Vous pouvez trouver ces fichiers JPEG Bonjour **Content\img** dossier Bonjour **WebApp** projet. Ces fichiers image s’affichent dans tableau de bord hello fabrique connecté.

Chaque station comprend plusieurs propriétés détaillées qui définissent le mappage des éléments de données de hello OPC UA de hello. Ces propriétés sont décrites dans les sections suivantes de hello :

### <a name="opcuri"></a>OpcUri

Hello **OpcUri** valeur est hello OPC UA Application URI qui identifie de façon unique hello server de OPC UA. Par exemple, hello **OpcUri** valeur pour la station d’assembly hello sur la ligne de production 1 de Munich ressemble à hello suivantes : **urn : scada2194:ua:munich:productionline0:assemblystation**.

Vous pouvez afficher hello URI des serveurs OPC UA hello connecté dans le tableau de bord de solution hello :

![Afficher l’URI des serveurs OPC UA][img-server-uris]

### <a name="simulation"></a>Simulation

Hello informations Bonjour **Simulation** nœud est toohello spécifique simulation OPC UA qui s’exécute dans hello serveurs OPC UA qui sont configurés par défaut. Elles ne sont pas utilisées pour un serveur OPC UA réel.

### <a name="kpi1-and-kpi2"></a>Kpi1 et Kpi2

Ces nœuds décrivent comment les données à partir de la station de hello contribuent toohello deux valeurs d’indicateur de performance clé dans le tableau de bord hello. Dans un déploiement par défaut, ces valeurs de KPI sont des unités par heure et des kWh. solution de Hello calcule les valeurs d’indicateur de performance clé au niveau d’une station de hello et agrège les niveaux de fabrique et de la ligne de production hello.

Chaque KPI présente une valeur minimale, maximale et cible. Chaque valeur d’indicateur de performance clé peut également définir des actions d’alerte pour hello connecté fabrique solution tooperform. Hello extrait de code suivant montre les définitions d’indicateur de performance clé hello pour station d’assembly hello sur la ligne de production 1 de Munich :

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

Hello capture d’écran suivante montre hello KPI données dans le tableau de bord hello.

![Informations d’indicateur de performance clé dans le tableau de bord hello][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

Hello **OpcNodes** identifient les nœuds hello des éléments de données publiées à partir de hello server de OPC UA et spécifiez comment tooprocess ces données.

Hello **NodeId** valeur identifie hello NodeID de UA OPC spécifique à partir de hello server de OPC UA. Hello premier nœud station d’assembly hello pour la ligne de production 1 de Munich a la valeur **ns = 2 ; i = 385**. A **NodeId** valeur spécifie tooread d’élément de données hello hello server de OPC UA et hello **SymbolicName** fournit un nom convivial toouse dans le tableau de bord hello pour ces données.

Autres valeurs associées à chaque nœud sont résumées dans hello tableau suivant :

| Valeur | Description |
| ----- | ----------- |
| Pertinence  | valeurs d’indicateur de performance clé et OEE Hello ces données contribuent à. |
| OpCode     | Comment les données de salutation sont agrégées. |
| Units      | toouse d’unités Hello dans le tableau de bord hello.  |
| Visible    | Si toodisplay cette valeur de tableau de bord hello. Certaines valeurs sont utilisées dans les calculs mais ne sont pas affichées.  |
| Maximale    | valeur maximale Hello qui déclenche une alerte dans le tableau de bord hello. |
| MaximumAlertActions | Un tootake action dans l’alerte tooan de réponse. Par exemple, envoyer une station tooa de commande. |
| ConstValue | Valeur constante utilisée dans un calcul. |

## <a name="deploy-hello-changes"></a>Déployer les modifications de hello

Lorsque vous avez terminé d’apporter des modifications toohello **ContosoTopologyDescription.json** fichier, vous devez redéployer hello connecté fabrique solution tooyour compte Azure.

Hello **azure iot-connecté-usine** référentiel inclut un **build.ps1** script PowerShell vous pouvez utiliser toorebuild et déployer des solutions de hello.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur hello connecté fabrique préconfiguré solution hello lors de la lecture suivante d’articles :

* [Procédure pas à pas de la solution préconfigurée d’usine connectée][lnk-rm-walkthrough]
* [Déployer une passerelle pour une usine connectée][lnk-connect-cf]
* [Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]
* [FAQ sur la fabrique connectée](iot-suite-faq-cf.md)
* [FAQ][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md