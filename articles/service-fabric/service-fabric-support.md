---
title: "aaaLearn sur les options de prise en charge de l’infrastructure de Service Azure | Documents Microsoft"
description: Versions du cluster Service Fabric Azure pris en charge et des liens de tickets de support toofile
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 42394e2cd9dad2040d37d3a2ff3600ee040d8720
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-support-options"></a>Options de support d’Azure Service Fabric

prise en charge toodeliver hello approprié pour vos clusters Service Fabric que vous exécutez votre travail de l’application se charge, nous avons mis en place différentes options pour vous. Varie en fonction de hello au niveau de prise en charge et gravité hello du problème de hello, vous obtenez toopick hello droite options. 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>Signaler des problèmes de site en ligne ou en production ou demander un support payant pour Azure

Pour signaler des problèmes de site en ligne sur votre cluster Service Fabric déployé sur Azure, ouvrez un ticket de support professionnel [sur le Portail Azure](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) ou le [portail de support Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Pour en savoir plus :
 
- [Support professionnel Microsoft pour Azure](https://azure.microsoft.com/en-us/support/plans/?b=16.44).
- [Support Premier Microsoft](https://support.microsoft.com/en-us/premier).

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>Signaler des problèmes de site en ligne ou en production ou demander un support payant pour des clusters Service Fabric autonomes

Pour signaler des problèmes de site en ligne sur votre cluster Service Fabric déployé localement ou sur d’autres clouds, ouvrez un ticket de support professionnel sur le [portail de support technique Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Pour en savoir plus :

- [Support professionnel Microsoft local](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
- [Support Premier Microsoft](https://support.microsoft.com/en-us/premier).


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>Signaler des problèmes avec Azure Service Fabric 
Nous avons défini un référentiel GitHub pour signaler les problèmes de Service Fabric.  Nous sommes également surveillez hello suivant des forums.

### <a name="github-repo"></a>Référentiel GitHub 
Signaler des problèmes avec Azure Service Fabric sur le [Référentiel Git des problèmes de Service Fabric](https://github.com/Azure/service-fabric-issues). Ce référentiel est destiné au signalement et au suivi des problèmes rencontrés avec Azure Service Fabric, ainsi qu’aux demandes de petites fonctionnalités. **N’utilisez pas les problèmes de ce site live tooreport**.

### <a name="stackoverflow-and-msdn-forums"></a>Forums StackOverflow et MSDN

Hello [balise Service Fabric sur StackOverflow] [ stackoverflow] et hello [forum Service Fabric sur MSDN] [ msdn-forum] est recommandé d’utiliser pour poser des questions sur fonctionne de la plateforme de hello et comment vous pouvez accomplir certaines tâches avec lui.

### <a name="azure-feedback-forum"></a>Forum de commentaires Azure

Hello [Forum de commentaires de Azure pour Service Fabric] [ uservoice-forum] est hello meilleur endroit pour l’envoi des idées de fonctionnalité big qu’au produit de hello nous allons examiner les requêtes les plus populaires hello font partie de notre support toolong à long terme planification. Nous vous conseillons de prise en charge de toorally de vos suggestions au sein de la Communauté de hello.


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>Versions de Service Fabric prises en charge.

Veillez à ce que votre cluster exécute toujours une version prise en charge de Service Fabric. Et, lorsque nous annoncer version hello d’une nouvelle version de l’infrastructure de Service, version précédente de hello est marquée pour la fin de la prise en charge un minimum de 60 jours à partir de cette date. Hello nouvelles versions sont annoncées [sur le blog de l’équipe Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/).

Consultez toohello suivant des documents de plus d’informations sur la façon de tookeep votre cluster exécutant une version prise en charge de l’infrastructure de Service.

- [Mettre à niveau la version de Service Fabric sur un cluster Azure](service-fabric-cluster-upgrade.md)
- [Mettre à niveau la version de Service Fabric sur un cluster de serveurs Windows autonome](service-fabric-cluster-upgrade-windows-server.md)
 
Voici la liste hello des versions de Service Fabric hello qui sont prises en charge et leur date de fin de prise en charge.

| **Cluster runtime Service Fabric** | **Kit de développement logiciel compatible / Versions de package NuGet** | **Date de fin de prise en charge** |
| --- | --- | --- |
| Tous les too5.3.121 de précédentes versions de cluster |Inférieur ou égale tooversion 2.3 |20 janvier 2017 |
| 5.3.* |Inférieur ou égale tooversion 2.3 |24 février 2017 |
| 5.4.* |Inférieur ou égale tooversion 2.4 |10 mai 2017     |
| 5.5.* |Inférieur ou égale tooversion 2.5 |10 août 2017    |
| 5.6.* |Inférieur ou égale tooversion 2.6 |13 octobre 2017    |
| 5.7.* |Inférieur ou égale tooversion 2.7 |Version actuelle ; par conséquent, pas de date de fin

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Versions préliminaires de Service Fabric – non pris en charge pour la production.
À partir de tootime de temps, nous diffuserons de versions qui ont des fonctionnalités importantes, que nous souhaitons vos commentaires, qui sont publiées sous forme d’aperçu. Ces versions préliminaires doivent uniquement être utilisées à des fins de test. Votre cluster de production doit toujours exécuter une version de Service Fabric prise en charge et stable. Les versions préliminaires commencent toujours par un numéro de version majeure et mineure : 255. Par exemple, si vous voyez un Service Fabric version 255.255.5703.949, cette version de release est toobe uniquement utilisés dans des clusters de test et est en version préliminaire. Ces versions préliminaires sont également annoncées sur hello [blog de l’équipe Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric) et avoir plus d’informations sur les fonctionnalités de hello incluses.

Il n’existe aucune option de support technique payant pour ces versions préliminaires. Utilisez une des options de hello répertoriées sous [rapport Azure Service Fabric émet](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues) tooask questions ou fournir des commentaires.

## <a name="next-steps"></a>Étapes suivantes

- [Mettre à niveau la version de Service Fabric sur un cluster Azure](service-fabric-cluster-upgrade.md)
- [Mettre à niveau la version de Service Fabric sur un cluster de serveurs Windows autonome](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
