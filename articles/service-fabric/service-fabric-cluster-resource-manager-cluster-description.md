---
title: aaaCluster Description du Gestionnaire de ressources Cluster | Documents Microsoft
description: "Qui décrit un cluster Service Fabric en spécifiant les domaines d’erreur, mettre à niveau des domaines, propriétés de nœud et les capacités de nœud pour hello Gestionnaire de ressources du Cluster."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>Description d’un cluster Service Fabric
Hello, Gestionnaire de ressources du Cluster Service Fabric fournit plusieurs mécanismes pour la description d’un cluster. Pendant l’exécution, hello Gestionnaire du Cluster de ressource utilise cette information tooensure haute disponibilité des services hello en cours d’exécution dans un cluster de hello. Lors de l’application de ces règles importants, il tente également de la consommation des ressources toooptimize hello au sein du cluster de hello.

## <a name="key-concepts"></a>Concepts clés
Hello, Gestionnaire de ressources de Cluster prend en charge plusieurs fonctionnalités qui décrivent un cluster :

* Domaines d'erreur
* Domaines de mise à niveau
* Propriétés du nœud
* Capacités du nœud

## <a name="fault-domains"></a>Domaines d'erreur
Un domaine d’erreur est une zone d’échec coordonné. Un seul ordinateur est un domaine d’erreur (dans la mesure où il peut échouer sur son propre pour diverses raisons, à partir de l’alimentation approvisionnement échecs toodrive échecs toobad NIC du microprogramme). Machines toohello connecté même commutateur Ethernet sont dans hello même domaine par défaut, comme sont des ordinateurs qui partagent une seule source d’alimentation ou à un emplacement unique. Dans la mesure où il est naturel pour toooverlap des erreurs matérielles, les domaines d’erreur sont par nature hiérarchiques et sont représentées sous la forme d’URI dans l’infrastructure de Service.

Il est important que les domaines d’erreur sont définies correctement, car le Service Fabric utilise cette toosafely place les services. Service Fabric ne veut pas tooplace services tels que la perte hello d’un domaine d’erreur (causée par une défaillance hello d’un composant) provoque une toogo service vers le bas. Bonjour environnement Azure Service Fabric utilise les informations de domaine d’erreur de hello fournies par hello environnement toocorrectly configurer nœuds hello dans un cluster de hello en votre nom. L’infrastructure de Service autonome, les domaines d’erreur sont définis au moment de hello ce cluster hello est configuré 

