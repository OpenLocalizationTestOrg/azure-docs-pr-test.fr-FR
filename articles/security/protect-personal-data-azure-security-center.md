---
title: "les données personnelles aaaProtect avec Azure Security Center | Documents Microsoft"
description: "protéger les données personnelles à l’aide d’Azure Security Center"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>Protéger les données personnelles contre les violations et attaques : Azure Security Center

Cet article vous aidera à comprendre comment toouse Azure Security Center tooprotect les données personnelles d’atteinte et les attaques.

## <a name="scenario"></a>Scénario 

Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée et mer Baltique, ainsi que hello britanniques. toohelp à cet égard, elle a acquis plusieurs lignes croisière plus petits dans Italie, Allemagne, Danemark et hello Royaume-Uni.

la société de Hello utilise des données d’entreprise de Microsoft Azure toostore dans le cloud de hello. Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit. Des informations de ressources humaines sont également inclues comme :

- Adresses
- Numéros de téléphone
- Numéros d’identification fiscale
- Informations médicales

ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité. Réseau de hello accès employés de l’entreprise à partir de sites distants et les agents de voyage société hello situés dans Bonjour tout le monde ont accès aux ressources de l’entreprise toosome.
Données personnelles parcourent le réseau de hello entre ces bureaux et le centre de données Microsoft hello.

## <a name="problem-statement"></a>Définition du problème

Hello société est préoccupée menace hello d’attaques sur leurs ressources Azure. Ils veulent exposition tooprevent de personnes de toounauthorized données personnelles des employés et clients. Ils veulent quant à la fois prévention et correction/réponse, mais aussi un moyen efficace toomonitor hello en continu la sécurité de leurs ressources de cloud.
Elle nécessite une solide ligne de défense contre les attaques complexes et organisées d’aujourd’hui.

## <a name="company-goal"></a>Objectif de l’entreprise

Un des objectifs de l’entreprise hello est confidentialité de hello tooensure des employés et les clients des données personnelles à protéger contre les menaces. Un des objectifs est toorespond immédiatement toosigns de violation toomitigate hello impact. Il nécessite un moyen tooassess hello l’état actuel de la sécurité, identifier les configurations vulnérables et les corriger.

## <a name="solutions"></a>Solutions

Microsoft Azure Security Center (ASC) fournit une solution de surveillance de sécurité et de gestion de stratégie intégrée. Il offre des fonctionnalités de prévention, de détection et de réponse aux menaces efficaces et faciles à utiliser.

### <a name="prevention"></a>Prévention

ASC vous aide à empêcher les violations vous tooset des stratégies de sécurité, fournir un accès juste-à-temps et mettre en œuvre des recommandations de sécurité.

Une stratégie de sécurité définit ensemble hello de contrôles recommandé pour les ressources hello spécifié abonnement. Juste-à-temps accès peut être utilisé toolock vers le bas le trafic entrant tooyour les machines virtuelles Azure, ce qui réduit les risques tooattacks. Recommandations de sécurité sont créées par ASC après l’analyse d’état de la sécurité de vos ressources Azure hello.

#### <a name="how-do-i-set-security-policies-in-asc"></a>Comment définir des stratégies de sécurité dans ASC ?

Vous pouvez configurer des stratégies de sécurité pour chaque abonnement. toomodify une stratégie de sécurité, vous devez être propriétaire ou contributeur de cet abonnement. Bonjour portail Azure, procédez comme hello suivant :

1. Sélectionnez **stratégie** dans le tableau de bord hello ASC.

2. Sélectionnez l’abonnement hello sur lequel vous souhaitez que la stratégie de hello de tooenable.

3. Choisissez **stratégie de prévention de** stratégies tooconfigure par abonnement. **Collecter des données à partir d’ordinateurs virtuels** doit être défini trop**sur.**

4. Bonjour **stratégie de prévention de** options, sélectionnez **sur** tooenable les recommandations de sécurité hello qui sont pertinentes pour l’abonnement de hello.

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

