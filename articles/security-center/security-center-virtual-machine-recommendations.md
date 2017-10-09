---
title: "aaaProtecting vos machines virtuelles dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document traite des recommandations d’Azure Security Center qui peuvent vous aider à protéger vos machines virtuelles et à rester en conformité avec les stratégies de sécurité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>Protection de vos machines virtuelles dans Azure Security Center
Centre de sécurité Azure analyse l’état de la sécurité de vos ressources Azure hello. Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il crée des recommandations qui vous guident tout au long des processus de hello de configuration de contrôles de hello nécessité.  Recommandations s’appliquent à des types de ressources tooAzure : machines virtuelles (VM), mise en réseau, SQL et les applications.

Cet article traite des recommandations qui s’appliquent tooVMs.  Les recommandations relatives aux machines virtuelles se concentrent autour de la collecte de données, de l’application des mises à jour du système, de la configuration du logiciel anti-programme malveillant, du chiffrement de vos disques de machines virtuelles, et bien plus encore.  Tableau hello ci-dessous comme un toohelp de référence que vous comprenez les recommandations machine virtuelle disponibles hello et que chacun d’eux faire si vous l’appliquez.

## <a name="available-vm-recommendations"></a>Recommandations disponibles pour les machines virtuelles
| Recommandation | Description |
| --- | --- |
| [Activer la collecte des données pour des abonnements](security-center-enable-data-collection.md) |Vous recommande d’activer la collecte des données dans la stratégie de sécurité hello pour chacun de vos abonnements et toutes les machines virtuelles (VM) dans vos abonnements. |
| [Activer le chiffrement pour le compte de stockage Azure](security-center-enable-encryption-for-storage-account.md) | Recommande d’activer Azure Storage Service Encryption pour les données au repos. Chiffrement de Service de stockage (SSE) fonctionne en chiffrant les données de hello lorsqu’il est écrit tooAzure stockage et déchiffre avant récupération. SSE n’est actuellement disponible uniquement pour hello service Blob Azure et peut être utilisé pour les objets BLOB de blocs, objets BLOB de pages et ajoute des objets BLOB. toolearn, voir [chiffrement de Service de stockage pour les données au repos](../storage/common/storage-service-encryption.md).</br>SSE est uniquement pris en charge sur les comptes de stockage Resource Manager. Les comptes de stockage Classic ne sont actuellement pas pris en charge. hello toounderstand classique et les modèles de déploiement du Gestionnaire de ressources, consultez [modèles de déploiement Azure](../azure-classic-rm.md). |
| [Corriger des vulnérabilités du système d’exploitation](security-center-remediate-os-vulnerabilities.md) |Recommande que vous s’alignent sur vos configurations de système d’exploitation hello recommandé de règles de configuration, par exemple, ne permettent pas de toobe des mots de passe enregistré. |
| [Appliquer des mises à jour système](security-center-apply-system-updates.md) |Recommande de déployer la sécurité du système manquantes et tooVMs de mises à jour critiques. |
| [Appliquer un contrôle d’accès réseau Juste à temps](security-center-just-in-time.md) | Recommande d’appliquer un accès Juste à temps à la machine virtuelle. Hello juste-à-temps est en version préliminaire et disponible sur hello niveau Standard de centre de sécurité. Consultez [tarification](security-center-pricing.md) niveaux de tarification du toolearn en savoir plus sur le centre de sécurité. |
| [Redémarrage après des mises à jour système](security-center-apply-system-updates.md#reboot-after-system-updates) |Recommande de redémarrer un processus de hello toocomplete machine virtuelle de l’application de mises à jour du système. |
| [Installer Endpoint Protection](security-center-install-endpoint-protection.md) |Recommande que vous configuriez tooVMs de programmes de logiciels anti-programme malveillant (machines virtuelles Windows uniquement). |
| [Résoudre les alertes d’intégrité Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recommande la résolution des défaillances de protection de point de terminaison. |
| [Activer l’agent de machine virtuelle](security-center-enable-vm-agent.md) |Permet de toosee qui nécessitent des machines virtuelles hello Agent de machine virtuelle. Hello Agent de machine virtuelle doit être installé sur des machines virtuelles dans le correctif de tooprovision d’ordre d’analyse, l’analyse de la ligne de base et des programmes de logiciels anti-programme malveillant. Hello Agent de machine virtuelle est installé par défaut pour les ordinateurs virtuels qui sont déployés à partir de hello Azure Marketplace. article de Hello [Agent de machine virtuelle et Extensions-partie 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fournit des informations sur la façon dont tooinstall hello Agent de machine virtuelle. |
| [Apply disk encryption (Appliquer le chiffrement de disque Azure Disk Encryption)](security-center-apply-disk-encryption.md) |Recommande le chiffrement des disques des machines virtuelles à l’aide d’Azure Disk Encryption (Windows et Linux). Le chiffrement est recommandé pour hello du système d’exploitation et les volumes de données sur votre machine virtuelle. |
| [Mettre à jour la version du système d’exploitation](security-center-update-os-version.md) |Vous recommande de mettre à jour version de système d’exploitation (OS) hello pour votre Service Cloud toohello version la plus récente pour votre famille de systèmes d’exploitation.  toolearn savoir plus sur les Services de cloud computing, consultez hello [vue d’ensemble des Services de cloud computing](../cloud-services/cloud-services-choose-me.md). |
| [Évaluation des vulnérabilités non installée](security-center-vulnerability-assessment-recommendations.md) |Recommande d’installer une solution d’évaluation des vulnérabilités sur votre machine virtuelle. |
| [Corriger des vulnérabilités](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Vous permet de toosee système et application des vulnérabilités détectées par la solution d’évaluation des risques de vulnérabilité hello installée sur votre machine virtuelle. |

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur les recommandations qui s’appliquent les types de ressources Azure tooother, voir hello :

* [Protection de vos applications dans Azure Security Center](security-center-application-recommendations.md)
* [Protection de votre réseau dans Azure Security Center](security-center-network-recommendations.md)
* [Protection de votre service SQL Azure dans Azure Security Center](security-center-sql-service-recommendations.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