> [!WARNING]
> Il est important que les informations de domaine d’erreur hello fourni tooService Fabric est exacte. Par exemple, supposons que les nœuds de votre cluster Service Fabric s’exécutent à l’intérieur de 10 machines virtuelles, s’exécutant sur cinq hôtes physiques. Dans ce cas, même s’il y a 10 ordinateurs virtuels, il y a seulement 5 domaines d’erreur (de niveau supérieur) différents. Partage hello même hôte physique provoque tooshare de machines virtuelles hello même domaine racine par défaut, étant donné que hello expérience des machines virtuelles coordonnée échec en cas de leur hôte physique.  
>
> Étant donné que le Service Fabric attend hello domaine par défaut d’un nœud toochange pas. Autres mécanismes de garantir la haute disponibilité de hello machines virtuelles, telles que [machines virtuelles de la haute disponibilité](https://technet.microsoft.com/en-us/library/cc967323.aspx), utilisez la migration transparente des ordinateurs virtuels à partir d’un ordinateur hôte tooanother. Ces mécanismes de ne pas reconfigurer ou notifier hello code à l’intérieur de hello machine virtuelle en cours d’exécution. À ce titre, ils ne sont **pas prises en charge** en tant qu’environnements d’exécution de clusters Service Fabric. Service Fabric doit être la technologie de haute disponibilité uniquement hello utilisée. La migration dynamique de machines virtuelles, les SAN et autres mécanismes ne sont pas nécessaires. S’ils sont utilisés avec Service Fabric, ces mécanismes _réduisent_ la disponibilité et la fiabilité des applications, car ils introduisent une complexité supplémentaire, ajoutent des sources centralisées de défaillance et utilisent des stratégies de fiabilité et de disponibilité qui sont en conflit avec celles de Service Fabric. 
>
>

Dans le graphique de hello ci-dessous nous couleur toutes les entités hello qui contribuent tooFault domaines et liste que tous les hello différents domaines d’erreur résultant. Dans cet exemple, nous avons des centres de données (« DC »), des racks (« R ») et des panneaux (« B »). En théorie, si chaque panneau conserve plus d’un ordinateur virtuel, il peut être une autre couche Bonjour hiérarchie du domaine d’erreur.

<center>
![Nœuds organisés par domaines d’erreur][Image1]
</center>

Pendant l’exécution, hello Gestionnaire de ressources du Cluster Service Fabric considère que les domaines d’erreur hello dans un cluster de hello et modes de dispositions. Hello réplicas avec état ou sans état instances pour un service donné sont distribués afin qu’ils soient dans des domaines d’erreur. Distribution de service de hello entre domaines d’erreur garantit une disponibilité hello du service de hello n’est pas compromise en cas d’échec d’un domaine d’erreur à n’importe quel niveau de hiérarchie de hello.

Gestionnaire de ressources de Cluster du service Fabric ne tient pas compte le nombre de couches existe dans hello hiérarchie du domaine d’erreur. Toutefois, il essaie de tooensure perte hello de toute une partie de la hiérarchie de hello n’affecte pas les services en cours d’exécution qu’il contient. 

Il est préférable de s’il n’y hello même nombre de nœuds à chaque niveau de profondeur Bonjour hiérarchie du domaine d’erreur. Si hello « arborescence » de domaines d’erreur est déséquilibrée dans votre cluster, il rend plus difficile pour hello toofigure Gestionnaire de ressources de Cluster à l’allocation de meilleures hello de services. Déséquilibré mises en page de domaines d’erreur par cette perte de hello de certains domaines de disponibilité de hello impact de services plus que les autres domaines. Par conséquent, hello Gestionnaire de ressources du Cluster est détruite entre deux objectifs : il veut machines de hello toouse dans ce domaine « heavy » en plaçant des services sur les, et il tooplace des services dans d’autres domaines afin qu’une perte de hello d’un domaine n’entraîne aucun problème. 

À quoi ressemblent des domaines déséquilibrés ? Dans le diagramme hello ci-dessous, nous affichons deux dispositions de cluster différent. Dans le premier exemple de hello, les nœuds de hello sont répartis uniformément entre hello domaines d’erreur. Dans le deuxième exemple de hello, un domaine d’erreur a bien plus de noeuds hello autres domaines d’erreur. 

<center>
![Deux dispositions de cluster différentes][Image2]
</center>

Dans Azure, le choix de hello dont domaine d’erreur contient un nœud est gérée pour vous. Toutefois, en fonction du nombre de hello de nœuds que vous préparez vous pouvez toujours se retrouver avec des domaines d’erreur avec plus de noeuds dans les autres. Par exemple, vous avez cinq domaines d’erreur dans le cluster de hello mais configurez sept nœuds pour un type donné. Dans ce cas, hello tout d’abord deux domaines d’erreur vous retrouver avec plusieurs nœuds. Si vous continuez à toodeploy plus NodeTypes avec seulement quelques instances, hello problème s’aggrave. Pour cette raison, qu'il est recommandé que hello nombre de nœuds dans chaque type de nœud est un multiple de nombre hello de domaines d’erreur.

## <a name="upgrade-domains"></a>Domaines de mise à niveau
Domaines de mise à niveau sont une autre fonctionnalité qui permet de hello du Gestionnaire de ressources du Cluster Service Fabric comprendre disposition hello du cluster de hello. Mise à niveau des domaines définissent des jeux de nœuds qui sont mis à niveau en hello même temps. Mettre à niveau des domaines aide hello Gestionnaire de ressources du Cluster de comprendre et orchestrer les opérations de gestion telles que des mises à niveau.

Les domaines de mise à niveau sont très semblables aux domaines d’erreur, avec cependant quelques différences clés. Tout d’abord, les zones de défaillances matérielles coordonnées définissent les domaines d’erreur. Mise à niveau des domaines relatifs hello d’autre part, sont définis par la stratégie. Vous obtenez toodecide combien vous voulez que, au lieu d’il dictée par l’environnement de hello. Vous pouvez disposer d’autant de domaines mise à niveau que de nœuds. Une autre différence entre les domaines d’erreur et les domaines de mise à niveau est que les domaines de mise à niveau ne sont pas hiérarchiques. En effet, ils s’apparentent plus à une balise simple. 

Hello diagramme suivant illustre trois que domaines de mise à niveau sont réparties sur trois domaines d’erreur. Il montre également un emplacement possible pour trois réplicas différents d’un service avec état, où chaque réplica est attribué à des domaines d’erreur et de mise à niveau différents. Cet emplacement permet la perte de hello d’un domaine d’erreur en milieu de hello d’une mise à niveau de service et toujours avoir une copie de données et le code de hello.  

<center>
![Positionnement avec des domaines d’erreur et de mise à niveau][Image3]
</center>

Il existe des avantages et inconvénients toohaving grand nombre de domaines de mise à niveau. Mettre à niveau vos domaines signifie que chaque étape de mise à niveau hello est plus précis et affecte donc un plus petit nombre de nœuds ou des services. Par conséquent, moins de services ont à la fois, des toomove présentation moins de l’évolution du système de hello. Cela a tendance tooimprove fiabilité, étant donné que moins de service de hello est affectée par n’importe quel problème introduit pendant la mise à niveau hello. Mettre à niveau vos domaines signifie également que vous avez besoin de moins de mémoire tampon disponible autres nœuds toohandle hello l’impact de hello mettre à niveau. Par exemple, si vous avez cinq domaines de mise à niveau, nœuds hello dans chaque sont gère environ 20 % de votre trafic. Si vous devez tootake ce domaine de mise à niveau vers le bas pour une mise à niveau, cette charge doit généralement toogo quelque part. Étant donné que vous avez quatre domaines restants de mise à niveau, chacun doit avoir la salle d’environ 5 % de total du trafic hello. Plusieurs domaines de mise à niveau implique moins mémoire tampon sur les nœuds hello dans un cluster de hello. Par exemple, imaginons que vous disposez de 10 domaines de mise à niveau. Dans ce cas, chaque UD serait uniquement gérer environ 10 % du total du trafic hello. Lorsqu’une mise à niveau parcourt les cluster hello, chaque domaine suffit salle toohave 1.1 % environ de total du trafic hello. Mettre à niveau vos domaines qui vous permettent généralement toorun vos nœuds à une utilisation plus importante, étant donné que vous avez besoin d’une capacité inférieure réservée. Hello même a la valeur true pour les domaines d’erreur.  

inconvénient Hello d’avoir plusieurs domaines de mise à niveau est que les mises à niveau ont tendance à tootake plus de temps. Service Fabric attend pendant une courte période de temps après qu’une mise à niveau de domaine est terminé et effectue des vérifications avant le début tooupgrade hello suivant. Ces délais activer la détection de problèmes introduits par la mise à niveau hello avant le démarrage de la mise à niveau hello. compromis de Hello est acceptable, car il empêche les modifications incorrectes d’affecter trop de service de hello à la fois.

Un nombre insuffisant de domaines de mise à niveau a de nombreux effets secondaires négatifs : quand chaque domaine de mise à niveau est hors service au cours d’une mise à niveau, une grande partie de votre capacité globale n’est pas disponible. Par exemple, si vous avez seulement trois domaines de mise à niveau, vous vous défaites d’environ 1/3 de votre service global ou de votre capacité de cluster à la fois. Grande partie de votre service ayant à la fois vers le bas n’est pas souhaitable puisque vous avez toohave une capacité suffisante dans reste hello de votre charge de travail de cluster toohandle hello. En conservant cette mémoire tampon, dans des conditions normales de fonctionnement, ces nœuds subissent une moindre charge. Cela augmente le coût de hello de votre service en cours d’exécution.

Il n’existe aucune limite réelle toohello nombre total de pannes ou les domaines de mise à niveau dans un environnement, ou des contraintes sur la façon dont elles se chevauchent. Ceci dit, il existe plusieurs modèles courants :

- Correspondance parfaite des domaines d’erreur et des domaines de mise à niveau
- Un domaine de mise à niveau par nœud (instance de système d’exploitation physique ou virtuel)
- Un modèle « agrégés par bandes » ou « matrice », où les domaines d’erreur hello et mettre à niveau forment une matrice avec les ordinateurs généralement en cours d’exécution vers le bas les diagonales hello

<center>
![Dispositions de domaines d’erreur et de mise à niveau][Image4]
</center>

Il existe qu'aucune mieux ne répondre à quels toochoose de disposition, chacun possède certains avantages et inconvénients. Par exemple, modèle de 1FD:1UD hello est tooset simple. Hello 1 domaine de mise à niveau par le modèle de nœud est le plus telles que les personnes sont utilisés pour. Lors des mises à niveau, chaque nœud est mis à jour indépendamment. Cela s’apparente toohow de petits ensembles d’ordinateurs ont été mis à niveau manuellement Bonjour passées. 

modèle le plus courant Hello est la matrice de FD/UD hello, où hello groupes et domaines d’erreur forment une table et les nœuds sont placés dans hello en diagonale. Il s’agit de modèle hello utilisé par défaut dans les clusters Service Fabric dans Azure. Pour les clusters à plusieurs nœuds, tous les éléments se termine ressemble au modèle de matrice dense hello ci-dessus.

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>Contraintes des domaines d’erreur et de mise à niveau, et comportement résultant
Hello, Gestionnaire de ressources du Cluster traite désir hello tookeep un service équilibrée à travers les domaines d’erreur et mettre à niveau en tant que contrainte. Vous trouverez plus d’informations sur les contraintes dans [cet article](service-fabric-cluster-resource-manager-management-integration.md). Hello d’état de contraintes d’erreur et de mettre à niveau un domaine : « pour une partition de service donné il devrait jamais y avoir une différence *supérieur à un* nombre hello des objets de service (instances de service sans état ou des réplicas de service avec état) entre deux domaines. » Cela empêche certains déplacements ou organisations qui enfreignent cette contrainte.

Examinons un exemple. Supposons que nous avons un cluster avec six nœuds, configuré avec cinq domaines d’erreur et cinq de mise à niveau.

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

Maintenant, supposons que nous créons un service en attribuant à TargetReplicaSetSize (ou, pour un service sans état, à InstanceCount) la valeur 5. terres de réplicas Hello sur N1-N5. En fait, N6 n’est jamais utilisé, quel que soit le nombre de services équivalents que vous créez. Mais pourquoi ? Examinons la différence de hello entre la disposition actuelle de hello et ce qui se passerait si vous choisissez N6.

Voici la mise en page hello nous et vos hello nombre total de réplicas par erreur et de domaine de mise à niveau :

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Cette disposition est équilibrée en termes de nœuds par domaine d’erreur et domaine de mise à niveau. Il est également équilibrée en termes de nombre de hello de réplicas par erreur et de domaine de mise à niveau. Chaque domaine possède hello même nombre de nœuds et hello même nombre de réplicas.

À présent, jetons un œil à ce qui se passerait si au lieu de N2, nous avions utilisé N6. Comment les réplicas hello est répartis puis ?

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

Cette disposition ne respecte pas notre définition pourquoi la contrainte de domaine d’erreur. FD0 a deux réplicas, alors que FD1 a zéro, faisant hello différencie FD0 FD1 un total de deux. Hello, Gestionnaire de ressources de Cluster n’autorise pas cette configuration. De même, si nous avions choisi N2 et N6 (au lieu de N1 et N2) nous aurions obtenu :

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Cette disposition est équilibrée du point de vue des domaines d’erreur. Toutefois, il est désormais violation contrainte de mise à niveau domaine hello. Cela est dû au fait que UD0 n’a aucun réplica, alors que UD1 en a deux. Par conséquent, cette disposition est également non valide et ne seront pas prise en hello Gestionnaire de ressources du Cluster. 

## <a name="configuring-fault-and-upgrade-domains"></a>Configuration des domaines d’erreur et de mise à niveau
La définition des domaines d’erreur et de mise à niveau s’effectue automatiquement dans les déploiements Service Fabric hébergés sur Azure. Service Fabric récupère et utilise les informations sur l’environnement à partir d’Azure hello.

Si vous créez votre propre cluster (ou souhaitez toorun une topologie particulière en cours de développement), vous pouvez fournir les informations de domaine d’erreur et de mettre à niveau un domaine hello vous-même. Dans cet exemple, nous définissons un cluster de développement local à neuf nœuds qui s’étend sur trois « centres de données » (chacun avec trois racks). Ce cluster a également trois domaines de mise à niveau répartis sur ces trois centres de données. Un exemple de configuration de hello est ci-dessous : 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

via ClusterConfig.json pour les déploiements autonomes

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> Quand les clusters sont définis via Azure Resource Manager, les domaines d’erreur et les domaines de mise à niveau sont assignés par Azure. Par conséquent, définition hello de vos Types de nœuds et les machines virtuelles identiques dans votre modèle Azure Resource Manager n’inclut pas de domaine par défaut ou domaine de mise à niveau.
>

## <a name="node-properties-and-placement-constraints"></a>Propriétés de nœud et contraintes de placement
Parfois (en fait, la plupart du temps de hello) que vous allez tooensure toowant qui certaines charges de travail s’exécutent uniquement sur certains types de nœuds de cluster de hello. Par exemple, certaines charges de travail peuvent nécessiter des GPU ou des SSD, tandis que d’autres n’en ont pas besoin. Un bon exemple de ciblage des charges de travail tooparticular matériel est presque chaque architecture multicouche très utiles. Certains ordinateurs servent hello frontal ou API servant le côté de l’application hello et sont exposées toohello clients ou hello internet. Des ordinateurs différents, souvent avec les ressources matérielles différentes gérer hello des couches de calcul ou stockage hello. Il s’agit généralement _pas_ directement exposé tooclients ou hello internet. L’infrastructure de service attend qu’il existe des cas où les charges de travail particuliers doivent toorun sur les configurations de matériel spécifique. Par exemple :

* une application multiniveau existante a été « augmentée et déplacée » dans un environnement Service Fabric
* une charge de travail souhaite toorun sur du matériel spécifique pour les performances, l’échelle ou des raisons de sécurité d’isolation
* une charge de travail doit être isolée des autres charges de travail pour des raisons de stratégie ou de consommation de ressources

ces types de configurations, de toosupport Service Fabric a une notion de première classe de balises qui peuvent être appliqués toonodes. Ces balises sont appelés **propriétés de nœud**. **Les contraintes de placement** sont des instructions de hello attachés tooindividual les services que vous sélectionnez pour un ou plusieurs propriétés de nœud. Les contraintes de placement définissent là où les services doivent s’exécuter. ensemble Hello de contraintes est extensible, n’importe quelle paire clé/valeur peut travailler. 

<center>
![Disposition du cluster avec différentes charges de travail][Image5]
</center>

### <a name="built-in-node-properties"></a>Propriétés de nœud intégrées
L’infrastructure de service définit certaines propriétés de nœud par défaut qui peuvent être utilisées automatiquement sans utilisateur hello toodefine les. propriétés par défaut de Hello définies sur chaque nœud sont hello **NodeType** et hello **NodeName**. Par exemple, vous pouvez écrire une contrainte de placement ainsi : `"(NodeType == NodeType03)"`. Nous avons généralement constaté NodeType toobe une des propriétés de hello couramment utilisé. Elle est utile, car elle correspond parfaitement à un type de machine. Chaque type d’ordinateur correspond type tooa de charge de travail dans une application multicouche classique.

<center>
![Contraintes de placement et propriétés de nœud][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>Syntaxe des contraintes de placement et des propriétés de nœud 
valeur de Hello spécifiée dans la propriété de nœud hello peut être une chaîne, bool, ou long signé. instruction Hello au niveau de service de hello est appelée un placement *contrainte* , car il limite où service de hello permettre s’exécuter dans un cluster de hello. contrainte de Hello peut être n’importe quelle instruction booléenne qui fonctionne sur hello différentes propriétés du nœud de cluster de hello. sélecteurs de valide Hello dans ces instructions booléennes sont :

1) des vérifications conditionnelles pour la création d’instructions particulières

| Instruction | Syntaxe |
| --- |:---:|
| "égal à" | "==" |
| "non égal à" | "!=" |
| "supérieur à" | ">" |
| "supérieur ou égal à" | ">=" |
| "inférieur à" | "<" |
| "inférieur ou égal à" | "<=" |

2) instructions booléennes pour les opérations de groupage et logiques

