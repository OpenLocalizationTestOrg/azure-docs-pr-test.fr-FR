---
title: "aaaAdd un pare-feu d’applications web dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandations du centre de sécurité Azure ** ajouter une application de web pare-feu ** et ** finaliser la protection d’application **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Ajouter un pare-feu d'applications web dans le Centre de sécurité Azure
Centre de sécurité Azure peut recommander que vous ajoutez un pare-feu d’applications web (WAF) à partir d’un toosecure de partenaire Microsoft vos applications web. Ce document présente un exemple de procédure tooapply cette recommandation.

Une recommandation WAF est indiquée pour n’importe quelle IP publique (adresse IP de niveau d’instance ou adresse IP à équilibrage de charge) ayant un groupe de sécurité réseau associé avec des ports web entrants ouverts (80, 443).

Centre de sécurité vous recommande de que configurer un toohelp WAF vous défendre contre des attaques ciblant vos applications web sur des ordinateurs virtuels et sur l’environnement App Service. Un environnement App Service (ASE) est une option de plan de service [Premium](https://azure.microsoft.com/pricing/details/app-service/) d'Azure App Service qui fournit un environnement totalement isolé et dédié pour l'exécution sécurisée de vos applications Azure App Service. toolearn en savoir plus sur ASE, consultez hello [Documentation d’environnement App Service](../app-service/app-service-app-service-environments-readme.md).

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Ce document n'est pas un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **sécuriser l’application web à l’aide de pare-feu d’applications web**.
   ![Sécuriser l’application web][1]
2. Bonjour **sécuriser vos applications web à l’aide de pare-feu d’applications web** panneau, sélectionnez une application web. Hello **ajouter un pare-feu d’applications Web** panneau s’ouvre.
   ![Add a web application firewall][2]
3. Vous pouvez choisir toouse un pare-feu d’applications web existante si elle est disponible, ou vous pouvez créer un nouveau. Dans cet exemple, il n'existe aucun pare-feu WAF existant, et nous allons donc en créer un.
4. toocreate un WAF, sélectionnez une solution à partir de la liste hello de partenaires intégrés. Dans cet exemple, nous sélectionnons **Pare-feu d’applications web Barracuda**.
5. Hello **pare-feu d’applications Web Barracuda** panneau s’ouvre vous fournissant des informations sur les solutions de partenaire hello. Sélectionnez **créer** dans le panneau d’informations hello.

   ![Panneau d’informations du pare-feu][3]

6. Hello **nouveau pare-feu d’applications Web** panneau s’ouvre, où vous pouvez effectuer **Configuration de machine virtuelle** les étapes et fournir **WAF informations**. Sélectionnez **Configuration de machine virtuelle**.
7. Bonjour **Configuration d’ordinateur virtuel** panneau, que vous entrez les informations requise toospin hello virtual machine qui exécute hello WAF.
   ![VM configuration][4]
8. Retourner toohello **nouveau pare-feu d’applications Web** panneau et sélectionnez **WAF informations**. Bonjour **WAF informations** panneau, vous configurez WAF hello lui-même. Étape 7 vous permet de machine virtuelle de tooconfigure hello sur quel hello WAF s’exécute et l’étape 8 vous permet de tooprovision hello WAF lui-même.

## <a name="finalize-application-protection"></a>Finaliser la protection des applications
1. Retourner toohello **recommandations** panneau. Une nouvelle entrée a été générée après créé WAF hello, appelé **finaliser la protection de l’application**. Cette entrée permet de savoir que vous devez toocomplete hello consistant en réalité raccordant hello WAF dans hello réseau virtuel Azure afin qu’elle peut protéger l’application hello.

   ![Finaliser la protection des applications][5]

2. Sélectionnez **Finaliser la protection des applications**. Un nouveau panneau s'ouvre. Vous pouvez voir qu’il existe une application web qui doit toohave son trafic redirigé.
3. Sélectionnez l’application web de hello. Un panneau s’ouvre, fournit les étapes pour la finalisation de l’installation de pare-feu hello web application. Effectuez les étapes de hello, puis sélectionnez **restreindre le trafic**. Centre de sécurité ensuite hello de connexion à distance pour vous.

   ![Restreindre le trafic][6]

> [!NOTE]
> Vous pouvez protéger plusieurs applications web dans le centre de sécurité en ajoutant ces applications tooyour WAF les déploiements existants.
>
>

les journaux à partir de ce WAF Hello sont maintenant entièrement intégrés. Centre de sécurité peut démarrer automatiquement collecte et l’analyse des journaux de hello afin qu’il peut faire surface tooyou d’alertes de sécurité importantes.

## <a name="next-steps"></a>Étapes suivantes
Ce document vous a montré comment tooimplement hello recommandation du centre de sécurité « Ajouter une application web ». toolearn savoir plus sur la configuration d’un pare-feu d’applications web, voir hello :

* [Configuration d'un pare-feu d'applications Web (WAF) pour un environnement App Service](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
