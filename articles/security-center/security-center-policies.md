---
title: "aaaSet des stratégies de sécurité dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous aide à tooconfigure des stratégies de sécurité dans le centre de sécurité Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Définir des stratégies de sécurité dans Azure Security Center
Ce document vous aide à tooconfigure des stratégies de sécurité dans le centre de sécurité en vous guidant dans hello étapes nécessaires tooperform cette tâche.

>[!NOTE] 
>À compter de début juin 2017, centre de sécurité utilise des données de toocollect et le magasin de Microsoft Monitoring Agent de hello. Consultez [Migration de plateforme Azure Security Center](security-center-platform-migration.md) toolearn plus. informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>

## <a name="what-are-security-policies"></a>Que sont les stratégies de sécurité ?
Une stratégie de sécurité définit l’ensemble de hello de contrôles, qui sont recommandés pour les ressources hello spécifié abonnement. Dans le centre de sécurité, vous définissez des stratégies pour vos abonnements Azure, selon les besoins de sécurité d’entreprise tooyour et de type hello d’applications ou de la sensibilité des données hello dans chaque abonnement.

Par exemple, les ressources utilisées pour le développement ou le test peuvent avoir des exigences de sécurité différentes de celles utilisées pour les applications de production. De même, les applications qui utilisent des données réglementées, telles que des informations d’identification personnelle, peuvent nécessiter un niveau de sécurité plus élevé. Stratégies de sécurité qui sont activées dans les recommandations de sécurité de lecteur Azure Security Center et de surveillance toohelp identifier les vulnérabilités potentielles et d’atténuer les menaces. Lecture [Azure Security Center Guide de planification et opérations](security-center-planning-and-operations-guide.md) pour plus d’informations sur comment toodetermine hello option qui vous convient.

## <a name="set-security-policies"></a>Définir des stratégies de sécurité
Vous pouvez configurer des stratégies de sécurité pour chaque abonnement. toomodify une stratégie de sécurité, vous devez être propriétaire ou contributeur de cet abonnement. Connectez-vous à toohello portail Azure et suivez hello qui suit les étapes de stratégies de sécurité de tooconfigure dans le centre de sécurité :