| Instruction | Syntaxe |
| --- |:---:|
| "et" | "&&" |
| "ou" | "&#124;&#124;" |
| "non" | "!" |
| "regrouper en tant qu’instruction unique" | "()" |

Voici quelques exemples d’instructions de contrainte de base.

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

Seuls les nœuds où hello globalement la sélection élective contrainte instruction prend la valeur trop « True » peuvent avoir service hello placé sur celui-ci. Les nœuds sans une propriété définie ne correspondent à aucune contrainte de placement contenant cette propriété.

Supposons que hello suivant nœud propriétés ont été définies pour un type de nœud donné :

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure. 

> [!NOTE]
> Dans le nœud de hello de votre modèle Azure Resource Manager type est généralement paramétré. Il ressemble à « [parameters('vmNodeType1Name')] » plutôt qu’à « NodeType01 ».
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

Vous pouvez créer des *contraintes* de placement de service pour un service comme suit :

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

Si tous les nœuds de NodeType01 sont valides, vous pouvez également sélectionner ce type de nœud avec la contrainte de hello "(NodeType == NodeType01) ».

Une des choses intéressantes hello contraintes de placement d’un service est qu’ils peuvent être mis à jour dynamiquement pendant l’exécution. Par conséquent, si vous le souhaitez, vous pouvez déplacer un service de cluster de hello, ajouter et supprimer, etc.. Prend en charge l’infrastructure de service de s’assurer que le service de hello reste disponible même lorsque ces types de modifications sont apportées.

