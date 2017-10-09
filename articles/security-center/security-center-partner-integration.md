---
title: "intégration aaaPartner dans le centre de sécurité Azure | Documents Microsoft"
description: "En savoir plus sur la façon dont Azure Security Center s’intègre aux partenaires tooenhance sécurité globale de vos ressources Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Intégration des partenaires dans Azure Security Center

Dans cet article, nous décrivons comment Azure Security Center s’intègre avec les partenaires toohelp vous améliorez la sécurité globale. Centre de sécurité offre une expérience intégrée dans Azure et tire parti de hello Azure Marketplace pour le partenaire de certification et facturation.

> [!NOTE] 
> À compter de juin 2017, centre de sécurité utilise des données de toocollect et le magasin de Microsoft Monitoring Agent hello. Pour plus d’informations, consultez l’article [Migration de plateforme Azure Security Center](security-center-platform-migration.md). informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>Pourquoi déployer des solutions de partenaire à partir de Security Center ?

Intégration de partenaires quatre principales raisons tooleverage dans le centre de sécurité sont les suivantes :

- **Déploiement facile** : Déploiement d’une solution de partenaire en suivant hello recommandation du centre de sécurité est beaucoup plus facile. processus de déploiement Hello peut être entièrement automatisée à l’aide d’une topologie de réseau et le programme d’installation par défaut. Alternativement, les clients peuvent choisir une option semi-automatisée pour plus de flexibilité et de personnalisation.
- **Détections intégrées** : les événements de sécurité des solutions de partenaire sont automatiquement collectés, agrégés et affichés dans le cadre des alertes et des incidents de Security Center. Ces événements sont également fusionnés avec les détections des autres tooprovide sources des fonctionnalités de détection des menaces avancées.
- **Gestion et surveillance unifiées de l’intégrité** : Les clients peuvent utiliser toomonitor des événements de contrôle d’intégrité intégré toutes les solutions de partenaire en un coup de œil. Gestion de base est disponible, avec le programme d’installation tooadvanced d’accéder facilement à l’aide de solutions de partenaire hello.
- **Exporter tooSIEM**. Centre de sécurité tous les clients peuvent exporter et partenaire avertit en commun systèmes des informations de sécurité et de gestion des événements (SIEM) local tooon Format d’événement (CEF) à l’aide de l’intégration des journaux Azure (aperçu).


## <a name="partners-that-integrate-with-security-center"></a>Partenaires qui s’intègrent à Security Center

Pour le moment, Security Center s’intègre aux solutions suivantes :

- Endpoint protection ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec et [Microsoft Antimalware pour Azure Cloud Services et Machines Virtuelles](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- Pare-feu d’applications web ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets), [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- Pare-feu de nouvelle génération ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) et [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- Évaluation des vulnérabilités ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

Au fil du temps, le centre de sécurité développez nombre hello de partenaires au sein de ces catégories et ajouter de nouvelles catégories. 

## <a name="deploy-a-partner-solution"></a>Déploiement d’une solution de partenaire

Selon le programme d’installation de hello de votre environnement Azure et de la stratégie de sécurité hello que vous avez défini, le centre de sécurité peut recommander que vous déployez une solution de partenaires. Hello recommandation du centre de sécurité vous guide tout au long des processus de hello de sélectionner et d’installer une solution partenaire. Hello expérience globale de déploiement peut varier en fonction de type hello de solution et de partenaire que vous utilisez. Pour plus d’informations, consultez hello suivant des articles :

- [Installer Endpoint Protection](security-center-install-endpoint-protection.md)
- [Ajouter un pare-feu d’applications web](security-center-add-web-application-firewall.md)
- [Ajouter un pare-feu de nouvelle génération](security-center-add-next-generation-firewall.md)
- [Évaluation des vulnérabilités non installée](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>Gestion des solutions de partenaires

Après le déploiement, tooview informations sur hello d’intégrité de la solution de hello et effectuer des tâches de gestion de base, sur hello **centre de sécurité** panneau, sélectionnez hello **solutions de partenaire** option. Pour plus d’informations sur la gestion des solutions de partenaire dans Security Center, consultez [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md).

![Intégration des partenaires](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Prise en charge de Symantec endpoint protection est limitée toodiscovery. Aucune alerte d’intégrité n’est disponible.
>

## <a name="see-also"></a>Voir aussi

Dans cet article, vous avez appris comment toointegrate partenaire solutions dans le centre de sécurité Azure. toolearn en savoir plus sur le centre de sécurité, consultez hello suivant des articles :

* [Guide des opérations et de planification de Security Center](security-center-planning-and-operations-guide.md)
* [Gérer et répondre toosecurity des alertes dans le centre de sécurité](security-center-managing-and-responding-alerts.md)
* [Alertes de sécurité par type dans Security Center](security-center-alerts-type.md)
* [Surveillance de l’intégrité de la sécurité dans Security Center](security-center-monitoring.md). Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Surveillance des solutions de partenaires avec Security Center](security-center-partner-solutions.md). Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Questions fréquentes : Azure Security Center](security-center-faq.md). Obtenir elles sonttrop des réponses aux questions ayant trait à l’aide du service de hello.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/). accédez à des billets de blog sur la sécurité et la conformité Azure.
