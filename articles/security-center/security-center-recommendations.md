---
title: "recommandations de sécurité aaaManaging dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment les recommandations du Centre de sécurité Azure peuvent vous aider à protéger vos ressources Azure et à rester en conformité avec les stratégies de sécurité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Gestion des recommandations de sécurité dans le Centre de sécurité Azure
Ce document vous guide tout comment toouse recommandations toohelp du centre de sécurité Azure protègent vos ressources Azure.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Ce document n'est pas un guide pas à pas.
>
>

## <a name="what-are-security-recommendations"></a>Quelles sont les recommandations de sécurité ?
Centre de sécurité analyse régulièrement l’état de la sécurité de vos ressources Azure hello. Lorsqu’il identifie des failles de sécurité potentielles, il crée des recommandations. recommandations de Hello vous guident tout au long des processus de hello de configuration de contrôles de hello si nécessaire.

## <a name="implementing-security-recommendations"></a>Mise en œuvre des recommandations de sécurité
### <a name="set-recommendations"></a>Définition de recommandations
Dans la section [Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md), vous apprendrez à :

* configurer des stratégies de sécurité ;
* activer la collecte des données ;
* Choisissez le toosee recommandations dans le cadre de votre stratégie de sécurité.

Les recommandations de stratégie actuelles se concentrent sur les mises à jour système, les règles de base, les logiciels anti-programme malveillant, les [groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) pour les sous-réseaux et les interfaces réseau, l’audit des bases de données SQL, le Transparent Data Encryption de bases de données SQL et les pare-feu d’applications web.  [Définition de stratégies de sécurité](security-center-policies.md) fournit une description de chacune des recommandations.

### <a name="monitor-recommendations"></a>Suivi des recommandations
Après avoir défini une stratégie de sécurité, le centre de sécurité analyse état de sécurité hello des vulnérabilités potentielles tooidentify ressources. Hello **recommandations** vignette sur hello **centre de sécurité** panneau vous permet de connaître le nombre total de hello de recommandations identifié par le centre de sécurité.

![Panneau Recommandations][1]

Détails de hello toosee de chaque recommandation :

Sélectionnez hello **recommandations vignette** sur hello **centre de sécurité** panneau. Hello **recommandations** panneau s’ouvre.

recommandations de Hello sont affichées sous forme de tableau, où chaque ligne représente une recommandation particulière. Hello des colonnes de cette table sont :

* **DESCRIPTION**: explique la recommandation de hello et la procédure toobe fait tooaddress il.
* **RESSOURCE**: répertorie les toowhich de ressources hello cette recommandation s’applique.
* **ÉTAT**: décrit l’état actuel de hello de recommandation de hello :
  * **Ouvrez**: recommandation de hello n’a pas encore été satisfaite.
  * **En cours d’exécution**: recommandation de hello est en train de ressources de toohello appliqués et aucune action n’est requise par vous.
  * **Résolu**: recommandation de hello a déjà été effectuée (dans ce cas, la ligne de hello est grisée).
* **GRAVITÉ**: décrit la gravité hello de cette recommandation particulier :
  * **Élevée** : existence d’une vulnérabilité sur une ressource importante (application, machine virtuelle ou groupe de sécurité réseau). Le problème doit être analysé.
  * **Support**: il existe une vulnérabilité et non critiques ou d’autres étapes sont requise tooeliminate ou toocomplete un processus.
  * **Faible**: existence d’une vulnérabilité devant être prise en compte, mais qui ne nécessite pas une attention immédiate. (Par défaut, les recommandations faibles ne sont pas présentées, mais vous pouvez filtrer sur les recommandations faibles si vous souhaitez toosee les.)

Tableau hello ci-dessous comme un toohelp de référence que vous comprenez les recommandations disponibles hello et ce que fait chacun d’eux si vous l’appliquez.

> [!NOTE]
> Vous pouvez toounderstand hello [classique et les modèles de déploiement Resource Manager](../azure-classic-rm.md) pour les ressources Azure.
>
>