C# :

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

PowerShell :

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

Les contraintes de placement sont spécifiées pour chaque différente instance de service nommée. Les mises à jour ont toujours lieu hello de (overwrite) ce qui a été spécifié précédemment.

définition de cluster Hello définit les propriétés de hello sur un nœud. La modification des propriétés d’un nœud nécessite une mise à niveau de la configuration du cluster. Les propriétés d’un nœud de la mise à niveau nécessite chaque tooreport toorestart de nœud affecté ses nouvelles propriétés. Ces mises à niveau propagées sont gérées par Service Fabric.

## <a name="describing-and-managing-cluster-resources"></a>Description et gestion des ressources de cluster
Une des principales tâches de n’importe quel orchestrator est toohelp de hello gérer la consommation des ressources de cluster de hello. La gestion des ressources de cluster peut signifier plusieurs choses. En premier lieu, il peut s’agir de veiller à ce que les machines ne soient pas en surcharge. Cela implique de vérifier que les machines n’exécutent pas plus de services qu’elles ne peuvent en gérer. Ensuite, il est équilibrage et optimisation qui est critique toorunning services efficacement. Les offres de service sensibles à compter du ou des performances coûts n’autorise pas certains toobe de nœuds à chaud alors que d’autres sont à froid. Les nœuds à chaud entraîner contention de tooresource et des performances médiocres, des nœuds à froid représentent perdu et les ressources une augmentation des coûts. 

