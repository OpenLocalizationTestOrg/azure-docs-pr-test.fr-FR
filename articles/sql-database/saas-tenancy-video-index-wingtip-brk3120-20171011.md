---
title: "Vidéo indexée, application SQL SaaS Azure | Microsoft Docs"
description: "Cet article indexe plusieurs points de temps dans notre vidéo de 81 minutes sur la conception de l’application de location de bases de données SaaS, depuis la conférence Ignite qui s’est tenue le 11 octobre 2017. Vous pouvez directement à la partie qui vous intéresse. Au moins 3 modèles sont décrits. Fonctionnalités Azure qui simplifient le développement et la gestion sont décrites."
ms.custom: 
ms.date: 12/06/2017
ms.prod: sql-server
ms.reviewer: billgib
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db47d1dd0a6114ebca0715da179cc0629b26781a
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/07/2017
---
# <a name="video-indexed-and-annotated-for-mulit-tenant-saas-app-using-azure-sql-database"></a>Vidéo indexée et annotée pour l’application SaaS multi-locataire à l’aide d’Azure SQL Database

Cet article est un index annoté dans les emplacements de temps d’une vidéo de 81 minutes sur les modèles ou motifs de location SaaS. Cet article vous permet de faire défiler la vidéo en avant ou en arrière jusqu’à la partie qui vous intéresse. La vidéo explique les options de conception importantes pour une application de base de données multi-locataire sur Azure SQL Database. La vidéo inclut des démonstrations, des guides de code de gestion et propose des informations plus détaillées par l’expérience que notre documentation écrite.

La vidéo amplifie les informations de notre documentation écrite, par exemple : 
- *Conceptuelles :* [modèles de location de base de données SaaS multi-locataire][saas-concept-design-patterns-563e]
- *Didacticiels :* [l’application SaaS Wingtip Tickets][saas-how-welcome-wingtip-app-679t]

La vidéo et les articles décrivent les différentes phases de création d’une application multi-locataire sur Azure SQL Database dans le cloud. Des fonctionnalités spéciales de Azure SQL Database facilitent le développement et la mise en œuvre des applications multi-locataires, toutes les deux plus faciles à gérer et performantes en toute confiance.

Nous mettons à jour régulièrement notre documentation écrite. La vidéo n’est pas modifiée ni mise à jour, par conséquent, davantage d’informations peuvent devenir obsolètes.



## <a name="sequence-of-38-time-indexed-screenshots"></a>Séquence de 38 captures d’écran temporellement indexées

Cette section indexe l’emplacement de temps de 38 discussions à travers la vidéo de 81 minutes. Chaque index de temps est annoté avec une capture d’écran de la vidéo et parfois avec des informations supplémentaires.

Chaque index de temps est au format *h:mm:ss*. Par exemple, le deuxième emplacement de temps indexé, étiqueté **Objectifs des sessions**, démarre à l’emplacement de temps approximatif de **0:03:11**.


### <a name="compact-links-to-video-indexed-time-locations"></a>Compacter des liens vers les emplacements de temps indexés de la vidéo

Les titres suivants sont des liens vers leurs sections annotées correspondantes plus loin dans cet article :

