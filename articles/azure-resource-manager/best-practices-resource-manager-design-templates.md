---
title: "aaaDesign Azure modèles pour les solutions complexes | Documents Microsoft"
description: "Présente les bonnes pratiques de conception des modèles Azure Resource Manager pour les scénarios complexes"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>Concevoir des modèles pour les modèles Azure Resource Manager lors du déploiement de solutions complexes
À l’aide d’une approche souple, basée sur des modèles Azure Resource Manager, vous pouvez déployer des topologies complexes rapidement et de manière homogène. Vous pouvez adapter ces déploiements facilement en tant que de faire évoluer les offres de base ou tooaccommodate des variantes des scénarios de valeurs hors norme ou des clients.

Cette rubrique fait partie d’un livre blanc plus volumineux. hello tooread complète papier, téléchargez [World classe Azure Resource Manager modèles et éprouvée méthodes conseillées](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

Les modèles contiennent des avantages hello Hello sous-jacent Azure Resource Manager avec capacité d’adaptation hello et la lisibilité de JavaScript Objet Notation (JSON). En utilisant des modèles, vous pouvez :

* déployer des topologies et leurs charges de travail de manière cohérente ;
* gérer l’ensemble de vos ressources dans une application à l’aide de groupes de ressources ;
* Appliquer l’accès en fonction du rôle (RBAC) de contrôle toogrant accès approprié toousers, des groupes et des services.
* Utiliser des tâches de toostreamline associations balises telles que des cumuls de facturation.

Cet article fournit des détails sur les scénarios de consommation, l’architecture et les modèles d’implémentation identifiés au cours de nos sessions de conception et pendant les implémentations de modèle dans le monde réel auprès des clients AzureCAT (Azure Customer Advisory Team). Loin d’être éducation, ces approches des pratiques éprouvées par développement hello des modèles de 12 de technologies de systèmes d’exploitation basés sur Linux de haut hello, y compris : Apache Kafka, Apache Spark, Cloudera, Couchbase, Hortonworks HDP, Enterprise DataStax alimenté par Apache Cassandra, Elasticsearch, Jenkins, MongoDB, PostgreSQL, Redis et Nagios. 

Cet article partage ces toohelp pratiques éprouvées architecte de modèles Azure Resource Manager de classe mondiale.  

Au cours de notre collaboration avec les clients, nous avons identifié plusieurs expériences de consommation de modèles Resource Manager dans les entreprises, chez les intégrateurs de systèmes et les fournisseurs de services cloud. Hello sections suivantes fournissent une vue d’ensemble des scénarios courants et des modèles pour différents types de clients.

## <a name="enterprises-and-system-integrators"></a>Entreprises et intégrateurs de systèmes
Dans les grandes entreprises, il existe généralement deux utilisateurs de modèles Resource Manager : les équipes de développement logiciel internes et les services informatiques. Nous avons constaté que les scénarios de hello pour hello SIs mappent toohello scénarios pour les entreprises, c’est le cas hello mêmes considérations s’appliquent.

### <a name="internal-software-development-teams"></a>Équipes de développement logiciel internes
Si votre équipe développe toosupport du logiciel de votre entreprise, modèles fournissent un moyen simple tooquickly déployer des technologies à utiliser dans les solutions d’entreprise spécifiques. Vous pouvez également utiliser des modèles toorapidly créer des environnements de formation qui permettent les compétences nécessaires de toogain de membres de l’équipe.

Vous pouvez utiliser des modèles en tant que-est ou d’étendre ou de les composer tooaccommodate vos besoins. En utilisant un marquage dans les modèles, vous pouvez fournir un récapitulatif de facturation avec différentes vues, par exemple équipe, projet, individu et formation.

Les entreprises souhaitent souvent un modèle pour un déploiement cohérent d’une solution toocreate des équipes de développement de logiciels. modèle de Hello facilite contraintes afin que certains éléments au sein de cet environnement restent fixes et ne peut pas être substituées. Par exemple, une banque peut nécessiter un tooinclude modèle RBAC, pour un programmeur ne peut pas modifier une solution bancaire compte de stockage personnel tooa toosend données.

### <a name="corporate-it"></a>Services informatiques
Les entreprises disposant de services informatiques utilisent généralement des modèles pour fournir une capacité de cloud et des fonctionnalités hébergées dans le cloud.

#### <a name="cloud-capacity"></a>Capacité de cloud
Une méthode courante pour l’entreprise informatique groupes tooprovide capacité du cloud pour les équipes est « tailles t-shirt », qui sont standard offre des tailles de petite, moyenne et grande. offres de taille de t-shirt Hello peuvent combiner différents types de ressources et les quantités tout en offrant un niveau de normalisation qui rend possible toouse modèles. modèles de Hello offrent des capacités de façon cohérente qui applique les stratégies d’entreprise et utilise des balises tooprovide rétrofacturation tooconsuming organisations.

Par exemple, vous devrez peut-être tooprovide développement, de test ou les environnements de production dans le hello équipes de développement logiciel peuvent déployer leurs solutions. environnement de Hello possède une topologie de réseau prédéfinis et éléments hello équipes de développement logiciel ne peut pas modifier, tels que les règles régissant l’accès toohello publique internet et paquet d’inspection. Vous pourriez également avoir des rôles spécifiques à l’entreprise pour ces environnements avec des droits d’accès distincts pour les environnement hello.

#### <a name="cloud-hosted-capabilities"></a>Fonctionnalités hébergées dans le cloud
Vous pouvez utiliser des modèles toosupport hébergé dans le cloud fonctions, y compris des packages logiciels individuels ou des offres de composites qui sont proposés toointernal des secteurs d’activité. Exemple d’une offre composite : analyse proposée en tant que service (analyse, visualisation et autres technologies), transmise dans une configuration optimisée et connectée dans une topologie de réseau prédéfinie.

Hébergé dans le cloud de fonctionnalités sont affectées par la sécurité de hello et les considérations de rôle établies par la capacité du cloud hello offre sur lequel elles sont construites. Ces fonctionnalités sont proposées telles quelles ou en tant que service administré. Pourquoi ce dernier, où l’accès est limité de rôles sont requis accès tooenable dans l’environnement de hello à des fins de gestion.

## <a name="cloud-service-vendors"></a>Fournisseurs de services cloud
Après avoir parlé des volumes partagés de cluster réduire, nous avons identifié plusieurs approches toodeploy des services pour vos clients et les exigences associées.

### <a name="csv-hosted-offering"></a>Offre hébergée par un fournisseur de services cloud
Si vous hébergez votre offre dans votre abonnement Azure, deux approches d’hébergement sont courantes : un déploiement distinct pour chaque client ou le déploiement d’unités d’échelle qui étayent l’infrastructure partagée utilisée pour tous les clients.

* **Déploiements distincts pour chaque client.** Les déploiements distincts par client nécessitent des topologies fixes de différentes configurations connues. Ces déploiements peuvent avoir différentes tailles de machine virtuelle, différents nombres de nœuds et différentes quantités de stockage associé. Le marquage des déploiements est utilisé pour la facturation des cumuls de chaque client. RBAC peut être activé tooallow clients accès tooaspects de leur environnement cloud.
* **Unités d’échelle dans des environnements partagés mutualisés.** Un modèle peut représenter une unité d’échelle pour des environnements mutualisés. Dans ce cas, hello même infrastructure est toosupport utilisé tous les clients. les déploiements Hello représentent un groupe de ressources qui fournissent un niveau de la capacité hello hébergé offre, telles que le nombre d’utilisateurs et nombre de transactions. Ces unités d’échelle sont augmentées ou réduites en fonction des besoins de la demande.

### <a name="csv-offering-injected-into-customer-subscription"></a>Offre des fournisseurs de services cloud injectée dans l’abonnement client
Vous souhaiterez toodeploy votre logiciel dans les abonnements détenus par les clients. Vous pouvez utiliser des modèles toodeploy distinctes des déploiements dans Azure compte client.

Ces déploiements utilisent RBAC afin de pouvoir mettre à jour et gérer le déploiement hello dans hello du compte client.

### <a name="azure-marketplace"></a>Azure Marketplace
tooadvertise et vendre vos offres via un marketplace, tels que Azure Marketplace, vous pouvez développer des modèles toodeliver types de déploiements qui s’exécutent dans le compte Azure d’un client. Ces déploiements distincts sont décrits en général d’après leur taille (petite, moyenne, grande), le type de produit/public (communauté, développeur, entreprise) ou le type de fonctionnalité (de base, haute disponibilité).  Dans certains cas, ces types permettent toospecify certains attributs du déploiement hello, telles que le type de machine virtuelle ou le nombre de disques.

## <a name="oss-projects"></a>Projets OSS
Au sein des projets open source, les modèles de gestionnaire de ressources permettent à un toodeploy Communauté une solution rapidement grâce à des pratiques éprouvées. Vous pouvez stocker des modèles dans un référentiel GitHub afin de la Communauté de hello peut les modifier au fil du temps. Les utilisateurs déploient ces modèles dans leur propre abonnement Azure.

Hello sections suivantes identifient hello choses tooconsider avant de concevoir votre solution.

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>Identification des éléments externes et internes d’une machine virtuelle
Lorsque vous concevez votre modèle, il est utile toolook exigences hello en termes de ce qui est externe et interne hello virtual machines virtuelles :

* Extérieur signifie hello des machines virtuelles et autres ressources de votre déploiement, telles que la topologie réseau hello, le balisage, les références toohello certificats/clés secrètes et le contrôle d’accès en fonction du rôle. Toutes ces ressources font partie de votre modèle.
* Configuration d’état à l’intérieur signifie hello logiciels installés et globalement souhaité. Les autres mécanismes, tels que les extensions de machine virtuelle ou les scripts sont utilisés en tout ou partie. Ces mécanismes peuvent être identifiés et exécutés par le modèle de hello mais ne sont pas qu’il contient.

Des exemples courants d’activités que vous le feriez « à l’intérieur de la zone de hello » sont les suivants :  

* Installer ou supprimer des fonctionnalités et des rôles de serveur
* Installer et configurer le logiciel au niveau de cluster ou nœud hello
* Déployer des sites web sur un serveur web
* Déployer des schémas de base de données
* Gérer le Registre ou d’autres types de paramètre de configuration
* Gérer les fichiers et répertoires
* Démarrer, arrêter et gérer les processus et services
* Gérer les groupes locaux et comptes d’utilisateur
* Installer et gérer les packages (.msi, .exe, yum, etc.)
* Gérer les variables d’environnement
* Exécuter les scripts natifs (Windows PowerShell, bash, etc.)

### <a name="desired-state-configuration-dsc"></a>Configuration d’état souhaité (DSC)
Vous réfléchissez à l’état interne de hello de vos machines virtuelles au-delà de déploiement, vous souhaitez toomake que ce déploiement ne » dérive » à partir de la configuration hello que vous avez définie et activée dans le contrôle de code source. Cette approche garantit vos développeurs ou personnel chargé des opérations ne faites pas environnement tooan de modifications ad hoc qui ne sont pas approuvés, testé ou enregistrées dans le contrôle de code source. Ce contrôle est important, car les modifications manuelles hello ne se trouvent pas dans le contrôle de code source. Ils sont également pas partie du déploiement standard de hello et aura un impact sur les futurs déploiements automatisés de logiciels de hello.

Outre pour vos employés internes, la configuration d’état souhaité est également importante en matière de sécurité. Les pirates informatiques essaient régulièrement toocompromise et exploitent les systèmes logiciels. Cas de réussite, il est fichiers tooinstall communs et état hello d’un système compromis. À l’aide de la configuration de l’état souhaité, vous pouvez identifier les deltas entre hello souhaitée et l’état réel et restaurer une configuration connue.

Il existe des extensions de ressource hello plus populaires mécanismes pour DSC - PowerShell DSC, Chef et Puppet. Chacune de ces extensions de déploiement état initial de hello de votre machine virtuelle et également être utilisé toomake vraiment hello souhaité de l’état est maintenu.

## <a name="common-template-scopes"></a>Étendues courantes de modèle
Nous avons vu que trois étendues clés de modèle de solution émergent. Ces trois étendues de capacité, fonctionnalité et solution de bout en bout – sont décrits dans les sections suivantes de hello.

### <a name="capacity-scope"></a>Étendue de capacité
Une étendue de la capacité fournit un ensemble de ressources dans une topologie standard qui est préconfigurée toobe conformément aux réglementations et stratégies. exemple Hello le plus courant consiste à déployer un environnement de développement standard dans un scénario informatique d’entreprise ou SI.

### <a name="capability-scope"></a>Étendue de fonctionnalité
Une étendue de fonctionnalité est axée sur le déploiement et la configuration d’une topologie pour une technologie donnée. Les scénarios courants incluent les technologies SQL Server, Cassandra et Hadoop.

### <a name="end-to-end-solution-scope"></a>Étendue de solution de bout en bout
Une portée de bout en bout pour la Solution est ciblée au-delà d’une fonctionnalité unique et à la place le focus sur une solution globale tooend fin constitué de plusieurs fonctionnalités.  

Un modèle avec étendue de solution se manifeste comme un ensemble d’un ou plusieurs modèles à étendue de fonctionnalité avec des ressources, une logique et un état souhaité propres à la solution. Un exemple d’un modèle de solution de portée est un modèle de solution fin tooend données pipeline. modèle de Hello peut combiner topologie spécifique de la solution et l’état avec plusieurs modèles de solution de capacité étendue comme Kafka, Storm et Hadoop.

## <a name="choosing-free-form-vs-known-configurations"></a>Choix de configurations ouvertes et connues
Vous pouvez penser initialement un modèle doit fournir aux consommateurs une grande flexibilité de hello, mais plusieurs considérations affectent le choix entre hello toouse des configurations de forme libre et configurations connues. Cette section identifie les spécifications du client clé hello et les considérations techniques en forme approche hello partagé dans ce document.

### <a name="free-form-configurations"></a>Configurations ouvertes
Sur la surface de hello, les configurations de forme libre son idéale. Ils vous tooselect un type de machine virtuelle et fournir un nombre arbitraire de nœuds et les disques pour les nœuds associés, et faire en tant que modèle tooa de paramètres. Toutefois, cette approche n’est pas idéale pour certains scénarios.

Dans [tailles des machines virtuelles](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), types de machine virtuelle hello et tailles disponibles sont identifiés et chaque nombre hello de durabilité disques (2, 4, 8, 16, 32) qui peut être attaché. Chaque disque attaché fournit 500 E/S par seconde, et plusieurs disques peuvent être regroupés pour obtenir un multiplicateur de ce nombre d’E/S par seconde. Par exemple, 16 disques peut être mis en pool tooprovide IOPS 8 000. Le regroupement s’effectue avec la configuration dans le système d’exploitation de hello, à l’aide des espaces de stockage de Microsoft Windows ou une baie redondante de disques (RAID) dans Linux.

Une configuration de forme libre permet la sélection de hello plusieurs instances de machine virtuelle, VM différents types et tailles pour ces instances, des disques différents pour hello type d’ordinateurs virtuels, et un ou plusieurs scripts de contenu de machine virtuelle tooconfigure hello.

Il est courant qu’un déploiement comprenne plusieurs types de nœud, tels que les nœuds principaux et de données. Cette flexibilité est donc souvent proposée pour tous les types de nœud.

Lorsque vous commencez clusters toodeploy d’une importance, commencer toowork avec ces scénarios complexes. Si vous déployez un cluster Hadoop, par exemple, avec 8 nœuds principaux et des nœuds de données de 200 et bureaux 4 disques sur chaque nœud principal et les bureaux 16 disques attachés par nœud de données, vous devez 208 machines virtuelles et 3,232 disques toomanage.

Un compte de stockage accélèrera demandes ci-dessus que son identifié de 20 000 transactions par seconde limiter, donc vous devez examiner le partitionnement de compte de stockage et utiliser des calculs nombre approprié de hello toodetermine de stockage des comptes tooaccommodate cette topologie. Étant donné la multitude de hello de combinaisons prises en charge par l’approche de forme libre hello, des calculs dynamiques sont requis toodetermine hello partitionnement appropriée. Hello langue de modèle de gestionnaire de ressources Azure ne fournit pas actuellement les fonctions mathématiques, vous devez effectuer ces calculs dans le code, la génération d’un modèle unique, codé en dur avec les détails appropriés hello.

Dans l’informatique d’entreprise et les scénarios SI, une personne doit maintenir des modèles de hello et prend en charge les topologies de hello déployé pour une ou plusieurs organisations. Cette surcharge supplémentaire, à savoir différentes configurations et différents modèles pour chaque client, est loin d’être souhaitable.

Vous pouvez utiliser ces environnements toodeploy de modèles dans un abonnement Azure de votre client, mais les équipes informatiques d’entreprise et volumes partagés de cluster en général les déployer dans leurs propres abonnements, à l’aide d’un toobill de fonction rétrofacturation leurs clients. Dans ces scénarios, hello vise capacité toodeploy pour plusieurs clients sur un pool d’abonnements et de conserver les déploiements denses dans hello abonnements toominimize abonnement prolifération : autrement dit, plus toomanage d’abonnements. Avec des tailles de déploiement véritablement dynamique, pour parvenir à ce type de densité requiert une planification et développement supplémentaires pour le travail de génération de modèles automatique pour le compte d’organisation de hello.

En outre, vous ne peut pas créer des abonnements via un appel d’API mais vous devez le faire manuellement via le portail de hello. L’augmentation de nombre de hello d’abonnements, toute la prolifération des abonnement résultant nécessite une intervention humaine, elle ne peut pas être automatisée. Avec la variabilité bien dans des tailles de hello de déploiements, vous devez toopre-configurer un nombre d’abonnements manuellement tooensure les abonnements sont disponibles.

Compte tenu de tous ces facteurs, une configuration réellement ouverte est moins intéressante que de prime abord.

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>Connu configurations : hello approche de taille de t-shirt
Plutôt qu’offrent un modèle qui fournit une flexibilité totale et les variations d’innombrables, dans notre expérience est courant tooprovide hello capacité tooselect connu des configurations : en effet, des tailles de t-shirt standard tels que de bac à sable, petite, moyenne et grande. Les autres exemples de taille standard sont des offres de produits, telles que l’édition Community ou Enterprise.  Dans d’autres cas, il peut s’agir de configurations d’une technologie propres à une charge de travail, par exemple MapReduce ou sans SQL.

Nombre d’entreprises informatiques, de fournisseurs OSS et d’intégrateurs de systèmes proposent leurs offres aujourd’hui de cette façon dans des environnements locaux, virtualisés (entreprises) ou en tant qu’offres SaaS (fournisseurs de services cloud et de systèmes d’exploitation).

Cette approche fournit des configurations correctes, connues de différentes tailles qui sont préconfigurées pour les clients. Sans des configurations connues, clients finaux doivent déterminer la taille de cluster sur leurs propres, tenir compte des contraintes de ressources de plateforme et faire mathématiques tooidentify hello résultant partitionnement des comptes de stockage et d’autres ressources (échéance toocluster taille et de ressources contraintes). Connu configurations activer une taille de t-shirt droite clients tooeasily sélectionnez hello, autrement dit, un déploiement donné. En outre toomaking une meilleure expérience client de hello, un petit nombre de configurations connues est toosupport plus facile et peut vous aider à assurer un haut niveau de densité.

Une approche de configuration connue axée sur des tailles standard peut également proposer un nombre de nœuds variable par taille. Par exemple, une petite taille peut comprendre 3 à 10 nœuds.  taille de t-shirt Hello serait conçue tooaccommodate des nœuds de too10 et fournir des sélections de forme libre consommateur hello capacité toomake taille maximale de toohello identifié hello.  

Une taille de t-shirt selon le type de charge de travail, peut être plus de forme libre dans la nature en termes de nombre hello de nœuds qui peuvent être déployées mais a taille de nœud distinct de la charge de travail et la configuration des logiciels de hello sur le nœud de hello.

Taille de T-shirt basé sur les offres de produits, telles que la Communauté ou entreprise, peuvent avoir des types de ressources distinct et le nombre maximal de nœuds qui peuvent être déployées, liée généralement toolicensing considérations ou la disponibilité des fonctionnalités entre les offres hello.

Vous pouvez également utiliser des clients avec les variantes uniques à l’aide des modèles JSON hello. Lorsque vous traitez des valeurs hors norme, vous pouvez incorporer la planification appropriée hello et les considérations de développement, la prise en charge et d’évaluation des coûts.

En fonction des scénarios de consommation de modèle client hello et des besoins identifiés au début de hello de ce document, nous avons déterminé un modèle pour la décomposition du modèle.

## <a name="capacity-and-capability-scoped-solution-templates"></a>Modèles de solution avec étendue de capacité et de fonctionnalité
Décomposition fournit un développement tootemplate approche modulaire qui prend en charge la réutilisation, d’extensibilité, de test et les outils. Cette section fournit des détails sur comment une approche de décomposition peut être appliqués tootemplates avec une portée de capacité ou la fonctionnalité.

Dans cette approche, un modèle principal reçoit des valeurs de paramètre à partir d’un consommateur de modèle, puis lie tooseveral des types de modèles et de scripts en aval, comme indiqué ci-dessous. Paramètres, les variables statiques et les variables générées sont des valeurs de tooprovide utilisés et les modèles hello lié.

![Paramètres de modèle](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**Les paramètres sont transmis les modèles principal tooa puis toolinked modèles**

Hello suivant de focus des sections de types hello de modèles et de scripts est décomposé selon un modèle unique. les sections de Hello présentent des approches permettant de passer des informations d’état entre les modèles hello. Chaque type de script de modèle et hello dans l’image de hello décrits ainsi que des exemples. Pour obtenir un exemple contextuel, consultez la rubrique « Synthèse générale : Exemple d’implémentation » plus loin dans ce document.

### <a name="template-metadata"></a>Métadonnées de modèle
Métadonnées du modèle (fichier de metadata.json hello) contient des paires clé/valeur qui décrivent un modèle au format JSON, qui peut être lu par l’homme et les systèmes logiciels.

![Métadonnées de modèle](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**Les métadonnées de modèle sont décrite dans le fichier de metadata.json hello**

Agents de logiciels peuvent récupérer le fichier de metadata.json hello et publier des informations hello et un modèle de toohello de lien dans une page web ou le répertoire. Les éléments incluent *itemDisplayName*, *description*, *summary*, *githubUsername* et *dateUpdated*.

Un exemple de fichier est présenté ci-dessous dans son intégralité.

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>Modèle principal
les modèles principal Hello reçoit des paramètres d’un utilisateur utilise des variables objet complexe toopopulate plus d’informations et exécute les modèles hello lié.

![Modèle principal](./media/best-practices-resource-manager-design-templates/main-template.png)

**les modèles principal Hello reçoit des paramètres d’un utilisateur**

Un paramètre qui est fourni est un type de configuration connue également connu sous les paramètres de taille de t-shirt hello en raison de ses valeurs standardisés tels que de petite, moyenne ou grande. Dans la pratique, vous pouvez utiliser ce paramètre de plusieurs façons. Pour plus d’informations, consultez la rubrique « Modèles de ressource de configuration connue », plus loin dans ce document.

Certaines ressources sont déployées, quelle que soit la configuration connue de hello spécifiée par un paramètre utilisateur. Ces ressources sont configurés à l’aide d’un modèle de ressource partagée unique et sont partagés par les autres modèles, modèle de ressource partagée hello est exécuté en premier.

Certaines ressources sont déployées si vous le souhaitez, quelle que soit la configuration connue de hello spécifié.

### <a name="shared-resources-template"></a>Modèle de ressource partagé
Ce modèle propose des ressources communes à toutes les configurations connues. Il contient le réseau virtuel de hello, haute disponibilité et d’autres ressources qui sont requis, quelle que soit le modèle de configuration connues hello qui est déployé.

![Ressources de modèle](./media/best-practices-resource-manager-design-templates/template-resources.png)

**Modèle de ressource partagé**

Les noms de ressources, telles que nom de réseau virtuel hello sont basées sur les modèles principal hello. Vous pouvez les spécifier comme une variable dans le modèle ou les recevoir en tant que paramètre à partir de l’utilisateur de hello, comme requis par votre organisation.

### <a name="optional-resources-template"></a>Modèle de ressource facultatif
modèle de ressources facultative Hello contient des ressources qui sont déployés par programme en fonction de valeur hello d’une variable ou un paramètre.

![Ressources facultatives](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**Modèle de ressource facultatif**

Par exemple, vous pouvez utiliser un tooconfigure de modèle de ressources facultative un jumpbox qui permet un accès indirect des environnement de tooa déployé à partir de hello Internet public. Vous devez utiliser un tooidentify paramètre ou une variable si hello jumpbox doit être activée et hello *concat* toobuild hello cible nom pour le modèle de hello, de la fonction comme *jumpbox_enabled.json*. Liaison de modèle utiliserait hello résultant tooinstall variable hello jumpbox.

Vous pouvez lier le modèle de ressources facultative hello à partir de plusieurs emplacements :

* Lorsque tooevery applicable, déploiement, créez un lien contrôlée par le paramètre de modèle de ressources partagées hello.
* Lors de la tooselect applicable connu des configurations, par exemple, installer uniquement sur les déploiements à grandes échelle : créer un lien contrôlée par le paramètre ou variable-driven à partir du modèle de configuration connues hello.

Si une ressource donnée est facultative ne peut pas déterminée par les consommateurs de modèle hello mais plutôt par le fournisseur de modèle hello. Par exemple, vous devrez peut-être toosatisfy une spécification de produit particulière ou un module complémentaire de produit (commun pour les volumes partagés de cluster) ou des stratégies de tooenforce (pour les SIs et de l’informatique d’entreprise groupes). Dans ce cas, vous pouvez utiliser une variable tooidentify si la ressource de hello doit être déployée.

### <a name="known-configuration-resources-template"></a>Modèle de ressource de configuration connue
Dans le modèle principal de hello, un paramètre peut être exposé tooallow hello modèle consommateur toospecify un toodeploy souhaitée configuration connue. Souvent, cette configuration connue utilise une approche de taille standard, avec un ensemble de tailles de configuration fixes, telles que bac à sable, petite, moyenne et grande.

![Ressources de configuration connue](./media/best-practices-resource-manager-design-templates/known-config.png)

**Modèle de ressource de configuration connue**

approche de taille de t-shirt Hello est couramment utilisé, mais les paramètres hello peuvent représenter n’importe quel jeu de configurations connues. Par exemple, vous pouvez spécifier un ensemble d’environnements pour une application d’entreprise comme Développement, Test et Production. Vous pouvez l’utiliser pour un toorepresent de service de cloud différents à l’échelle unités, les versions de produit ou configurations de produits tels que la Communauté, Developer ou Enterprise.

Comme avec le modèle de ressource partagée hello, les variables sont passées modèle de configurations connues toohello à partir d’un :

* Un utilisateur final, autrement dit, les paramètres de hello envoyé toohello les modèles principal.
* Une organisation : hello, autrement dit, les variables dans les modèles principal hello qui représentent des exigences internes ou des stratégies.

### <a name="member-resources-template"></a>Modèle de ressource de membre
Dans une configuration connue, un ou plusieurs types de nœud de membre sont souvent inclus. Par exemple, avec Hadoop, vous disposez de nœuds principaux et de nœuds de données. Si vous installez MongoDB, vous disposez de nœuds de données et d’un arbitre. Si vous déployez DataStax, vous disposez de nœuds de données et d’une machine virtuelle avec OpsCenter installé.

![Ressources de membres](./media/best-practices-resource-manager-design-templates/member-resources.png)

**Modèle de ressource de membre**

Chaque type de nœud peut avoir différentes tailles de machines virtuelles, les numéros de disques attachés, les scripts tooinstall et configurer les nœuds de hello, configurations de port pour les machines virtuelles de hello, nombre d’instances et d’autres détails. Pour chaque type de nœud obtient son propre modèle de ressource de membre, qui contient hello détails pour le déploiement et configuration d’une infrastructure ainsi que l’exécution de scripts toodeploy et configurer les logiciels au sein de la machine virtuelle de hello.

En général, pour les machines virtuelles, deux types de script sont utilisés : les scripts réutilisables à grande échelle et les scripts personnalisés.

### <a name="widely-reusable-scripts"></a>Scripts réutilisables à grande échelle
Les scripts réutilisables à grande échelle peuvent être utilisés dans plusieurs types de modèle. Un des exemples de meilleures hello de ces scripts réutilisables largement définit RAID sur les disques toopool Linux et obtenir un plus grand nombre d’IOPS. Quel que soit le logiciel hello en cours d’installation Bonjour machine virtuelle, ce script offre la réutilisation des pratiques éprouvées pour les scénarios courants.

![Scripts réutilisables](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**Les modèles de ressource de membre peuvent appeler des scripts réutilisables à grande échelle**

### <a name="custom-scripts"></a>Scripts personnalisés
Les modèles appellent généralement un ou plusieurs scripts qui installent et configurent des logiciels sur les machines virtuelles. Cette approche est couramment rencontrée dans les topologies de grande taille dans lesquelles plusieurs instances d’un ou plusieurs types de membre sont déployées. Un script d’installation pouvant être exécuté en parallèle est lancé pour chaque machine virtuelle, suivi d’un script de configuration qui est appelé à l’issue du déploiement de toutes les machines virtuelles (ou de toutes les machines virtuelles d’un type de membre donné).

![Scripts personnalisés](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**Les modèles de ressource de membre peuvent appeler des scripts pour un objectif spécifique, par exemple la configuration d’une machine virtuelle**

## <a name="capability-scoped-solution-template-example---redis"></a>Exemple de modèle de solution avec étendue de capacité : Redis
tooshow comment une implémentation fonctionnent, examinons un exemple pratique de la création d’un modèle qui facilite le déploiement de hello et la configuration de Redis dans des tailles de t-shirt standard.  

Pour le déploiement de hello, il existe un ensemble de ressources partagées (réseau virtuel, le compte de stockage, haute disponibilité) et une ressource facultative (jumpbox). Il existe plusieurs configurations connues représentées par des tailles standard (petite, moyenne, grande), mais chacune dispose d’un type de nœud unique. Il existe également deux scripts propres aux besoins (installation et configuration).

### <a name="creating-hello-template-files"></a>Création des fichiers de modèle hello
Vous allez créer un modèle principal nommé azuredeploy.json.

Vous allez créer un modèle de ressource partagé, nommé shared-resources.json.

Vous créez un déploiement de hello tooenable facultatif modèle de ressource d’un jumpbox, nommé jumpbox_enabled.json

Comme Redis utilise simplement un type de nœud unique, vous allez créer un modèle de ressource de membre unique, nommé node-resources.json.

Avec Redis, vous souhaitez tooinstall chaque nœud, puis mettez en cluster de hello.  Vous avez des scripts tooaccommodate hello installation et configuré, redis-cluster-install.sh et redis-cluster-setup.sh.

### <a name="linking-hello-templates"></a>Liaison de modèles de hello
Utilisant la liaison de modèle, les modèles principal hello lie modèle toohello des ressources partagées, qui établit le réseau virtuel de hello.

Logique est ajoutée au sein de hello modèle principal tooenable les consommateurs de hello modèle toospecify si un jumpbox doit être déployé. Un *activé* valeur hello *EnableJumpbox* paramètre indique que le client hello veut toodeploy un jumpbox. Lorsque cette valeur est fournie, le modèle de hello concatène *_enabled du* comme nom de modèle de base tooa de suffixe pour prendre en charge jumpbox hello.

les modèles principal Hello appliquent hello *grand* valeur du paramètre comme un nom de modèle de base de tooa de suffixe pour la taille de t-shirt, puis utilise cette valeur dans une liaison de modèle out trop*technology_on_os_large.json*.

topologie de Hello ressemblerait à cette illustration.

![Modèle Redis](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Structure d’un modèle Redis**

### <a name="configuring-state"></a>Configuration d’un état
Pour les nœuds hello dans un cluster de hello, il existe deux étapes état de hello tooconfiguring, représentés par des Scripts spécifiques objectif.  « redis-cluster install.sh » installe Redis et « redis-cluster-setup.sh » configure le cluster de hello.

### <a name="supporting-different-size-deployments"></a>Prise en charge des déploiements de taille différente
Dans des variables, modèle de taille de t-shirt hello Spécifie le nombre de hello de nœuds de chaque type toodeploy pour hello de taille spécifiée (*grand*). Il déploie ensuite ce nombre d’instances de machine virtuelle à l’aide de boucles de ressource, en fournissant des noms uniques tooresources en ajoutant un nom de nœud avec un numéro de séquence numérique de *copyIndex()*. Il le fait ces étapes pour les deux machines virtuelles de zone à chaud, tel que défini dans le modèle de nom hello t-shirt

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>Modèles de décomposition et avec étendue de solution de bout en bout
Un modèle de solution avec étendue de solution de bout en bout est destiné à fournir une solution de bout en bout.  Cette approche repose généralement sur la composition de plusieurs modèles avec étendue de fonctionnalité avec des ressources supplémentaires, une logique et un état.

Mise en évidence dans l’image hello ci-dessous, hello même modèle utilisé pour les modèles de la fonctionnalité d’une étendue est étendu pour les modèles avec une portée de bout en bout pour la Solution.

Un modèle de ressources partagées et les modèles de ressources facultative servent hello même fonction que dans la capacité de hello et des fonctionnalités des approches de modèle d’une étendue, mais sont limités pour les solutions tooend hello.

Comme solution de tooend de fin d’une étendue modèles peuvent avoir également généralement des tailles de t-shirt, modèle de ressources de Configuration connu hello reflète ce qui est requis pour une configuration donnée connue de solution de hello.

Hello connu un modèle de ressources de Configuration des liens tooone ou plus grande capacité de portée des modèles de solution qui sont pertinentes toohello tooend solutions ainsi que hello des modèles de ressources de membres qui sont requis pour une solution complète tooend hello.

Taille de t-shirt hello de solution de hello peut-être être différente de modèle d’étendue de la fonctionnalité hello individuels, les variables dans hello connu un modèle de ressources de Configuration sont hello tooprovide utilisé les valeurs appropriées pour la solution de capacité en aval d’une étendue modèles toodeploy hello t-shirt taille appropriée.

![Bout en bout](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**modèle de Hello utilisé pour la capacité ou une étendue de la fonctionnalité des modèles de solution peuvent être facilement étendues pour les étendues de modèle de solution tooend fin**

## <a name="preparing-templates-for-hello-marketplace"></a>Préparation des modèles hello Marketplace
Hello précédant approche facilement prend en charge les scénarios où les entreprises, SIs et volumes partagés de cluster tooeither de que vous souhaitez déployer des modèles de hello eux-mêmes ou activer leur toodeploy de clients sur leur propre.

Un autre scénario consiste à déployer un modèle via le marketplace de hello.  Cette approche de décomposition fonctionne pour marketplace hello, avec quelques changements mineurs.

Comme mentionné précédemment, modèles peuvent être des types de déploiement distinct de toooffer utilisé pour la vente dans marketplace de hello. Les types de déploiement distinct peuvent être des tailles standard (petite, moyenne, grande), le type de produit/public (communauté, développeur, entreprise) ou le type de fonctionnalité (de base, haute disponibilité).

Comme illustré ci-dessous, hello existant fin tooend solution ou modèles étendues peuvent être facilement utilisées toolist hello différentes configurations connues dans marketplace de hello.

Hello paramètres toohello principal modèle sont tout d’abord modifié tooremove hello entrant paramètre nommé tshirtSize.

Alors que les types de déploiement distinct hello mappent toohello connu un modèle de ressources de Configuration, ils doivent également des ressources communes hello et configuration trouvée dans hello modèle de ressources partagées et potentiellement celles figurant dans les modèles de ressources facultative.

Si vous souhaitez toopublish votre marketplace toohello de modèle, vous établissez des copies distinctes de votre modèle principal qui remplace hello précédemment disponible paramètre entrant de tshirtSize tooa variable incorporé dans le modèle de hello.

![Marketplace](./media/best-practices-resource-manager-design-templates/marketplace.png)

**Adaptation d’une solution de modèle pour le marketplace de hello d’une étendue**

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur le partage d’état vers et depuis des modèles, consultez [partager l’état sur les modèles Azure Resource Manager](best-practices-resource-manager-state.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