Service Fabric représente les ressources en tant que `Metrics`. Les métriques sont n’importe quelle ressource logique ou physique que vous souhaitez toodescribe tooService l’ensemble fibre optique. Par exemple, « WorkQueueDepth » et « MemoryInMb » sont des métriques. Pour plus d’informations sur les ressources physiques hello qui régit l’infrastructure de Service sur les nœuds, consultez [gouvernance des ressources](service-fabric-resource-governance.md). Pour plus d’informations sur la configuration de métriques personnalisées et sur leur utilisation, consultez [cet article](service-fabric-cluster-resource-manager-metrics.md)

Les mesures sont différentes des contraintes de placement et des propriétés de nœud. Propriétés de nœud sont statiques descripteurs de nœuds hello eux-mêmes. Les métriques décrivent les ressources à la disposition des nœuds et que les services consomment quand ils s’exécutent sur un nœud. Une propriété de nœud peut être « HasSSD » et peut être définie tootrue ou false. quantité Hello d’espace disponible sur ce disque SSD et la quantité est consommée par les services est une mesure telle que « DriveSpaceInMb ». 

Il est important toonote que la même façon que pour les contraintes de placement et les propriétés du nœud, hello Gestionnaire de ressources du Cluster Service Fabric ne comprend pas les noms hello hello métriques moyenne. Les noms des mesures ne sont que des chaînes. Il s’agit d’un unités toodeclare de bonnes pratiques dans le cadre de noms de métrique hello que vous créez lorsque cela peut être ambiguë.

