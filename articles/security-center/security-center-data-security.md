---
title: "aaaAzure données de centre de sécurité | Documents Microsoft"
description: "Ce document explique comment les données sont gérées et protégées dans le Centre de sécurité Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Sécurité des données du Centre de sécurité Azure
les clients toohelp empêchent, détectent et répondent toothreats, Azure Security Center collecte et traite les données relatives à la sécurité, y compris les informations de configuration, métadonnées, journaux des événements, les fichiers de vidage sur incident et bien plus encore. Microsoft respecte les instructions de sécurité et de conformité toostrict : du codage toooperating un service.

Cet article explique comment les données sont gérées et protégées dans le Centre de sécurité Azure.

>[!NOTE] 
>À compter de début juin 2017, centre de sécurité utiliser hello Microsoft Monitoring Agent toocollect et stocker des données. Consultez [Migration de plateforme Azure Security Center](security-center-platform-migration.md) toolearn plus. informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>


## <a name="data-sources"></a>Sources de données
Azure Security Center analyse les données de hello suivant la visibilité de tooprovide sources dans votre état de sécurité, identifier les failles et recommander des solutions d’atténuation et détecter les menaces actives :

- Les Services Azure : Utilise les informations sur la configuration de hello des services Azure que vous avez déployé en communiquant avec le fournisseur de ressources du service.
- Trafic réseau : tire parti des métadonnées de trafic réseau échantillonnées provenant de l’infrastructure de Microsoft, telles que l’IP/le port source/de destination, la taille de paquet et le protocole réseau.
- Solutions de partenaires : collecte les alertes de sécurité des solutions de partenaires intégrées, telles que les solutions de pare-feu et anti-programme malveillant. 
- Vos machines virtuelles et vos serveurs : utilise les informations de configuration et les données relatives aux événements de sécurité, telles que les journaux des événements Windows et les journaux d’audit, les journaux IIS, les messages syslog et les fichiers de vidage sur incident, qui figurent sur vos machines virtuelles. En outre, lorsqu’une alerte est créée, centre de sécurité Azure peut générer un instantané du disque de machine virtuelle hello affecté et extraire l’alerte de machine artefacts toohello connexes à partir du disque de machine virtuelle hello, tel qu’un fichier de Registre, à des fins légales.


## <a name="data-protection"></a>Protection des données
**La segmentation des données**: données sont maintenues séparées logiquement sur chaque composant dans le service de hello. Toutes les données sont balisées en fonction de l'organisation. Ce balisage est conservé tout au long du cycle de vie des données hello, et elle est appliquée à chaque couche de service de hello.

**Accès aux données**: pouvoir tooprovide recommandations de sécurité et examiner les menaces de sécurité potentielles, technique de Microsoft peut accéder aux informations collectées ou analysés par des services Azure, y compris les fichiers de vidage sur incident, traiter les événements de création, machine virtuelle instantanés de disque et les artefacts, qui peuvent inclure involontairement des données personnelles à vos machines virtuelles ou des données client. Nous respecter toohello [déclaration de confidentialité et les termes du contrat de Services en ligne Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), état que Microsoft ne sera pas utiliser les données clients ou dériver des informations à partir de celle-ci à des fins commerciales de publicité ou similaires. Nous utilisent uniquement les données client comme requis tooprovide vous avec Azure services, y compris à des fins compatible avec la fourniture de ces services. Vous conservez tous les droits tooCustomer données.

**Utilisation des données**: Microsoft utilise des modèles et menaces vu sur plusieurs locataires tooenhance nos fonctions de détection et la prévention ; nous faire conformément aux engagements de confidentialité hello décrites dans nos [confidentialité Instruction](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Emplacement des données

**Votre espace**: un espace de travail est spécifié pour hello suivant l’Union européenne, et les données collectées à partir de vos machines virtuelles Azure, y compris les vidages sur incident et certains types de données d’alerte, sont stockées dans hello plus proche de l’espace de travail. 

| Zone géographique de machine virtuelle                        | Zone géographique d’espace de travail |
|-------------------------------|---------------|
| États-Unis, Brésil, Canada | États-Unis |
| Europe, Royaume-Uni        | Europe        |
| Asie-Pacifique, Japon, Inde    | Asie-Pacifique  |
| Australie                     | Australie     |

 
Instantanés de disque de machine virtuelle sont stockés dans hello même compte de stockage comme disque de machine virtuelle hello.
 
Pour les ordinateurs virtuels et les serveurs exécutant d’autres environnements, par exemple, sur site, vous pouvez spécifier les espace de travail hello et région où les données collectées sont stockées. 

**Stockage du centre de sécurité Azure**: plus d’informations sur les alertes de sécurité, y compris les alertes de partenaire, sont stockés régional selon l’emplacement toohello Hello liées ressource Azure, tandis que plus d’informations sur l’état d’intégrité de la sécurité et recommandation stockée de façon centralisée dans hello États-Unis ou Europe selon l’emplacement de toocustomer.
Le Centre de sécurité Azure collecte des copies éphémères de vos fichiers de vidage sur incident et les analyse pour obtenir des preuves de tentatives d’attaque par le biais de code malveillant exploitant une faille de sécurité et de compromis ayant abouti. Centre de sécurité Azure effectue cette analyse dans hello même emplacement que hello d’espace de travail, et suppressions hello copies éphémères lors de l’analyse est terminée.

Artefacts de l’ordinateur sont stockées de manière centralisée dans hello même région que hello de machine virtuelle. 


## <a name="managing-data-collection-from-virtual-machines"></a>Gestion de la collecte de données à partir de machines virtuelles

Lorsque vous activez Security Center dans Azure, la collecte de données est activée pour chacun de vos abonnements Azure. Vous pouvez également activer la collecte de données pour vos abonnements Bonjour section de stratégie de sécurité du centre de sécurité Azure. Lors de la collecte de données est activée, Azure Security Center dispositions hello Microsoft Monitoring Agent sur toutes les existantes prise en charge des machines virtuelles et nouveaux qui sont créés. Hello Microsoft Monitoring agent analyses de sécurité différentes configurations et des événements liées dans [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) traces (ETW). En outre, système d’exploitation de hello déclenche des événements du journal des événements pendant hello machine de hello en cours d’exécution. Il peut s’agir des données suivantes : type et version de système d’exploitation, journaux de système d’exploitation (journaux d’événements Windows), processus en cours d’exécution, nom de machine, adresses IP, utilisateur connecté et ID de locataire. Hello Microsoft Monitoring Agent lit les entrées de journal des événements et ETW effectue le suivi et les copie espace tooyour pour l’analyse. Hello Microsoft Monitoring Agent copie également l’espace de tooyour de fichiers de vidage sur incident.

Si vous utilisez le centre de sécurité Azure gratuit, vous pouvez également désactiver la collecte de données à partir d’ordinateurs virtuels dans hello stratégie de sécurité. Collecte de données est requise pour les abonnements sur le niveau Standard de hello. La collecte des artefacts et des captures instantanées des disques de machine virtuelle reste activée, même si la collecte de données est désactivée.


## <a name="see-also"></a>Voir aussi
Ce document explique comment les données sont gérées et protégées dans le Centre de sécurité Azure. toolearn en savoir plus sur Azure Security Center, consultez :

* [Azure Security Center Guide de planification et opérations](security-center-planning-and-operations-guide.md) — Découvrez comment tooplan et comprendre les considérations de conception hello tooadopt Azure Security Center.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) — Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.