1. Cliquez sur hello **stratégie** vignette dans le tableau de bord de centre de sécurité hello.
2. Dans le panneau de la stratégie de sécurité hello qui s’ouvre, sélectionnez l’abonnement hello sur lequel vous souhaitez la stratégie de sécurité tooenable hello.

    ![Définition de stratégie](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Hello **stratégie de sécurité** panneau pour l’abonnement de hello sélectionné s’ouvre avec un ensemble d’options. Hello les options disponibles dans ce panneau sont :

   * **Stratégie de prévention de**: utiliser des stratégies de tooconfigure cette option par abonnement.  
   * **Notification par courrier électronique**: utilisez cette tooconfigure option une notification par courrier électronique qui est envoyée sur hello première quotidienne d’une alerte et des alertes de gravité élevée. Les préférences de courrier électronique peuvent être configurées uniquement pour les stratégies d’abonnement. Lecture [fournissent des détails de contact de sécurité dans le centre de sécurité Azure](security-center-provide-security-contact-details.md) pour plus d’informations sur la façon tooconfigure une notification par courrier électronique.
   * **Niveau de tarification**: utilisez cette hello de tooupgrade d’option Sélection du niveau de tarification. Consultez [tarification du centre de sécurité](security-center-pricing.md) toolearn plus sur les options de tarification.
4. Vérifiez que l’option **Collecter des données à partir des machines virtuelles** est définie sur **Activé**. Cette option active la collecte d’ouverture de session automatique pour les ressources nouvelles et existantes à l’aide de hello Microsoft Monitoring Agent – il s’agit de hello même agent utilisé par le service Operations Management Suite et Analytique de journal de hello. Données collectées à partir de cet agent sont stockées dans un espace de journal Analytique existant associé à votre abonnement Azure ou dans un nouvel espace, tenant geography hello de compte de hello machine virtuelle.

5. Bonjour **stratégie de sécurité** panneau, cliquez sur **stratégie de prévention de** toosee hello options disponibles. Cliquez sur **sur** tooenable les recommandations de sécurité hello qui sont pertinentes pour cet abonnement.

    ![Sélectionner des stratégies de sécurité hello](./media/security-center-policies/security-center-policies-fig7.png)

Utilisation de chaque option hello tableau comme un toounderstand de référence suivant :

| Stratégie | Lorsque l’option est activée |
| --- | --- |
| Mises à jour système |Une liste quotidienne des mises à jour de sécurité et critiques disponibles est récupérée à partir de Windows Update ou de Windows Server Update Services. liste récupérée de Hello dépend du service hello qui est configuré pour cette machine virtuelle et recommande que les mises à jour manquantes hello soient appliquées. Pour les systèmes Linux, stratégie de hello utilise hello packages fourni par le distributeur gestion système toodetermine packages qui ont des mises à jour disponibles. Elle vérifie également la disponibilité des mises à jour de sécurité et critiques à partir des machines virtuelles des [Services cloud Azure](../cloud-services/cloud-services-how-to-configure.md). |
| Vulnérabilités du système d’exploitation |Analyse le système d’exploitation configurations quotidienne toodetermine problèmes qui pourraient rendre tooattack vulnérable de machine virtuelle hello. stratégie de Hello recommande également ces vulnérabilités tooaddress des modifications de configuration. Consultez hello [liste des lignes de base recommandées](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) pour plus d’informations sur les configurations spécifiques hello qui sont en cours d’analyse. (À ce stade, Windows Server 2016 n'est pas entièrement pris en charge.) |
| Protection du point de terminaison |Vous recommande de toobe de protection de point de terminaison configuré pour tous les ordinateurs de virtuels Windows toohelp identifier et supprimer les virus, logiciels espions et autres logiciels malveillants. |
| Chiffrement de disque |Recommande d’activer le chiffrement de disque toutes les machines virtuelles tooenhance protection de données au repos. |
| groupes de sécurité réseau ; |Vous recommande [groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) être configuré toocontrol entrant et sortant du trafic tooVMs qui ont des points de terminaison publics. Les groupes de sécurité réseau configurés pour un sous-réseau sont hérités par toutes les interfaces réseau de machine virtuelle, sauf indication contraire. En outre toochecking qu’un groupe de sécurité réseau a été configuré, cette stratégie évalue les règles de tooidentify de règles de sécurité de trafic entrant qui autorisent le trafic entrant. |
| Pare-feu d’application web |Vous recommande de configurer un pare-feu d’applications web sur des ordinateurs virtuels lorsque de hello suivantes est vraie : </br></br>[Adresse IP publique au niveau de l’instance](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP) est utilisé et les règles de sécurité de trafic entrant pour le groupe de sécurité réseau associé hello hello sont configurés tooallow accès tooport 80/443.</br></br>Équilibrage de la charge est utilisée et hello associée à l’équilibrage de charge et règles de traduction d’adresse réseau entrant sont configurés tooallow accès tooport 80/443. Pour plus d’informations, consultez [Prise en charge d’un équilibrage de charge par Azure Resource Manager](../load-balancer/load-balancer-arm.md). |
| Pare-feu de nouvelle génération |Étend les protections du réseau au-delà des groupes de sécurité réseau intégrés à Azure. Centre de sécurité détecte les déploiements pour lequel un pare-feu de la génération suivant est recommandée et activer tooprovision un équipement virtuel. |
| Audit SQL et détection des menaces |Recommande que l’audit d’accès tooAzure de base de données activée pour la conformité et en outre, la détection des menaces, fins de recherche avancée. |
| Chiffrement SQL |Recommande l’activation du chiffrement au repos pour votre base de données Azure SQL Database, ainsi que pour les sauvegardes associées et les fichiers journaux de transaction. Même si vos données font l’objet d’une violation de sécurité, elles ne seront pas lisibles. |
| Évaluation des vulnérabilités |Recommande d’installer une solution d’évaluation des vulnérabilités sur votre machine virtuelle. |
| Chiffrement du stockage |Cette fonctionnalité est actuellement disponible pour les objets blob et fichiers Azure. Après l’activation du chiffrement de service de stockage, seules les nouvelles données seront chiffrées et tous les fichiers existants dans ce compte de stockage resteront non chiffrés. |
| Accès réseau JIT |Lorsque juste-à-temps est activé, le centre de sécurité bloque le trafic entrant tooyour machines virtuelles Azure en créant une règle de groupe de sécurité réseau. Vous sélectionnez les ports hello sur hello VM toowhich le trafic entrant doit être verrouillé. Pour plus d’informations, consultez [Gérer l’accès Juste à temps à la machine virtuelle](https://docs.microsoft.com/azure/security-center/security-center-just-in-time). |

Après avoir configuré toutes les options, cliquez sur **OK** Bonjour **stratégie de sécurité** panneau qui comporte des recommandations de hello, puis cliquez sur **enregistrer** Bonjour **sécurité Stratégie** panneau qui a les paramètres initiaux hello.

> [!NOTE]
> Hello niveau tarifaire est toujours applicable pour le niveau de groupe de ressources hello. Pour plus d’informations, visitez hello [tarification](https://azure.microsoft.com/pricing/details/security-center/) page.
>
>

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment tooconfigure des stratégies de sécurité dans le centre de sécurité Azure. toolearn en savoir plus sur Azure Security Center, voir hello :

* [Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md). Découvrez comment tooplan et comprendre les considérations de conception hello tooadopt Azure Security Center.
* [Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md). Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Gestion et répond toosecurity les alertes dans Azure Security Center](security-center-managing-and-responding-alerts.md). Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md). Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [FAQ du Centre de sécurité Azure](security-center-faq.md). Trouver des questions fréquemment posées sur l’utilisation du service de hello.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/). accédez à des billets de blog sur la sécurité et la conformité Azure.
