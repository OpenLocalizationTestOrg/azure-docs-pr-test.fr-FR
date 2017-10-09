---
title: "aaaSecurity analyse dans le centre de sécurité Azure | Documents Microsoft"
description: "Cet article vous aide à vous tooget démarré avec l’analyse des fonctionnalités dans le centre de sécurité Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Surveillance de l’intégrité de la sécurité dans le Centre de sécurité Azure
Cet article vous permet d’utiliser hello capacités d’analyse dans le centre de sécurité Azure toomonitor respect des stratégies.

## <a name="what-is-security-health-monitoring"></a>Qu’est-ce que la surveillance de l’intégrité de la sécurité ?
Nous pensons que souvent de l’analyse en tant que la surveillance et d’attendre un événement toooccur afin que nous pouvons réagir toohello situation. Surveillance de la sécurité fait référence toohaving une stratégie proactive des audits de vos systèmes de tooidentify de ressources qui ne répondent pas aux normes de l’organisation ou les meilleures pratiques.

## <a name="monitoring-security-health"></a>Surveillance de l’intégrité de la sécurité
Après avoir activé [des stratégies de sécurité](security-center-policies.md) pour les ressources d’un abonnement, le centre de sécurité analyse la sécurité de hello des vulnérabilités potentielles tooidentify ressources. Les informations sur la configuration du réseau sont instantanément disponibles. Peut prendre une heure ou plus pour plus d’informations sur la configuration de l’ordinateur virtuel, telles que la sécurité mise à jour le statut et configuration de système d’exploitation, toobecome disponible. Vous pouvez afficher l’état de la sécurité de vos ressources et les problèmes hello Bonjour **prévention** section. Vous pouvez également afficher une liste de ces problèmes sur hello **recommandations** vignette.

Pour plus d’informations sur la façon tooapply recommandations, lire [mise en œuvre des recommandations de sécurité dans le centre de sécurité Azure](security-center-recommendations.md).

Sous hello **prévention** section, vous pouvez surveiller état hello de la sécurité de vos ressources. Dans l’exemple suivant de hello, vous pouvez voir que dans la vignette de chaque ressource (calcul, mise en réseau, stockage & données et l’Application) a le nombre total de hello de problèmes qui ont été identifiées.

