---
title: "aaaAzure centre de sécurité et des Machines virtuelles Azure | Documents Microsoft"
description: "Ce document vous aide à toounderstand comment Azure Security Center peut protéger des Machines virtuelles Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a>Azure Security Center et machines virtuelles Azure
[Centre de sécurité Azure](https://azure.microsoft.com/services/security-center/) vous aide à empêcher, détecter et répondre toothreats. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

Cet article explique comment Security Center peut vous aider à sécuriser vos machines virtuelles Azure.

## <a name="why-use-security-center"></a>Pourquoi utiliser Security Center ?
Security Center vous aide à protéger les données de vos machines virtuelles dans Azure en vous offrant de la visibilité sur les paramètres de sécurité de votre machine virtuelle. Lorsque le centre de sécurité protège vos machines virtuelles, hello suivant les fonctionnalités seront disponible :

* Paramètres de sécurité de système d’exploitation (OS) avec hello recommandé de règles de configuration
* Sécurité du système et mises à jour critiques manquantes
* Recommandations de protection du point de terminaison
* Validation du chiffrement de disque
* Évaluation et correction des vulnérabilités
* Détection de menaces

En outre toohelping protéger vos machines virtuelles Azure, le centre de sécurité fournit également la surveillance de la sécurité et de gestion pour les Services de cloud computing, Services d’application, les réseaux virtuels et bien plus encore. 

> [!NOTE]
> Consultez [Introduction tooAzure centre de sécurité](security-center-intro.md) toolearn plus d’informations sur Azure Security Center.
> 
> 

## <a name="prerequisites"></a>Composants requis
tooget main Azure Security Center, vous devez tooknow et tenez compte hello qui suit :

* Vous devez avoir un tooMicrosoft abonnement Azure. Pour plus d’informations sur les niveaux Gratuit et Standard de Security Center, consultez l’article [Tarification de Security Center](https://azure.microsoft.com/pricing/details/security-center/).
* Planifier l’adoption de votre centre de sécurité, consultez [guide de planification et les opérations Azure Security Center](security-center-planning-and-operations-guide.md) toolearn plus d’informations sur les considérations de planification et les opérations.
* Pour plus d’informations sur la prise en charge du système d’exploitation, consultez le [Forum au questions Azure Security Center](security-center-faq.md). 

## <a name="set-security-policy"></a>Définir une stratégie de sécurité
Données collection besoins toobe activée afin que ce centre de sécurité Azure peut recueillir des informations hello nécessaires tooprovide recommandations et des alertes sont générées en fonction de la stratégie de sécurité hello que vous configurez. Dans la figure hello ci-dessous, vous pouvez voir que **collecte des données** a été activée **sur**.

Une stratégie de sécurité définit un jeu hello des contrôles qui sont recommandés pour les ressources hello spécifié abonnement ou groupe de ressources. Avant d’activer la stratégie de sécurité, vous devez avoir activé la collecte de données, tooassess leur état de sécurité, fournir des recommandations de sécurité et vous alerter toothreats de commande du centre de sécurité recueille des données à partir de vos machines virtuelles dans. Dans le centre de sécurité, vous définissez des stratégies pour vos abonnements Azure ou les groupes de ressources en fonction de la société tooyour aux besoins de sécurité et de type hello d’applications ou de la sensibilité des données hello dans chaque abonnement. 

![Stratégie de sécurité](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> toolearn plus en détail chacune **stratégie de prévention de** disponible, voir [définir des stratégies de sécurité](security-center-policies.md) l’article.
> 
> 

## <a name="manage-security-recommendations"></a>Gérer les recommandations de sécurité
Centre de sécurité analyse l’état de la sécurité de vos ressources Azure hello. Lorsqu’il identifie des failles de sécurité potentielles, il crée des recommandations. recommandations de Hello vous guident tout au long des processus de hello de configuration de contrôles de hello si nécessaire.

Après avoir défini une stratégie de sécurité, le centre de sécurité analyse état de sécurité hello des vulnérabilités potentielles tooidentify ressources. recommandations de Hello sont affichées sous forme de tableau, où chaque ligne représente une recommandation particulière. tableau Hello ci-dessous fournit des exemples de recommandations pour les machines virtuelles Azure et que chacun d’eux faire si vous l’appliquez. Lorsque vous sélectionnez une recommandation, vous recevrez des informations qui vous montre comment tooimplement hello recommandation dans le centre de sécurité.

| Recommandation | Description |
| --- | --- |
| [Activer la collecte des données pour des abonnements](security-center-enable-data-collection.md) |Vous recommande d’activer la collecte des données dans la stratégie de sécurité hello pour chacun de vos abonnements et toutes les machines virtuelles (VM) dans vos abonnements. |
| [Corriger des vulnérabilités du système d’exploitation](security-center-remediate-os-vulnerabilities.md) |Recommande que vous s’alignent sur vos configurations de système d’exploitation hello recommandé de règles de configuration, par exemple, ne permettent pas de toobe des mots de passe enregistré. |
| [Appliquer des mises à jour système](security-center-apply-system-updates.md) |Recommande de déployer la sécurité du système manquantes et tooVMs de mises à jour critiques. |
| [Redémarrage après des mises à jour système](security-center-apply-system-updates.md#reboot-after-system-updates) |Recommande de redémarrer un processus de hello toocomplete machine virtuelle de l’application de mises à jour du système. |
| [Installer Endpoint Protection](security-center-install-endpoint-protection.md) |Recommande que vous configuriez tooVMs de programmes de logiciels anti-programme malveillant (machines virtuelles Windows uniquement). |
| [Résoudre les alertes d’intégrité Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recommande la résolution des défaillances de protection de point de terminaison. |
| [Activer l’agent de machine virtuelle](security-center-enable-vm-agent.md) |Permet de toosee qui nécessitent des machines virtuelles hello Agent de machine virtuelle. Hello Agent de machine virtuelle doit être installé sur des machines virtuelles dans le correctif de tooprovision d’ordre d’analyse, l’analyse de la ligne de base et des programmes de logiciels anti-programme malveillant. Hello Agent de machine virtuelle est installé par défaut pour les ordinateurs virtuels qui sont déployés à partir de hello Azure Marketplace. article de Hello [Agent de machine virtuelle et Extensions-partie 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fournit des informations sur la façon dont tooinstall hello Agent de machine virtuelle. |
| [Apply disk encryption (Appliquer le chiffrement de disque Azure Disk Encryption)](security-center-apply-disk-encryption.md) |Recommande le chiffrement des disques des machines virtuelles à l’aide d’Azure Disk Encryption (Windows et Linux). Le chiffrement est recommandé pour hello du système d’exploitation et les volumes de données sur votre machine virtuelle. |
| [Évaluation des vulnérabilités non installée](security-center-vulnerability-assessment-recommendations.md) |Recommande d’installer une solution d’évaluation des vulnérabilités sur votre machine virtuelle. |
| [Corriger des vulnérabilités](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Vous permet de toosee système et application des vulnérabilités détectées par la solution d’évaluation des risques de vulnérabilité hello installée sur votre machine virtuelle. |

> [!NOTE]
> toolearn en savoir plus sur les recommandations, consultez [gestion des recommandations de sécurité](security-center-recommendations.md) l’article.
> 
> 

## <a name="monitor-security-health"></a>Surveiller l’intégrité de la sécurité
Après avoir activé [des stratégies de sécurité](security-center-policies.md) pour les ressources d’un abonnement, le centre de sécurité analysera sécurité hello des vulnérabilités potentielles tooidentify ressources.  Vous pouvez afficher d’état de la sécurité de vos ressources, ainsi que des problèmes dans hello hello **contrôle d’intégrité de sécurité** panneau. Lorsque vous cliquez sur **virtuels** Bonjour **sécurité des ressources** vignette de contrôle d’intégrité, hello **virtuels** panneau s’ouvre avec les recommandations pour vos machines virtuelles. 

![Intégrité de la sécurité](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>Gérer et répondre toosecurity alertes
Centre de sécurité collecte, analyse automatiquement et intègre des données de journal à partir de vos ressources Azure, hello réseau et les solutions de partenaire connecté (tels que des pare-feu et endpoint protection solutions), les menaces réelles toodetect et réduire les faux positifs. En tirant parti d’une agrégation divers de [des fonctionnalités de détection](security-center-detection-capabilities.md), centre de sécurité est en mesure de toogenerate hiérarchisé toohelp des alertes de sécurité vous étudiez hello problème rapidement et que vous fournissez des recommandations sur la manière tooremediate attaques possibles.

![Alertes de sécurité](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Sélectionnez un toolearn d’alerte de sécurité plus sur les événements hello ayant déclenché l’alerte de hello et, si elle existe, les étapes doivent tootake tooremediate une attaque. Les alertes de sécurité sont regroupées par [type](security-center-alerts-type.md) et date d’apparition.

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.