- [1. **(Début)** Diapositive d’accueil, 0:00:03](#anchor-image-wtip-min00001)
- [2. Objectifs des sessions, 0:03:11](#anchor-image-wtip-min00311)
- [3. Agenda, 0:04:17](#anchor-image-wtip-min00417)
- [4. Application web multi-locataire, 0:05:05](#anchor-image-wtip-min00505)
- [5. Formulaire web d’application en action, 0:05:55](#anchor-image-wtip-min00555)
- [6. Coût par locataire (mise à l’échelle, isolation, récupération), 0:09:31](#anchor-image-wtip-min00931)
- [7. Modèles de bases de données pour multi-locataire : pour et contre, 0:11:59](#anchor-image-wtip-min01159)
- [8. Le modèle hybride mélange des avantages de MT/ST, 0:13:01](#anchor-image-wtip-min01301)
- [9. Locataire unique contre multi-locataire : pour et contre, 0:16:44](#anchor-image-wtip-min01644)
- [10. Les pools sont rentables pour des charges de travail non prévisibles, 0:19:36](#anchor-image-wtip-min01936)
- [11. Démonstration de ST/MT de base de données par locataire et hybrides, 0:20:08](#anchor-image-wtip-min02008)
- [12. Formulaire d’application en direct affichant Dojo, 0:20:29](#anchor-image-wtip-min02029)
- [13. MYOB et pas une DBA en vue, 0:28:54](#anchor-image-wtip-min02854)
- [14. Exemple d’utilisation de pool élastique MYOB, 0:29:40](#anchor-image-wtip-min02940)
- [15. En savoir plus sur MYOB et autres ISV, 0:31:36](#anchor-image-wtip-min03136)
- [16. Modèles composés en scénarios SaaS E2E, 0:43:15](#anchor-image-wtip-min04315)
- [17. Application SaaS multi-locataire hybride Canonical, 0:47:33](#anchor-image-wtip-min04733)
- [18. Application exemple SaaS Wingtip, 0:48:10](#anchor-image-wtip-min04810)
- [19. Scénarios et modèles explorés dans les didacticiels, 0:49:10](#anchor-image-wtip-min04910)
- [20. Démonstration de didacticiels et référentiel Github, 0:50:18](#anchor-image-wtip-min05018)
- [21. Réf Github Microsoft/WingtipSaaS, 0:50:38](#anchor-image-wtip-min05038)
- [22. Exploration des modèles, 0:56:20](#anchor-image-wtip-min05620)
- [23. Approvisionnement de locataires et intégration, 0:57:44](#anchor-image-wtip-min05744)
- [24. Approvisionnement de locataires et connexion d’application, 0:58:58](#anchor-image-wtip-min05858)
- [25. Démonstration de scripts de gestion approvisionnant un locataire unique, 0:59:43](#anchor-image-wtip-min05943)
- [26. PowerShell pour approvisionner et cataloguer, 1:00:02](#anchor-image-wtip-min10002)
- [27. T-SQL SELECT * FROM TenantsExtended, 1:03:30](#anchor-image-wtip-min10330)
- [28. Gestion des charges de travail de locataire imprévisibles, 1:04:36](#anchor-image-wtip-min10436)
- [29. Surveillance du pool élastique, 1:06:39](#anchor-image-wtip-min10639)
- [30. Surveillance de la génération et des performances de charge, 1:09:42](#anchor-image-wtip-min10942)
- [31. Gestion des schémas à l’échelle, 1:10:33](#anchor-image-wtip-min11033)
- [32. Requête distribuée dans des bases de données de locataire, 1:12:21](#anchor-image-wtip-min11221)
- [33. Démonstration de la génération de tickets, 1:12:32](#anchor-image-wtip-min11232)
- [34. Analyse ad hoc SSMS, 1:12:46](#anchor-image-wtip-min11246)
- [35. Extraire les données de locataire dans DW SQL, 1:16:32](#anchor-image-wtip-min11632)
- [36. Graph de la distribution des ventes quotidiennes, 1:16:48](#anchor-image-wtip-min11648)
- [37. Conclusion et instructions, 1:19:52](#anchor-image-wtip-min11952)
- [38. Ressources pour plus d’informations, 1:20:42](#anchor-image-wtip-min12042)


&nbsp;

### <a name="annotated-index-time-locations-in-the-video"></a>Emplacements du temps d’index annoté dans la vidéo

Cliquer sur une image de la capture d’écran vous permet d’extraire l’emplacement de temps dans la vidéo.


&nbsp;<a name="anchor-image-wtip-min00001"/>
#### <a name="1-start-welcome-slide-00001"></a>1. *(Début)* Diapositive d’accueil, 0:00:01

*En savoir plus sur MYOB : concevoir des modèles pour des applications SaaS sur Azure SQL Database - BRK3120*

[![Diapositive d’accueil][image-wtip-min00003-brk3120-whole-welcome]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1)

- Titre : En savoir plus sur MYOB : concevoir des modèles pour des applications SaaS sur Azure SQL Database
- Bill.Gibson@microsoft.com
- Gestionnaire du programme principal, Azure SQL Database
- Session Microsoft Ignite BRK3120, Orlando, FL USA, 11 octobre 2017


&nbsp;<a name="anchor-image-wtip-min00311"/>
#### <a name="2-session-objectives-00153"></a>2. Objectifs des sessions, 0:01:53
[![Objectifs des sessions][image-wtip-min00311-session]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=113)

- Modèles alternatifs pour des applications multi-locataire, avec pour et contre.
- Modèles SaaS pour réduire le développement, la gestion et les coûts de ressource.
- Une application + scripts en exemple.
- Fonctionnalités SaaS + modèles SaaS font de SQL Database une plateforme de données hautement évolutive et rentable pour des SaaS multi-locataire.


&nbsp;<a name="anchor-image-wtip-min00417"/>
#### <a name="3-agenda-00409"></a>3. Agenda, 0:04:09
[![Agenda][image-wtip-min00417-agenda]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=249)


&nbsp;<a name="anchor-image-wtip-min00505"/>
#### <a name="4-multi-tenant-web-app-00500"></a>4. Application web multi-locataire, 0:05:00
[![Application Wingtip SaaS : application web multi-locataire][image-wtip-min00505-web-app]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=300)


&nbsp;<a name="anchor-image-wtip-min00555"/>
#### <a name="5-app-web-form-in-action-00539"></a>5. Formulaire web d’application en action, 0:05:39
[![Formulaire web d’application en action][image-wtip-min00555-app-web-form]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=339)


&nbsp;<a name="anchor-image-wtip-min00931"/>
#### <a name="6-per-tenant-cost-scale-isolation-recovery-00658"></a>6. Coût par locataire (mise à l’échelle, isolation, récupération), 0:06:58
[![Coût par locataire, mise à l’échelle, isolation, récupération][image-wtip-min00931-per-tenant-cost]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=418)


&nbsp;<a name="anchor-image-wtip-min01159"/>
#### <a name="7-database-models-for-multi-tenant-pros-and-cons-00952"></a>7. Modèles de bases de données pour multi-locataire : pour et contre, 0:09:52
[![Modèles de bases de données pour multi-locataire : pour et contre][image-wtip-min01159-db-models-pros-cons]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=592)


&nbsp;<a name="anchor-image-wtip-min01301"/>
#### <a name="8-hybrid-model-blends-benefits-of-mtst-01229"></a>8. Le modèle hybride mélange des avantages de MT/ST, 0:12:29
[![Le modèle hybride mélange des avantages de MT/ST][image-wtip-min01301-hybrid]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=749)


&nbsp;<a name="anchor-image-wtip-min01644"/>
#### <a name="9-single-tenant-vs-multi-tenant-pros-and-cons-01311"></a>9. Locataire unique contre multi-locataire : pour et contre, 0:13:11
[![Locataire unique contre multi-locataire : pour et contre][image-wtip-min01644-st-vs-mt]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=791)


&nbsp;<a name="anchor-image-wtip-min01936"/>
#### <a name="10-pools-are-cost-effective-for-unpredictable-workloads-01749"></a>10. Les pools sont rentables pour des charges de travail non prévisibles, 0:17:49
[![Les pools sont rentables pour des charges de travail non prévisibles][image-wtip-min01936-pools-cost]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1069)


&nbsp;<a name="anchor-image-wtip-min02008"/>
#### <a name="11-demo-of-database-per-tenant-and-hybrid-stmt-01959"></a>11. Démonstration de ST/MT de base de données par locataire et hybrides, 0:19:59
[![Démonstration de ST/MT de base de données par locataire et hybrides][image-wtip-min02008-demo-st-hybrid]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1199)


&nbsp;<a name="anchor-image-wtip-min02029"/>
#### <a name="12-live-app-form-showing-dojo-02010"></a>12. Formulaire d’application en direct affichant Dojo, 0:20:10
[![Formulaire d’application en direct affichant Dojo][image-wtip-min02029-live-app-form-dojo]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1210)

&nbsp;<a name="anchor-image-wtip-min02854"/>
#### <a name="13-myob-and-not-a-dba-in-sight-02506"></a>13. MYOB et pas une DBA en vue, 0:25:06
[![MYOB et pas une DBA en vue][image-wtip-min02854-myob-no-dba]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1506)


&nbsp;<a name="anchor-image-wtip-min02940"/>
#### <a name="14-myob-elastic-pool-usage-example-02930"></a>14. Exemple d’utilisation de pool élastique MYOB, 0:29:30
[![Exemple d’utilisation de pool élastique MYOB][image-wtip-min02940-myob-elastic]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1770)


&nbsp;<a name="anchor-image-wtip-min03136"/>
#### <a name="15-learning-from-myob-and-other-isvs-03125"></a>15. En savoir plus sur MYOB et autres ISV, 0:31:25
[![En savoir plus sur MYOB et autres ISV][image-wtip-min03136-learning-isvs]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1885)


&nbsp;<a name="anchor-image-wtip-min04315"/>
#### <a name="16-patterns-compose-into-e2e-saas-scenario-03142"></a>16. Modèles composés en scénarios SaaS E2E, 0:31:42
[![Modèles composés en scénarios SaaS E2E][image-wtip-min04315-patterns-compose]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1902)


&nbsp;<a name="anchor-image-wtip-min04733"/>
#### <a name="17-canonical-hybrid-multi-tenant-saas-app-04604"></a>17. Application SaaS multi-locataire hybride Canonical, 0:46:04
[![Application SaaS multi-locataire hybride Canonical][image-wtip-min04733-canonical-hybrid]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=2764)


&nbsp;<a name="anchor-image-wtip-min04810"/>
#### <a name="18-wingtip-saas-sample-app-04801"></a>18. Application exemple SaaS Wingtip, 0:48:01
[![Application exemple SaaS Wingtip][image-wtip-min04810-wingtip-saas-app]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=2881)


&nbsp;<a name="anchor-image-wtip-min04910"/>
#### <a name="19-scenarios-and-patterns-explored-in-the-tutorials-04900"></a>19. Scénarios et modèles explorés dans les didacticiels, 0:49:00
[![Scénarios et modèles explorés dans les didacticiels][image-wtip-min04910-scenarios-tutorials]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=2940)


&nbsp;<a name="anchor-image-wtip-min05018"/>
#### <a name="20-demo-of-tutorials-and-github-repository-05012"></a>20. Démonstration de didacticiels et référentiel Github, 0:50:12
[![Démonstration de didacticiels et réf Github][image-wtip-min05018-demo-tutorials-github]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3012)


&nbsp;<a name="anchor-image-wtip-min05038"/>
#### <a name="21-github-repo-microsoftwingtipsaas-05032"></a>21. Réf Github Microsoft/WingtipSaaS, 0:50:32
[![Réf Github Microsoft/WingtipSaaS][image-wtip-min05038-github-wingtipsaas]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3032)


&nbsp;<a name="anchor-image-wtip-min05620"/>
#### <a name="22-exploring-the-patterns-05615"></a>22. Exploration des modèles, 0:56:15
[![Exploration des modèles][image-wtip-min05620-exploring-patterns]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3375)


&nbsp;<a name="anchor-image-wtip-min05744"/>
#### <a name="23-provisioning-tenants-and-onboarding-05619"></a>23. Approvisionnement de locataires et intégration, 0:56:19
[![Approvisionnement de locataires et intégration][image-wtip-min05744-provisioning-tenants-onboarding-1]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3379)


&nbsp;<a name="anchor-image-wtip-min05858"/>
#### <a name="24-provisioning-tenants-and-application-connection-05752"></a>24. Approvisionnement de locataires et connexion d’application, 0:57:52
[![Approvisionnement de locataires et connexion d’application][image-wtip-min05858-provisioning-tenants-app-connection-2]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3472)


&nbsp;<a name="anchor-image-wtip-min05943"/>
#### <a name="25-demo-of-management-scripts-provisioning-a-single-tenant-05936"></a>25. Démonstration de scripts de gestion approvisionnant un locataire unique, 0:59:36
[![Démonstration de scripts de gestion approvisionnant un locataire unique][image-wtip-min05943-demo-management-scripts-st]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3576)


&nbsp;<a name="anchor-image-wtip-min10002"/>
#### <a name="26-powershell-to-provision-and-catalog-05956"></a>26. PowerShell pour approvisionner et cataloguer, 0:59:56
[![PowerShell pour approvisionner et cataloguer][image-wtip-min10002-powershell-provision-catalog]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3596)


&nbsp;<a name="anchor-image-wtip-min10330"/>
#### <a name="27-t-sql-select--from-tenantsextended-10325"></a>27. T-SQL SELECT * FROM TenantsExtended, 1:03:25
[![T-SQL SELECT * FROM TenantsExtended][image-wtip-min10330-sql-select-tenantsextended]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3805)


&nbsp;<a name="anchor-image-wtip-min10436"/>
#### <a name="28-managing-unpredictable-tenant-workloads-10334"></a>28. Gestion des charges de travail de locataire imprévisibles, 1:03:34
[![Gestion des charges de travail de locataire imprévisibles][image-wtip-min10436-managing-unpredictable-workloads]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3814)


&nbsp;<a name="anchor-image-wtip-min10639"/>
#### <a name="29-elastic-pool-monitoring-10632"></a>29. Surveillance du pool élastique, 1:06:32
[![Surveillance du pool élastique][image-wtip-min10639-elastic-pool-monitoring]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=3992)


&nbsp;<a name="anchor-image-wtip-min10942"/>
#### <a name="30-load-generation-and-performance-monitoring-10937"></a>30. Surveillance de la génération et des performances de charge, 1:09:37
[![Surveillance de la génération et des performances de charge][image-wtip-min10942-load-generation]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=4117)


&nbsp;<a name="anchor-image-wtip-min11033"/>
#### <a name="31-schema-management-at-scale-10940"></a>31. Gestion des schémas à l’échelle, 1:09:40
[![Gestion des schémas à l’échelle][image-wtip-min11033-schema-management-scale]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=34120)


&nbsp;<a name="anchor-image-wtip-min11221"/>
#### <a name="32-distributed-query-across-tenant-databases-11118"></a>32. Requête distribuée dans des bases de données de locataire, 1:11:18
[![Requête distribuée dans des bases de données de locataire][image-wtip-min11221-distributed-query]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=4278)


&nbsp;<a name="anchor-image-wtip-min11232"/>
#### <a name="33-demo-of-ticket-generation-11228"></a>33. Démonstration de la génération de tickets, 1:12:28
[![Démonstration de la génération de tickets][image-wtip-min11232-demo-ticket-generation]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=4348)


&nbsp;<a name="anchor-image-wtip-min11246"/>
#### <a name="34-ssms-adhoc-analytics-11235"></a>34. Analyse ad hoc SSMS, 1:12:35
[![Analyse ad hoc SSMS][image-wtip-min11246-ssms-adhoc-analytics]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=4355)


&nbsp;<a name="anchor-image-wtip-min11632"/>
#### <a name="35-extract-tenant-data-into-sql-dw-11546"></a>35. Extraire les données de locataire dans DW SQL, 1:15:46
[![Extraire les données de locataire dans DW SQL][image-wtip-min11632-extract-tenant-data-sql-dw]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=4546)


&nbsp;<a name="anchor-image-wtip-min11648"/>
#### <a name="36-graph-of-daily-sale-distribution-11638"></a>36. Graph de la distribution des ventes quotidiennes, 1:16:38
[![Graph de la distribution des ventes quotidiennes][image-wtip-min11648-graph-daily-sale-distribution]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=4598)


&nbsp;<a name="anchor-image-wtip-min11952"/>
#### <a name="37-wrap-up-and-call-to-action-11743"></a>37. Conclusion et instructions, 1:17:43
[![Conclusion et instructions][image-wtip-min11952-wrap-up-call-action]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=4663)


&nbsp;<a name="anchor-image-wtip-min12042"/>
#### <a name="38-resources-for-more-information-12035"></a>38. Ressources pour plus d’informations, 1:20:35
[![Ressources pour plus d’informations][image-wtip-min12042-resources-more-info]](https://www.youtube.com/watch?v=jjNmcKBVjrc&t=4835)

- [Billet de blog, 22 mai 2017][resource-blog-saas-patterns-app-dev-sql-db-768h]

- *Conceptuelles :* [modèles de location de base de données SaaS multi-locataire][saas-concept-design-patterns-563e]

- *Didacticiels :* [l’application SaaS Wingtip Tickets][saas-how-welcome-wingtip-app-679t]

- Référentiels Github pour des variantes de l’application Wingtip Tickets SaaS :
    - [Réf Github pour : modèle d’application autonome][github-wingtip-standaloneapp].
    - [Réf Github pour : modèle de base de données par locataire][github-wingtip-dbpertenant].
    - [Réf Github pour : modèle de base de données multi-locataire][github-wingtip-multitenantdb].





## <a name="next-steps"></a>Étapes suivantes

- [Premier article du didacticiel][saas-how-welcome-wingtip-app-679t]




<!-- Image link reference IDs. -->

[image-wtip-min00003-brk3120-whole-welcome]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min00003-brk3120-welcome-myob-design-saas-app-sql-db.png "Diapositive d’accueil"

[image-wtip-min00311-session]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min00311-session-objectives-takeaway.png "Objectifs des sessions."

[image-wtip-min00417-agenda]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min00417-agenda-app-management-models-patterns.png "Agenda."

[image-wtip-min00505-web-app]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min00505-wingtip-saas-app-mt-web.png "Application Wingtip SaaS : application web multi-locataire"

[image-wtip-min00555-app-web-form]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min00555-app-form-contoso-concert-hall-night-opera.png "Formulaire web d’application en action"

[image-wtip-min00931-per-tenant-cost]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min00931-saas-data-management-concerns.png "Coût par locataire, mise à l’échelle, isolation, récupération"

[image-wtip-min01159-db-models-pros-cons]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min01159-db-models-multi-tenant-saas-apps.png "Modèles de bases de données pour multi-locataire : pour et contre"

[image-wtip-min01301-hybrid]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min01301-hybrib-model-blends-benefits-mt-st.png "Le modèle hybride mélange des avantages de MT/ST"

[image-wtip-min01644-st-vs-mt]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min01644-st-mt-pros-cons.png "Locataire unique contre multi-locataire : pour et contre"

[image-wtip-min01936-pools-cost]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min01936-pools-cost-effective-unpredictable-workloads.png "Les pools sont rentables pour des charges de travail non prévisibles"

[image-wtip-min02008-demo-st-hybrid]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min02008-demo-st-hybrid.png "Démonstration de ST/MT de base de données par locataire et hybrides"

[image-wtip-min02029-live-app-form-dojo]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min02029-app-form-dogwwod-dojo.png "Formulaire d’application en direct affichant Dojo"

[image-wtip-min02854-myob-no-dba]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min02854-myob-no-dba.png "MYOB et pas une DBA en vue"

[image-wtip-min02940-myob-elastic]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min02940-myob-elastic-pool-usage-example.png "Exemple d’utilisation de pool élastique MYOB"

[image-wtip-min03136-learning-isvs]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min03136-myob-isv-saas-patterns-design-scale.png "En savoir plus sur MYOB et autres ISV"

[image-wtip-min04315-patterns-compose]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min04315-patterns-compose-into-e2e-saas-scenario-st-mt.png "Modèles composés en scénarios SaaS E2E"

[image-wtip-min04733-canonical-hybrid]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min04733-canonical-hybrid-mt-saas-app.png "Application SaaS multi-locataire hybride Canonical"

[image-wtip-min04810-wingtip-saas-app]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min04810-saas-sample-app-descr-of-modules-links.png "Application exemple SaaS Wingtip"

[image-wtip-min04910-scenarios-tutorials]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min04910-scenarios-patterns-explored-tutorials.png "Scénarios et modèles explorés dans les didacticiels"

[image-wtip-min05018-demo-tutorials-github]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min05018-demo-saas-tutorials-github-repo.png "Démonstration de didacticiels et référentiel Github"

[image-wtip-min05038-github-wingtipsaas]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min05038-github-repo-wingtipsaas.png "Réf Github Microsoft/WingtipSaaS"

[image-wtip-min05620-exploring-patterns]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min05620-exploring-patterns-tutorials.png "Exploration des modèles"

[image-wtip-min05744-provisioning-tenants-onboarding-1]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min05744-provisioning-tenants-connecting-run-time-1.png "Approvisionnement de locataires et intégration"

[image-wtip-min05858-provisioning-tenants-app-connection-2]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min05858-provisioning-tenants-connecting-run-time-2.png "Approvisionnement de locataires et connexion d’application"

[image-wtip-min05943-demo-management-scripts-st]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min05943-demo-management-scripts-provisioning-st.png "Démonstration de scripts de gestion approvisionnant un locataire unique"

[image-wtip-min10002-powershell-provision-catalog]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min10002-powershell-code.png "PowerShell pour approvisionner et cataloguer"

[image-wtip-min10330-sql-select-tenantsextended]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min10330-ssms-tenantcatalog.png "T-SQL SELECT * FROM TenantsExtended"

[image-wtip-min10436-managing-unpredictable-workloads]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min10436-managing-unpredictable-tenant-workloads.png "Gestion des charges de travail de locataire imprévisibles"

[image-wtip-min10639-elastic-pool-monitoring]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min10639-elastic-pool-monitoring.png "Surveillance du pool élastique"

[image-wtip-min10942-load-generation]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min10942-schema-management-scale.png "Surveillance de la génération et des performances de charge"

[image-wtip-min11033-schema-management-scale]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min11033-schema-manage-1000s-dbs-one.png "Gestion des schémas à l’échelle"

[image-wtip-min11221-distributed-query]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min11221-distributed-query-all-tenants-asif-single-db.png "Requête distribuée dans des bases de données de locataire"

[image-wtip-min11232-demo-ticket-generation]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min11232-demo-ticket-generation-distributed-query.png "Démonstration de la génération de tickets"

[image-wtip-min11246-ssms-adhoc-analytics]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min11246-tsql-adhoc-analystics-db-elastic-query.png "Analyse ad hoc SSMS"

[image-wtip-min11632-extract-tenant-data-sql-dw]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min11632-extract-tenant-data-analytics-db-dw.png "Extraire les données de locataire dans DW SQL"

[image-wtip-min11648-graph-daily-sale-distribution]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min11648-graph-daily-sale-contoso-concert-hall.png "Graph de la distribution des ventes quotidiennes"

[image-wtip-min11952-wrap-up-call-action]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min11952-wrap-call-action-saasfeedback.png "Conclusion et instructions"

[image-wtip-min12042-resources-more-info]: media/saas-tenancy-video-index-wingtip-brk3120-20171011/wingtip-20171011-min12042-resources-blog-github-tutorials-get-started.png "Ressources pour plus d’informations"




<!-- Article link reference IDs. -->

[saas-concept-design-patterns-563e]: saas-tenancy-app-design-patterns.md

[saas-how-welcome-wingtip-app-679t]: saas-tenancy-welcome-wingtip-tickets-app.md


[video-on-youtube-com-478y]: https://www.youtube.com/watch?v=jjNmcKBVjrc&t=1

[video-on-channel9-479c]: https://channel9.msdn.com/Events/Ignite/Microsoft-Ignite-Orlando-2017/BRK3120


[resource-blog-saas-patterns-app-dev-sql-db-768h]: https://azure.microsoft.com/blog/saas-patterns-accelerate-saas-application-development-on-sql-database/


[github-wingtip-standaloneapp]: https://github.com/Microsoft/WingtipTicketsSaaS-StandaloneApp/

[github-wingtip-dbpertenant]: https://github.com/Microsoft/WingtipTicketsSaaS-DbPerTenant/

[github-wingtip-multitenantdb]: https://github.com/Microsoft/WingtipTicketsSaaS-MultiTenantDB/