![Mosaïque Intégrité de la sécurité des ressources](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>Suivre les calculs
Lorsque vous cliquez sur **de calcul** vignette, hello **de calcul** panneau qui s’ouvre affiche trois onglets :

- **Vue d’ensemble** : recommandations relatives aux machines virtuelles et à la surveillance.
- **Machines virtuelles** : liste de toutes les machines virtuelles et informations relatives à l’intégrité de leur sécurité.
- **Services cloud** : liste de tous les rôles web et de travail contrôlés par Security Center.

![Mise à jour système manquante par machine virtuelle](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

Dans chaque onglet, vous pouvez avoir plusieurs sections, et dans chaque section, vous pouvez sélectionner une option individuelle de toosee plus de détails sur hello recommandé étapes tooaddress ce problème particulier. 

#### <a name="monitoring-recommendations"></a>Recommandations concernant la surveillance
Cette section indique le nombre total de hello d’ordinateurs virtuels qui ont été initialisés pour la collecte de données et leur état actuel. Après la collecte de données initialisée, tous les ordinateurs virtuels, il sera prêt tooreceive des stratégies de sécurité Centre de sécurité. Lorsque vous cliquez sur cette entrée, hello **Agent de machine virtuelle est manquant ou ne répond ne pas** panneau s’ouvre. 

![Mise à jour système manquante par machine virtuelle](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Recommandations pour machines virtuelles
Cette section contient une série de [recommandations pour chaque machine virtuelle](security-center-virtual-machine-recommendations.md) surveillée par Azure Security Center. Hello première colonne répertorie les recommandation hello. deuxième colonne de Hello montre le nombre total de hello d’ordinateurs virtuels qui sont affectés par cette recommandation. Hello troisième colonne affiche la gravité hello du problème de hello comme illustré dans hello suivant capture d’écran.

![Recommandations pour machines virtuelles](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Seules les machines virtuelles qui ont au moins un point de terminaison public sont affichés dans hello **mise en réseau de contrôle d’intégrité** panneau Bonjour **topologie de réseau** liste.
>
>

Chaque recommandation dispose d’un ensemble d’actions pouvant être effectuées après avoir cliqué dessus. Par exemple, si vous cliquez sur **mises à jour système manquantes**, hello **mises à jour système manquantes** panneau s’ouvre. Il répertorie les ordinateurs virtuels hello qui sont des correctifs manquants et hello gravité de la mise à jour manquante de hello, comme indiqué dans les éléments suivants de hello capture d’écran.

![Mise à jour système manquante pour les machines virtuelles](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

Hello **mises à jour système manquantes** panneau affiche un tableau avec hello informations suivantes :

* **MACHINE virtuelle**: nom hello de machine virtuelle hello auquel il manque des mises à jour.
* **Mises à jour système**: hello du nombre de mises à jour système manquantes.
* **DERNIÈRE analyse**: hello lecture que le centre de sécurité dernier ordinateur virtuel de hello pour les mises à jour.
* **ÉTAT**: hello l’état actuel de la recommandation de hello :
  * **Ouvrez**: recommandation de hello n’a pas encore été traitée.
  * **En cours d’exécution**: recommandation de hello est en train de ressources de toothose appliqués et aucune action n’est requise par vous.
  * **Résolu**: recommandation de hello était déjà terminée. (Lorsque hello est résolu, entrée de hello est grisée).
* **GRAVITÉ**: décrit la gravité hello de cette recommandation particulier :
  * **Élevée** : existence d’une vulnérabilité sur une ressource importante (application, machine virtuelle, groupe de sécurité réseau). Le problème doit être analysé.
  * **Support**: Non critiques ou d’autres étapes sont requise toocomplete un processus ou éliminer une vulnérabilité.
  * **Faible**: existence d’une vulnérabilité devant être prise en compte, mais qui ne nécessite aucune attention immédiate. (Par défaut, les recommandations faibles ne sont pas présentées, mais vous pouvez filtrer sur les recommandations faibles si vous souhaitez tooview les.)

Détails de la recommandation tooview hello, cliquez sur nom hello hello virtual machine. Un nouveau panneau pour que l’ordinateur virtuel s’ouvre avec liste hello des mises à jour comme indiqué dans hello suivant capture d’écran.

![Mise à jour système manquante pour une machine virtuelle spécifique](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> Hello ici les recommandations de sécurité sont hello identiques à ceux de hello **recommandations** panneau. Consultez hello [mise en œuvre des recommandations de sécurité dans le centre de sécurité Azure](security-center-recommendations.md) article pour plus d’informations sur les recommandations tooresolve. Cela s’applique non seulement pour les machines virtuelles, mais également pour toutes les ressources qui sont disponibles dans hello **l’intégrité des ressources** vignette.
>
>

#### <a name="virtual-machines-section"></a>Section Machines virtuelles
section de machines virtuelles Hello vous donne une vue d’ensemble de tous les ordinateurs virtuels et des recommandations. Chaque colonne représente un ensemble de recommandations, comme indiqué dans hello suivant capture d’écran :

![Vue d’ensemble des machines virtuelles et des recommandations](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

icône Hello qui s’affiche sous chaque permet de recommandation tooquickly vous identifier les machines virtuelles hello qui nécessitent une attention et hello du type de recommandation.

Dans l’exemple précédent de hello, un ordinateur virtuel possède une recommandation critiques en matière de protection de point de terminaison. tooget plus d’informations sur l’ordinateur virtuel de hello, cliquez dessus. Ouvre un nouveau panneau représente cet ordinateur virtuel comme indiqué dans hello suivant capture d’écran.

![Informations détaillées sur la sécurité de la machine virtuelle](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Ce panneau comporte les détails de sécurité hello pour la machine virtuelle de hello. Au bas de hello de ce panneau, vous pouvez voir hello recommandé d’action et gravité hello de chaque problème.

#### <a name="cloud-services-section"></a>Section Services cloud
Services de cloud computing, une recommandation est créée lors de la version du système d’exploitation hello est périmée comme indiqué dans hello suivant capture d’écran :

![État d’intégrité des services cloud](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

Dans un scénario où vous possédez recommandation (qui n’est pas les cas de hello pour hello l’exemple précédent), vous devez toofollow des étapes de hello dans la version de système d’exploitation hello recommandation tooupdate hello. Lorsqu’une mise à jour est disponible, vous aurez une alerte (rouge ou orange - dépend de gravité hello du problème de hello). Lorsque vous cliquez sur cette alerte dans les lignes hello WebRole1 (exécute Windows Server avec votre tooIIS d’application déployée automatiquement web) ou WorkerRole1 (exécute Windows Server avec votre tooIIS d’application déployée automatiquement web), un nouveau panneau s’ouvre avec plus de détails recommandation comme indiqué dans hello suivant capture d’écran :

![Détails du service cloud](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

toosee obtenir une explication plus normative sur cette recommandation, cliquez sur **version de mise à jour du système d’exploitation** sous hello **DESCRIPTION** colonne. Hello **version de système d’exploitation de la mise à jour (version préliminaire)** panneau s’ouvre avec plus de détails.

![Recommandations de services cloud](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Surveillance des réseaux virtuels
Lorsque vous cliquez sur **réseau** vignette, hello **réseau** panneau s’ouvre avec plus de détails comme dans hello suivant capture d’écran :

![Panneau Mise en réseau](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Recommandations pour la mise en réseau
Comme hello les informations de contrôle d’intégrité de ressources de l’ordinateur virtuel, ce panneau fournit une liste récapitulative des problèmes à haut hello du Panneau de hello et une liste des réseaux analysés sous hello.

Hello mise en réseau de la section de détail d’état répertorie les problèmes potentiels de sécurité et offre [recommandations](security-center-network-recommendations.md). Voici des exemples de problèmes potentiels :

* Absence d’installation d’un pare-feu de nouvelle génération
* Non-activation des groupes de sécurité réseau
* Non-activation des groupes de sécurité réseau sur les machines virtuelles
* Restriction de l’accès externe via le point de terminaison externe public
* Intégrité des points de terminaison exposés à Internet

Lorsque vous cliquez sur une recommandation, un nouveau panneau s’ouvre avec plus de détails sur la recommandation de hello comme indiqué dans hello l’exemple suivant.

![Détails d’une recommandation dans le panneau de mise en réseau hello](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

Dans cet exemple, hello **configurer manquant groupes de sécurité réseau pour les sous-réseaux** panneau a une liste de sous-réseaux et de protection du groupe de sécurité du réseau de machines virtuelles qui sont manquants. Si vous cliquez sur toowhich de sous-réseau hello souhaité d’un groupe de sécurité réseau tooapply hello, un autre panneau s’ouvre.

Bonjour **choisir un groupe de sécurité réseau** panneau, vous pouvez sélectionner le groupe de sécurité de réseau plus approprié hello pour le sous-réseau de hello, ou vous pouvez créer un nouveau groupe de sécurité réseau.

#### <a name="internet-facing-endpoints-section"></a>Section des points de terminaison accessibles sur Internet
Bonjour **Internet faisant face à des points de terminaison** section, vous pouvez voir des machines virtuelles hello actuellement configurés via une connexion Internet d’accès au point de terminaison et son état actuel.

![Les machines virtuelles configurées avec un point de terminaison accessible sur Internet et son état](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Cette table a le nom de point de terminaison hello représentant hello virtual machine, hello exposés à l’adresse IP, Internet et hello actuels de gravité du groupe de sécurité réseau hello et hello Conviction. tableau de Hello est trié par niveau de gravité :

* Rouge (en haut) : priorité élevée ; doivent être traités immédiatement
* Orange : priorité moyenne ; doivent être traités dès que possible
* Vert (le dernier) : état d’intégrité

#### <a name="networking-topology-section"></a>Section de topologie de mise en réseau
Hello **topologie de réseau** section comporte une vue hiérarchique des ressources de hello comme illustré dans hello suivant capture d’écran :

![Vue hiérarchique des ressources dans la section Topologie de mise en réseau](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Ce tableau est trié (machines virtuelles et sous-réseaux) par niveau de gravité :

* Rouge (en haut) : priorité élevée ; doivent être traités immédiatement
* Orange : priorité moyenne ; doivent être traités dès que possible
* Vert (le dernier) : état d’intégrité

Dans cette vue de la topologie, le premier niveau de hello a [réseaux virtuels](../virtual-network/virtual-networks-overview.md), [passerelles de réseau virtuel](/vpn-gateway/vpn-gateway-site-to-site-create.md), et [des réseaux virtuels (classiques)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). au niveau du deuxième Hello a des sous-réseaux, et au niveau du troisième hello a hello virtuels appartenant aux sous-réseaux de toothose. colonne de droite Hello a état actuel de hello du groupe de sécurité réseau hello pour ces ressources, comme illustré dans hello l’exemple suivant :

![État du groupe de sécurité réseau hello dans la section topologie de mise en réseau](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

recommandations hello pour cet ordinateur virtuel, qui est similaire a Hello partie inférieure de ce panneau toowhat est décrite précédemment. Vous pouvez cliquez sur une recommandation toolearn plus ou appliquer hello nécessité pour contrôler la sécurité ou configuration.

### <a name="monitor-storage--data"></a>Analyse de Stockage et données

Lorsque vous cliquez sur **stockage & données** Bonjour **prévention** section hello **ressources de données** panneau s’ouvre avec les recommandations pour le stockage et SQL. Il a également [recommandations](security-center-sql-service-recommendations.md) hello général États d’intégrité de base de données hello. Pour plus d’informations sur le chiffrement du stockage, consultez [Enable encryption for Azure storage account in Azure Security Center (Activer le chiffrement pour le compte de stockage Azure dans Azure Security Center)](security-center-enable-encryption-for-storage-account.md).

![Ressources de données](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

Sous **recommandations SQL**, vous pouvez cliquer sur n’importe quel recommandation et obtenir plus d’informations sur l’autre action tooresolve un problème. Hello suivant montre l’expansion de hello hello **détection de menace et de l’audit de base de données sur les bases de données SQL** recommandation.

![Détails relatifs à une recommandation SQL](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

Hello **activer l’audit et menace pour la détection sur les bases de données SQL** panneau a hello informations suivantes :

* Une liste des bases de données SQL.
* serveur Hello sur lequel ils se trouvent
* Plus d’informations sur si ce paramètre a été hérité hello serveur ou si elle est unique dans cette base de données
* état actuel de Hello
* gravité Hello du problème de hello

Lorsque vous cliquez sur tooaddress de base de données hello cette recommandation, hello **détection d’audit et de menaces** panneau s’ouvre, comme indiqué dans hello suivant l’écran.

![Panneau Audit et détection des menaces](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

tooenable l’audit, sélectionnez **ON** sous hello **audit** option.

### <a name="monitor-applications"></a>Surveillance des applications

Si votre charge de travail Azure a des applications situées dans [machines virtuelles (créées via Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) ports web exposé (ports TCP 80 et 443), le centre de sécurité permet de surveiller les problèmes potentiels de sécurité tooidentify et recommandant des étapes de mise à jour. Lorsque vous cliquez sur hello **Applications** vignette, hello **Applications** panneau s’ouvre avec une série de recommandations de hello **recommandations** section. Il montre également la décomposition d’application hello par adresse IP virtuelle/hôte comme indiqué dans hello suivant capture d’écran.

![État de sécurité des applications](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Tout comme vous avec hello autres recommandations, vous pouvez cliquer sur une recommandation toosee plus de détails sur le problème de hello et comment tooremediate. exemple Hello hello figure suivante est une application qui a été identifiée comme une application web non sécurisée. Lorsque vous sélectionnez application hello qui a été considérée comme sûre, un autre panneau s’ouvre avec hello option disponible suivante :

![Détails relatifs à une application non sécurisée](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

Ce panneau répertorie toutes les recommandations pour cette application. Lorsque vous cliquez sur hello **ajouter un pare-feu d’applications web** recommendation, hello **ajouter un pare-feu d’applications Web** panneau s’ouvre, avec des options pour vous tooinstall, un pare-feu d’applications web (WAF) à partir d’un partenaire en tant que illustré hello suivant capture d’écran.

![Boîte de dialogue Ajouter un pare-feu d’applications web](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Voir aussi
Dans cet article, vous avez appris comment toouse ses fonctionnalités dans le centre de sécurité Azure de surveillance. toolearn en savoir plus sur Azure Security Center, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md): Découvrez comment tooconfigure les paramètres de sécurité dans le centre de sécurité Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md): Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md): Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md): Forum aux questions sur l’utilisation hello service de recherche.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.
