---
title: incidents de toosecurity aaaRespond avec Azure Security Center | Documents Microsoft
description: "Ce document explique comment toouse Azure Security Center pour un scénario de réponse aux incidents."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>Utilisation d’Azure Security Center pour la réponse aux incidents
De nombreuses organisations apprendre comment incidents de toosecurity toorespond qu’après avoir subi une attaque. tooreduce coûts et dommages, il est important toohave une réponse aux incidents en place le plan avant une attaque a lieu. Vous pouvez utiliser Azure Security Center à différentes étapes de la réponse à un incident.

## <a name="incident-response-planning"></a>Planification de la réponse aux incidents
Un plan efficace dépend de trois fonctionnalités principales : qui est en mesure de tooprotect, détecter et répondre toothreats. Protection sur la prévention des incidents, la détection est sur l’identification des menaces au début, et réponse sur retirer les intrus hello et la restauration des impacts de hello toomitigate systèmes de violation.

Cet article utilise les étapes de réponse aux incidents de sécurité hello de hello [réponse de sécurité Microsoft Azure Bonjour Cloud](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) article, comme indiqué dans hello suivant schéma :

![Cycle de vie de la réponse aux incidents](./media/security-center-incident-response/security-center-incident-response-fig1.png)

Vous pouvez utiliser le centre de sécurité au cours des phases de détecter, évaluer et diagnostiquer hello. Voici les exemples de la façon dont le centre de sécurité peut être utile au cours des phases de réponse aux incidents initiale trois hello :

* **Détecter**: passez en revue la première indication de hello d’une analyse de l’événement.
  * Exemple : révision hello vérification primitive qu’une alerte de sécurité de haute priorité a été déclenchée dans le tableau de bord de centre de sécurité hello.
* **Évaluer**: effectuer hello évaluation initiale tooobtain plus d’informations sur les activités suspectes hello.
  * Exemple : obtenir plus d’informations sur l’alerte de sécurité hello.
* **Diagnostiquer** : mener une investigation technique et identifier les stratégies de confinement, d’atténuation des risques et de contournement.
  * Exemple : suivez les étapes de mise à jour de hello décrites par le centre de sécurité dans cette alerte de sécurité particulière.

scénario Hello qui suit montre comment le centre de sécurité tooleverage pendant hello détecter, évaluer et diagnostiquer/réponse, les étapes d’un incident de sécurité. Dans Azure Security Center, un [incident de sécurité](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) est un regroupement de toutes les alertes d’une ressource correspondant à des modèles de [chaîne de destruction](security-center-incident.md). Incidents apparaissent dans hello [alertes de sécurité](security-center-managing-and-responding-alerts.md) vignette et lame. Un incident, vous affichez hello liste d’alertes associées, ce qui permet de vous tooobtain plus d’informations sur chaque occurrence. Centre de sécurité présente également les alertes de sécurité peuvent également être utilisé tootrack vers le bas d’une activité suspecte autonome.

## <a name="scenario"></a>Scénario
Contoso migrée récemment certaines de leur tooAzure de ressources locales, y compris certains basée sur l’ordinateur virtuel les charges de travail line-of-business et les bases de données SQL. L’équipe principale de réponse aux incidents de sécurité informatique (CSIRT) de Contoso rencontre aujourd’hui des difficultés pour étudier les problèmes de sécurité car les renseignements sur la sécurité ne sont pas intégrés à leurs outils actuels de réponse aux incidents. Ce manque d’intégration présente un problème au cours de hello détecter étape (trop de faux positifs), ainsi qu’au cours de hello évaluation et les étapes de diagnostiquer. Dans le cadre de cette migration, ils ont choisi tooopt dans pour le centre de sécurité toohelp les résolvent ce problème.

Hello la première phase de migration terminée après leur embarquées toutes les ressources et le problème traité toutes les recommandations de sécurité hello du centre de sécurité. Contoso CSIRT est le point focal de hello pour le traitement des incidents de sécurité informatique. équipe de Hello se compose d’un groupe de personnes chargé du traitement des incidents de sécurité. membres de l’équipe Hello ont eux-mêmes clairement défini tooensure droits aucune zone de réponse n’est laissée non traité.

Pour les besoins de hello de ce scénario, nous allons toofocus sur des rôles hello Hello suivant personnages qui font partie de Contoso CSIRT :

![Cycle de vie de la réponse aux incidents](./media/security-center-incident-response/security-center-incident-response-fig2.png)

Judy travaille aux opérations de sécurité. Ses responsabilités incluent :