| Recommandation | Description |
| --- | --- |
| [Activer la collecte des données pour des abonnements](security-center-enable-data-collection.md) |Vous recommande d’activer la collecte des données dans la stratégie de sécurité hello pour chacun de vos abonnements et toutes les machines virtuelles (VM) dans vos abonnements. |
| [Corriger des vulnérabilités du système d’exploitation](security-center-remediate-os-vulnerabilities.md) |Vous recommande de vos configurations de système d’exploitation s’alignent hello recommandé des règles de configuration, par exemple, de ne pas autoriser les toobe des mots de passe enregistré. |
| [Appliquer des mises à jour système](security-center-apply-system-updates.md) |Recommande de déployer la sécurité du système manquantes et tooVMs de mises à jour critiques. |
| [Appliquer un contrôle d’accès réseau Juste à temps](security-center-just-in-time.md) | Recommande d’appliquer un accès Juste à temps à la machine virtuelle. Hello juste-à-temps est en version préliminaire et disponible sur hello niveau Standard de centre de sécurité. Consultez [tarification](security-center-pricing.md) niveaux de tarification du toolearn en savoir plus sur le centre de sécurité. |
| [Redémarrage après des mises à jour système](security-center-apply-system-updates.md#reboot-after-system-updates) |Recommande de redémarrer un processus de hello toocomplete machine virtuelle de l’application de mises à jour du système. |
| [Add a web application firewall](security-center-add-web-application-firewall.md) |Recommande le déploiement d’un pare-feu d’applications web (WAF) pour les points de terminaison web. Une recommandation WAF est indiquée pour n’importe quelle IP publique (adresse IP de niveau d’instance ou adresse IP à équilibrage de charge) ayant un groupe de sécurité réseau associé avec des ports web entrants ouverts (80, 443). </br>Centre de sécurité vous recommande de que configurer un toohelp WAF vous défendre contre des attaques ciblant vos applications web sur des ordinateurs virtuels et sur l’environnement App Service. Un environnement App Service (ASE) est une option de plan de service [Premium](https://azure.microsoft.com/pricing/details/app-service/) d'Azure App Service qui fournit un environnement totalement isolé et dédié pour l'exécution sécurisée de vos applications Azure App Service. toolearn en savoir plus sur ASE, consultez hello [Documentation d’environnement App Service](../app-service/app-service-app-service-environments-readme.md).</br>Vous pouvez protéger plusieurs applications web dans le centre de sécurité en ajoutant ces applications tooyour WAF les déploiements existants. |
| [Finaliser la protection des applications](security-center-add-web-application-firewall.md#finalize-application-protection) |configuration hello toocomplete un WAF, le trafic doit être toohello reroutage de remise WAF appliance. Respect de cette recommandation termine les modifications de configuration nécessaires hello. |
| [Ajouter un pare-feu de nouvelle génération](security-center-add-next-generation-firewall.md) |Recommande d’ajouter un pare-feu de la génération suivante (Conviction) à partir d’un tooincrease de partenaire Microsoft votre protections de sécurité. |
| [Acheminer le trafic uniquement via un pare-feu de nouvelle génération](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Recommande de configurer les règles de groupe (NSG) de sécurité réseau qui force le trafic entrant tooyour machine virtuelle via votre Conviction. |
| [Installer Endpoint Protection](security-center-install-endpoint-protection.md) |Recommande que vous configuriez tooVMs de programmes de logiciels anti-programme malveillant (machines virtuelles Windows uniquement). |
| [Résoudre les alertes d’intégrité Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recommande la résolution des défaillances de protection de point de terminaison. |
| [Activer des groupes de sécurité réseau sur les sous-réseaux et ou les machines virtuelles](security-center-enable-network-security-groups.md) |Recommande l’activation des groupes de sécurité réseau sur les sous-réseaux ou les machines virtuelles. |
| [Restreindre l’accès via un point de terminaison accessible sur Internet](security-center-restrict-access-through-internet-facing-endpoints.md) |Recommande la configuration de règles de trafic entrant pour les groupes de sécurité réseau. |
| [Activer l’audit et la détection des menaces dans les serveurs SQL](security-center-enable-auditing-on-sql-servers.md) |Recommande l’activation de l’audit et de la détection des menaces pour les serveurs Azure SQL. (Service Azure SQL uniquement. N’inclut pas SQL en cours d’exécution sur vos machines virtuelles.) |
| [Activer l’audit et la détection des menaces dans les bases de données SQL](security-center-enable-auditing-on-sql-databases.md) |Recommande l’activation de l’audit et de la détection des menaces pour les bases de données Azure SQL. (Service Azure SQL uniquement. N’inclut pas SQL en cours d’exécution sur vos machines virtuelles.) |
| [Activer le chiffrement transparent des données des bases de données SQL](security-center-enable-transparent-data-encryption.md) |Recommande l’activation du chiffrement pour les bases de données SQL. (Service Azure SQL uniquement.) |
| [Activer l’agent de machine virtuelle](security-center-enable-vm-agent.md) |Permet de toosee qui nécessitent des machines virtuelles hello Agent de machine virtuelle. Hello Agent de machine virtuelle doit être installé sur les machines virtuelles tooprovision correctif est l’analyse, l’analyse de la ligne de base et les programmes de logiciel anti-programme malveillant. Hello Agent de machine virtuelle est installé par défaut pour les ordinateurs virtuels qui sont déployés à partir de hello Azure Marketplace. article de Hello [Agent de machine virtuelle et Extensions-partie 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fournit des informations sur la façon dont tooinstall hello Agent de machine virtuelle. |
| [Apply disk encryption (Appliquer le chiffrement de disque Azure Disk Encryption)](security-center-apply-disk-encryption.md) |Recommande le chiffrement des disques des machines virtuelles à l’aide d’Azure Disk Encryption (Windows et Linux). Le chiffrement est recommandé pour hello du système d’exploitation et les volumes de données sur votre machine virtuelle. |
| [Fournir des informations de contact de sécurité](security-center-provide-security-contact-details.md) |Vous recommande de fournir des informations de contact de sécurité pour chacun de vos abonnements. Les informations de contact correspondent à une adresse électronique et à un numéro de téléphone. informations Hello sont toocontact utilisé si la recherche de notre équipe de sécurité que vos ressources sont compromis. |
| [Mettre à jour la version du système d’exploitation](security-center-update-os-version.md) |Vous recommande de mettre à jour version de système d’exploitation (OS) hello pour votre Service Cloud toohello version la plus récente pour votre famille de systèmes d’exploitation.  toolearn savoir plus sur les Services de cloud computing, consultez hello [vue d’ensemble des Services de cloud computing](../cloud-services/cloud-services-choose-me.md). |
| [Évaluation des vulnérabilités non installée](security-center-vulnerability-assessment-recommendations.md) |Recommande d’installer une solution d’évaluation des vulnérabilités sur votre machine virtuelle. |
| [Corriger des vulnérabilités](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Vous permet de toosee système et application des vulnérabilités détectées par la solution d’évaluation des risques de vulnérabilité hello installée sur votre machine virtuelle. |
| [Activer le chiffrement pour le compte de stockage Azure](security-center-enable-encryption-for-storage-account.md) | Recommande d’activer Azure Storage Service Encryption pour les données au repos. Chiffrement de Service de stockage (SSE) fonctionne en chiffrant les données de hello lorsqu’il est écrit tooAzure stockage et déchiffre avant récupération. SSE n’est actuellement disponible uniquement pour hello service Blob Azure et peut être utilisé pour les objets BLOB de blocs, objets BLOB de pages et ajoute des objets BLOB. toolearn, voir [chiffrement de Service de stockage pour les données au repos](../storage/common/storage-service-encryption.md).</br>SSE est uniquement pris en charge sur les comptes de stockage Resource Manager. |

Vous pouvez filtrer et ignorer les recommandations.

1. Sélectionnez **filtre** sur hello **recommandations** panneau. Hello **filtre** panneau s’ouvre et que vous sélectionnez des valeurs de gravité et son état hello toosee vous le souhaitez.

    ![Filtrer les recommandations][2]
2. Si vous déterminez qu’une recommandation n’est pas applicable, vous pouvez faire disparaître la recommandation de hello et puis de les filtrer en dehors de votre affichage. Il existe deux façons toodismiss une recommandation. Une façon est tooright cliquez sur un élément, puis sélectionnez **Dismiss**. Hello autres toohover sur un élément, cliquez sur les points de hello trois qui apparaissent à droite de toohello, puis sélectionnez **Dismiss**. Vous pouvez afficher les recommandations ignorées en cliquant sur **Filtrer**, puis en sélectionnant **Rejeté**.

    ![Ignorer une recommandation][3]

### <a name="apply-recommendations"></a>Appliquer les recommandations
Après avoir examiné toutes les recommandations, vous pouvez décider d’en appliquer une en priorité. Nous vous recommandons d’utiliser l’indice de gravité hello comme hello tooevaluate paramètre principal les recommandations doivent être appliquées en premier.

Dans la table hello des recommandations ci-dessus, sélectionnez une recommandation et suivre les étapes comme un exemple de tooapply une recommandation.

## <a name="next-steps"></a>Étapes suivantes
Dans ce document, vous ne les recommandations toosecurity introduites dans le centre de sécurité. toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) : Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) — Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