## <a name="capacity"></a>Capacity
Si vous avez désactivé toutes les fonctions d’*équilibrage* des ressources, Cluster Resource Manager de Service Fabric est tout de même en mesure de garantir qu’aucun nœud ne dépasse sa capacité. Il est possible de gérer les dépassements de capacité, sauf si le cluster de hello est saturé ou de la charge de travail hello est supérieure à n’importe quel nœud. La capacité est un autre *contrainte* ce gestionnaire de ressources du Cluster hello utilise toounderstand la quantité d’une ressource, un nœud a. Capacité restante est également suivi pour le cluster de hello dans sa globalité. Capacité de hello et la consommation au niveau de service hello hello sont exprimés en termes de métriques. Par exemple, la métrique de hello peut être « ClientConnections » et un nœud donné peut avoir une capacité de « ClientConnections » de 32 768. Autres nœuds peuvent avoir d’autres limites à certains services en cours d’exécution sur un nœud pouvant dire qu’elle est actuellement utilise des 32256 de métrique de hello « ClientConnections ».

Pendant l’exécution, hello Gestionnaire de ressources de Cluster effectue le suivi de capacité restante dans un cluster de hello et sur les nœuds. Dans l’ordre tootrack hello de capacité Gestionnaire de ressources du Cluster soustrait l’utilisation de chaque service à partir de la capacité du nœud sur lequel s’exécute le service de hello. Avec cette information, hello Gestionnaire de ressources du Cluster Service Fabric peut savoir où tooplace ou déplacez les réplicas afin que les nœuds ne pas dépasser la capacité.