* Surveiller et réagir de menaces toosecurity autour de l’horloge hello.
* Escalade de propriétaire de la charge de travail toohello cloud ou un analyste de sécurité en fonction des besoins.

Sam est analyste de la sécurité et ses responsabilités incluent :

* L’examen des attaques.
* La correction des alertes.
* Utilisation des toodetermine propriétaires de charges de travail et appliquez les solutions d’atténuation.

Comme vous pouvez le voir, Laura et Sam disposent de responsabilités différentes, et ils doivent travailler ensemble d’informations tooshare centre de sécurité.

## <a name="recommended-solution"></a>Solution recommandée
Laura et Sam ayant des rôles différents, ils utiliserez différentes zones des informations pertinentes tooobtain de centre de sécurité pour leurs activités quotidiennes. Judy utilise les **alertes de sécurité** dans le cadre de sa surveillance quotidienne.

![Alertes de sécurité](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Laura utilise des alertes de sécurité pendant la hello détecter et les étapes de l’évaluation. Laura après l’évaluation initiale de hello, elle peut réaffecter hello problème tooSam si un examen complémentaire est requis. À ce stade, Sam utilise les informations de hello qui a été fournies par le centre de sécurité, parfois en association avec d’autres sources de données, toomove toohello diagnostiquer étape.

## <a name="how-tooimplement-this-solution"></a>Comment tooimplement cette solution
toosee comment vous utilisez Azure Security Center dans un scénario de réponse aux incidents, nous allons comme suit de Laura dans les étapes de détecter et d’évaluation hello et ensuite voir ce que fait Sam problème de hello toodiagnose.

### <a name="detect-and-assess-incident-response-stages"></a>Étapes de détection et d’évaluation de la réponse aux incidents
Laura connecté toohello portail Azure et qu’il fonctionne dans la console hello centre de sécurité. Dans le cadre de son quotidienne suivi des activités, elle a démarré de révision de sécurité haute priorité hello d’alertes en procédant comme suit :

1. Cliquez sur hello **alertes de sécurité** hello vignette et accès **alertes de sécurité** panneau.
    ![Panneau Alertes de sécurité](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > Pour les besoins de hello de ce scénario, Laura est continu tooperform une évaluation de l’alerte d’activité hello SQL malveillant, Bonjour précédant figure.
   >
   >
2. Cliquez sur hello **activité SQL malveillant** d’alerte et examinez les ressources hello attaqué Bonjour **activité SQL malveillant** panneau : ![détails de l’Incident](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    Dans ce panneau, Laura peut prendre des notes relatives aux ressources de hello attaqué, comment plusieurs fois cette attaque s’est produite, et quand il a été détecté.
3. Cliquez sur hello **attaqué ressource** tooobtain plus d’informations sur ce type d’attaque.

Après avoir lu la description de hello, Laura est convaincue qu’il ne s’agit pas d’un faux positif et qu’elle doit escalader ce cas tooSam.

### <a name="diagnose-incident-response-stage"></a>Étape de diagnostic de la réponse aux incidents
SAM Laura reçoit les cas hello et démarre l’examen des étapes correctives hello suggéré du centre de sécurité.

![Cycle de vie de la réponse aux incidents](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>Ressources supplémentaires
équipe de réponse aux incidents Hello peut également bénéficier de hello [Security Center Power BI](security-center-powerbi.md) fonctionnalité toosee différents types de rapports. Ces rapports peuvent faciliter pendant plu toovisualize d’enquête, analyser et filtrer les recommandations et les alertes de sécurité. Pour les entreprises qui utilisent leurs informations de sécurité et de la solution de gestion (SIEM) des événements pendant le processus d’investigation hello, ils peuvent également [intégrer le centre de sécurité et leur solution](security-center-integrating-alerts-with-log-integration.md). Vous pouvez également intégrer des journaux d’audit Azure et les événements de sécurité de l’ordinateur virtuel (VM) à l’aide de hello [outil d’intégration Azure log](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/). tooinvestigate une attaque, vous pouvez utiliser ces informations conjointement avec les informations de hello offre du centre de sécurité.

## <a name="conclusion"></a>Conclusion
Constituer une équipe avant un incident se produit est très important tooyour organisation et positivement sur la gestion des incidents. Hello outils toomonitor ressources peut aider à cette tooremediate d’étapes précises équipe tootake un incident de sécurité. Centre de sécurité [des fonctionnalités de détection](security-center-detection-capabilities.md) peut aider les incidents de toosecurity informatique tooquickly répondre et corriger les problèmes de sécurité.