Pour plus d’instructions et une explication de chacune des recommandations pour la stratégie hello qui peuvent être activées, consultez [définir des stratégies de sécurité dans le centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>Comment configurer l’accès juste-à-temps (JIT) ?

Lorsque le JIT est activé, le centre de sécurité bloque le trafic entrant tooyour machines virtuelles Azure en créant une règle de groupe de sécurité réseau. Vous sélectionnez les ports hello sur hello VM toowhich le trafic entrant sera verrouillé. toouse JIT accéder, hello suivant :

1. Sélectionnez hello **juste dans la vignette de temps machine virtuelle accès** sur le panneau ASC hello.

2. Sélectionnez hello **recommandé** onglet.

3. Sous **machines virtuelles**, sélectionnez les machines virtuelles de hello que vous souhaitez tooenable. Cela permet de placer un ordinateur virtuel de tooa suivant coche. 
4. Sélectionnez **Activer JIT** sur les machines virtuelles.
5. Sélectionnez **Enregistrer**.

Ensuite, vous pouvez voir des ports par défaut hello ASC recommandées doivent être activés pour JIT. Vous pouvez également ajouter et configurer un nouveau port sur lequel vous souhaitez hello tooenable juste-à-solution de temps. Hello **juste à l’accès des ordinateurs virtuels de temps** vignette Bonjour centre de sécurité affiche nombre hello d’ordinateurs virtuels configurés pour l’accès JIT. Il montre également le nombre hello approuvées de demandes d’accès effectuées Bonjour la semaine dernière.

![](media/protect-personal-data-azure-security-center/jit-vm.png)

Pour obtenir des instructions sur la façon de toodo, et des informations supplémentaires sur juste dans access de temps, consultez [gérer l’accès d’ordinateur virtuel à l’aide de juste-à-temps.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>Comment implémenter les recommandations de sécurité ASC ?

Lorsqu’il identifie des failles de sécurité potentielles, il crée des recommandations. recommandations de Hello vous guident tout au long des processus de hello de configuration de contrôles de hello si nécessaire. 
1. Sélectionnez hello **recommandations** vignette sur le tableau de bord hello ASC.

2. Afficher les recommandations de hello, qui sont affichées sous forme de tableau, où chaque ligne représente une recommandation.

3. recommandations de toofilter, sélectionnez **filtre** et sélectionnez valeurs hello gravité et son état toosee vous le souhaitez.

4. toodismiss une recommandation qui n’est pas applicable, vous pouvez cliquez droit et sélectionnez **faire disparaître.**

5. Évaluez les recommandations à appliquer en premier.

6. Appliquer les recommandations de hello dans l’ordre de priorité.

Pour obtenir la liste des recommandations possibles et des procédures détaillées sur la façon de tooapply chaque, consultez [gestion des recommandations de sécurité dans le centre de sécurité Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>Détection et réponse

Détection et réponse allient ensemble, comme vous le voulez toorespond aussi rapidement que possible après qu’une menace est détectée.
Détection des menaces ASC fonctionne en collectant automatiquement des informations de sécurité à partir de vos ressources Azure, hello réseau et les solutions de partenaire connecté. ASC peut donc rapidement mettre à jour ses algorithmes de détection, puisque les pirates sont à l’origine d’attaques innovantes de plus en plus sophistiquées. Pour plus d’informations sur le fonctionnement de la détection des menaces par ASC, consultez [Fonctionnalités de détection d’Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>Comment gérer et répondre toosecurity alertes ?

Une liste des alertes de sécurité hiérarchisée est indiquée dans le centre de sécurité, ainsi que de hello informations dont vous avez besoin tooquickly examiner le problème de hello. Centre de sécurité inclut également des recommandations sur la manière tooremediate une attaque. toomanage votre sécurité des alertes, faire hello suivant :

1. Sélectionnez hello **alertes de sécurité** vignette dans le tableau de bord hello ASC. Celle-ci permet d’afficher les détails de chaque alerte.

2. alertes toofilter en fonction de date, d’état et de gravité, sélectionnez **filtre** , puis sélectionnez les valeurs hello toosee.

3. toorespond tooan alerte, sélectionnez-la et passez en revue les informations de hello, puis sélectionnez hello ressource qui a été attaqué.

4. Bonjour **Description** champ, vous verrez plus d’informations, y compris la résolution recommandée.

![](media/protect-personal-data-azure-security-center/security-alerts.png)

Pour des instructions sur les alertes toosecurity ne répond plus détaillées, consultez [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

Pour obtenir de l’aide de l’examen des alertes de sécurité, société de hello peut intégrer les alertes ASC sa propre solution SIEM, à l’aide de [Azure journal intégration](https://aka.ms/AzLog).

#### <a name="how-do-i-manage-security-incidents"></a>Comment gérer les incidents de sécurité ?

Dans ASC, un incident de sécurité est un regroupement de toutes les alertes d’une ressource correspondant à des modèles de chaîne de destruction. Un Incident indiquent liste hello d’alertes associées, ce qui permet de vous tooobtain plus d’informations sur chaque occurrence. Incidents apparaissent dans hello vignette alertes de sécurité et de panneau.

tooreview et la gestion des incidents de sécurité, hello suivant :

1. Sélectionnez hello **alertes de sécurité** vignette. Si un incident de sécurité est détecté, elle s’affiche sous le graphique d’alertes de sécurité de hello. Son icône diffère de celles des autres alertes.

2. Sélectionnez toosee d’incident hello plus de détails sur cet incident de sécurité. Des détails supplémentaires comprennent sa description complète, sa gravité, son état actuel, hello attaqué ressource, les étapes de conversion hello pour les incidents hello et hello alertes qui ont été inclus dans cet incident.

Vous pouvez filtrer toosee **uniquement les incidents**, **alertes uniquement**, ou **les deux**.

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>Comment accéder à hello Threat Intelligence rapport ?

ASC analyse les informations contre les menaces de tooidentify plusieurs sources. les équipes de réponse aux incidents tooassist examiner et corriger les menaces, centre de sécurité inclut un rapport de menace qui contient des informations sur les menaces hello qui a été détectée.

Azure Security Center propose trois types de rapports sur les menaces, qui peuvent varier en fonction de l’attaque.
rapports Hello disponibles sont :

- Rapport sur le groupe d’activités : fournit des informations détaillées sur les attaquants, leurs objectifs et leurs tactiques.

- Rapport sur la campagne : se concentre sur les détails des campagnes d’attaque spécifiques.

- Rapport de synthèse de menace : couvre tous les éléments dans les rapports de deux précédente hello.

Ce type d’information est très utile au cours du processus de réponse aux incidents hello, s’il existe une source de hello toounderstand enquête en cours d’attaque de hello, hello la personne malveillante, et des motivations le toomitigate toodo ce problème passer.

1. tooaccess hello sur les menaces de rapports, hello suivant :

2. Sélectionnez hello **alertes de sécurité** vignette sur le tableau de bord hello ASC.

3. Sélectionnez alerte de sécurité hello pour lequel vous souhaitez tooobtain plus d’informations.

4. Bonjour **rapports** , cliquez sur hello lien toohello threat intelligence du rapport.

5. Fichier PDF hello, que vous pouvez télécharger s’ouvre.

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

Pour plus d’informations sur hello rapport ASC menace, consultez [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>Évaluation

toohelp avec des tests, l’évaluation et d’évaluation de vos défenses, ASC fournit pour l’évaluation des vulnérabilités intégré avec Qualys agents du cloud, dans le cadre de son composant de recommandations de machine virtuelle.

agent de Qualys Hello signale une vulnérabilité données toohello Qualys plateforme de gestion, qui envoie ensuite la vulnérabilité et l’intégrité de l’analyse des données de sauvegarde tooASC. Hello tooadd recommandation une solution d’évaluation de la vulnérabilité est affichée dans hello **recommandations** panneau dans le tableau de bord hello ASC.

Une fois la solution d’évaluation des risques de vulnérabilité hello est installée sur la cible de hello machine virtuelle, les analyses de centre de sécurité hello toodetect de machine virtuelle et identifient les vulnérabilités des applications et système. A détecté les problèmes sont affichent sous hello **recommandations de Machines virtuelles** option.

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>Comment mettre en œuvre une solution d’évaluation des vulnérabilités ? 

Si une machine virtuelle n’a pas déjà une solution d’évaluation des vulnérabilités intégrée déployée, Security Center recommande d’en installer une.

1. De hello ASC tableau de bord sur hello **recommandations** panneau, sélectionnez **ajouter une solution d’évaluation de la vulnérabilité.**

2. Sélectionnez les machines virtuelles de hello où vous souhaitez la solution d’évaluation des risques de vulnérabilité tooinstall hello.

3. Cliquez sur **Installer sur [nombre] machines virtuelles.**

4. Sélectionnez une solution partenaire Bonjour Azure Marketplace ou sous **utiliser une solution existante,** sélectionnez **Qualys.**

5. Vous pouvez activer hello automatiquement mise à jour ou désactiver les paramètres de hello **Solutions de partenaire** panneau.

Pour plus d’informations sur la façon de tooimplement une solution d’évaluation de la vulnérabilité, consultez [évaluation des vulnérabilités dans le centre de sécurité Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>Étapes suivantes

- [Guide de démarrage rapide d’Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [Introduction tooAzure centre de sécurité](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [Intégration des alertes Azure Security Center aux journaux Azure](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [Renforcer Azure Security Center avec l’évaluation des vulnérabilités intégrée](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