<center>
![Nœuds de cluster et capacité][Image7]
</center>

C# :

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

Vous pouvez voir les capacités définies dans le manifeste du cluster hello :

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure. 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

En règle générale, la charge d’un service évolue de manière dynamique. Supposons que chargement d’un réplica de « ClientConnections » passé de 1024 too2048 mais le nœud hello s’exécutait sur ensuite avait uniquement 512 capacité restante pour cette métrique. À présent, le placement de ce réplica ou de cette instance n’est pas valide, car il n’y a pas suffisamment d’espace sur ce nœud. Hello Gestionnaire de ressources du Cluster a tookick et obtenir le nœud hello dessous de sa capacité. Il réduit la charge sur le nœud de hello sur la capacité en déplaçant un ou plusieurs réplicas de hello ou les instances à partir de ce nœud tooother nœuds. Lorsque vous déplacez des réplicas, hello Gestionnaire de ressources de Cluster tente de coût de hello toominimize les mouvements. Le coût du mouvement est décrite dans [cet article](service-fabric-cluster-resource-manager-movement-cost.md) plus sur hello Gestionnaire de ressources du Cluster de rééquilibrage des stratégies et les règles sont décrites [ici](service-fabric-cluster-resource-manager-metrics.md).

## <a name="cluster-capacity"></a>Capacité de cluster
Comment hello hello de conserver de gestionnaire de ressources du Cluster Service Fabric globale de cluster d’être trop complète ? En fait, du fait du chargement dynamique, il ne peut pas faire grand chose. Services peuvent avoir leur pic de charge indépendamment des actions effectuées par hello Gestionnaire de ressources du Cluster. Par conséquent, votre cluster qui dispose de suffisamment d’espace aujourd’hui pourrait ne pas être suffisamment puissant demain une fois que vous serez devenu célèbre. Ceci dit, il existe certains contrôles sont cuits tooprevent des problèmes. Hello première chose que nous pouvons faire est d’empêcher la création de hello de nouvelles charges de travail qui provoquerait le toobecome de cluster hello complète.

