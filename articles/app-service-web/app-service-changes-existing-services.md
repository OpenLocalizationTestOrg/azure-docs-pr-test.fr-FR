---
title: "aaaAzure du Service d’applications et son impact sur les services Azure existants"
description: "Explique comment hello nouveau Service d’application Azure et ses fonctionnalités avoir un impact sur les services existants dans Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Azure App Service et les services Azure existants
Cet article présente tooexisting de modifications hello services Azure dans le cadre de hello toobring de modifier simultanément plusieurs services Azure dans [Azure App Service](https://azure.microsoft.com/services/app-service/), une nouvelle offre intégrée.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Vue d'ensemble
[Azure App Service](https://azure.microsoft.com/services/app-service/) est un service de cloud de nouveaux et uniques qui permet aux développeurs toocreate applications web et mobiles pour n’importe quelle plateforme et de n’importe quel appareil. Service d’applications est qu'une solution intégrée conçue de toostreamline répétée fonctions codage, intégrer à l’entreprise et les systèmes de SaaS et automatiser des processus d’entreprise tout en respectant vos besoins de sécurité, fiabilité et l’évolutivité.

Service d’applications réunit hello suivant Azure existants services - [sites Web](https://azure.microsoft.com/services/websites/), [Services mobiles](https://azure.microsoft.com/services/mobile-services/), et [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) en un seul combinées service, tandis que Ajout de nouvelles fonctionnalités.  Service d’applications vous permet de hello toohost les types d’application suivants :

* Web Apps
* Mobile Apps
* Applications API
* Logic Apps

Hello tableau suivant explique comment les Azure services mappent tooApp hello application types de Service et disponibles dans celui-ci.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Service Azure existant</th>
<th align="left", style="width:10%">Azure App Service</th>
<th align="left", style="width:80%">Ce qui a changé</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Sites Web Azure</td>
<td align="left">Web Apps</td>
<td align="left"><li>Pour les sites Web Azure, du Service d’applications est strictement limité toochanging hello nom sites Web tooWeb applications.
<p><li>Toutes vos instances existantes de Sites Web s'appellent désormais Web Apps dans App Service.</p>
<p><li>Vous pouvez accéder à vos sites Web existants via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, où vous trouverez tous vos sites existants sous <em>Web Apps</em>.</p>
<p><li><em>Web Plan d’hébergement</em> est désormais <em>du Plan App Service</em>. Un <em>Plan App Service</em> peut héberger n’importe quel type d’application App Service (web, mobile, logique ou API).</p>
<p><li>Azure App Service Web Apps se trouve sous Disponibilité générale.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">En savoir plus sur les applications Web</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Azure Mobile Services</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Services mobiles continuer toobe disponible en tant que service autonome et restent entièrement pris en charge.</p>
<p><li>Applications mobiles est un type d’application dans le Service d’application, qui intègre toutes les fonctionnalités de hello des Services mobiles et bien plus encore.</p>
<p><li>Il est facile<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrer à partir des Services mobiles tooMobile applications</a>.</p>
<p><li>Dans le cadre d’App Service, les applications mobiles se voient offrir de nouvelles fonctionnalités allant au-delà des services mobiles, comme l’intégration aux systèmes locaux et SaaS, les emplacements intermédiaires, WebJobs, de meilleures options de mise à l’échelle, et bien plus encore.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">En savoir plus sur les applications mobiles</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API Apps</td>
<td align="left">
<p><li>Applications API est un nouveau type d’application dans le Service d’application qui vous permet de facilement créer et consommer des API dans le cloud de hello.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">En savoir plus sur les applications API</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Logic Apps</td>
<td align="left">
<p><li>Logic Apps est un nouveau type d’application d’App Service qui permet d’automatiser les processus d’entreprise.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">En savoir plus sur les applications de la logique de</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Azure BizTalk Services</td>
<td align="left">Applications API BizTalk</td>
<td align="left">
<li><p>Les Services BizTalk continuer toobe disponible en tant que service autonome et restent entièrement pris en charge.</p>
<li><p>Toutes les fonctions hello des Services BizTalk sont intégrées dans du Service d’applications en tant qu’applications API permettant aux utilisateurs tooperform intégration et des scénarios d’intégration B2B avec un des types d’application hello dans le Service d’applications.</p>
<li><p>Avec les applications de la logique, vous pouvez désormais automatiser des processus d’entreprise à l’aide d’un flux de travail de conception visuelle expérience toocreate.</p></td>
</tr>
</tbody>
</table>

toolearn plus, visitez [documentation du Service d’application](https://azure.microsoft.com/documentation/services/app-service/).