Supposons que vous créez un service sans état et qu’il a une charge associée. Supposons que le service de hello attentive à mesure de « DiskSpaceInMb » hello. Supposons également qu’il s’agit des cours tooconsume cinq unités de « DiskSpaceInMb » pour chaque instance du service de hello. Vous souhaitez toocreate trois instances de service de hello. Parfait ! Afin que signifie que nous devons 15 unités de « DiskSpaceInMb » toobe présente cluster hello afin que nous tooeven être en mesure de toocreate ces instances de service. Hello Gestionnaire de ressources du Cluster calcule en permanence la capacité de hello et la consommation de chaque mesure afin qu’il peut déterminer la capacité restante de hello dans un cluster de hello. Si l’espace est insuffisant, hello Gestionnaire de ressources de Cluster rejette hello créer appel de service.

Étant donné que hello exigence est seulement qu’il être 15 unités disponibles, cet espace peut être affecté à différentes façons. Par exemple, il peut y avoir une unité restante de capacité sur 15 nœuds différents ou trois unités restantes de capacité sur cinq nœuds différents. Si hello Gestionnaire de ressources du Cluster peut réorganiser les choses afin de cinq unités est disponible sur trois nœuds, il place les service hello. Cluster de hello la réorganisation est généralement possible, sauf si le cluster de hello est presque plein ou les services existants hello ne peut pas être consolidées pour une raison quelconque.

## <a name="buffered-capacity"></a>Capacité de mise en mémoire tampon
Capacité de mise en mémoire tampon est une autre fonctionnalité de hello Gestionnaire de ressources du Cluster. Il permet de réservation d’une partie du hello capacité globale du nœud. Cette mémoire tampon de la capacité est tooplace utilisés seuls services au cours des mises à niveau et d’échecs de nœud. La capacité mise en mémoire tampon est spécifiée de manière globale par métrique pour tous les nœuds. valeur Hello choisie pour la capacité de hello réservé est une fonction du nombre de hello de domaines d’erreur et mise à niveau vous avez hello cluster. Un nombre de domaines d’erreur et de mise à niveau plus important signifie que vous pouvez choisir un nombre inférieur pour la capacité de mise en mémoire tampon. Si vous avez plusieurs domaines, attendez-vous plus petites quantités de votre cluster de toobe indisponible pendant les mises à niveau et d’échecs. Spécification de capacité de mise en mémoire tampon convient uniquement si vous avez également la capacité de nœud hello spécifié pour une mesure.

Voici un exemple de comment toospecify mis en mémoire tampon capacité :

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

la création de nouveaux services Hello échoue lorsque le cluster de hello dépassement de la capacité de mise en mémoire tampon pour une mesure. Empêche la création de la nouvelle mémoire tampon services toopreserve hello hello garantit que les échecs et les mises à niveau ne provoquent pas de nœuds toogo surchargés. La capacité de mise en mémoire tampon est facultative mais recommandée dans tout cluster qui définit une capacité pour une mesure.

Hello Gestionnaire du Cluster de ressource expose ces informations de charge. Pour chaque métrique, ces informations incluent : 
  - Hello mis en mémoire tampon de paramètres de capacité
  - capacité totale de Hello
  - consommation actuelle de Hello
  - une indication de l’état équilibré ou non de chaque métrique ;
  - statistiques concernant l’écart type hello
  - nœuds Hello ayant hello plus et le moins de charge  
  
Voici un exemple de cette sortie :

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur le flux architecture et les informations de hello dans hello Gestionnaire de ressources de Cluster, consultez [cet article](service-fabric-cluster-resource-manager-architecture.md)
* Défragmentation des mesures sont charge tooconsolidate monodirectionnelle sur les nœuds au lieu de la propagation de. toolearn comment tooconfigure défragmentation, reportez-vous à la section trop[cet article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Démarrer à partir du début de hello et [obtenir une présentation de toohello Gestionnaire de ressources du Cluster Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
* toofind out sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, consultez l’article de hello sur [équilibrage de charge](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
