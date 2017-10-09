---
title: "Centre d’aaaSecurity Guide de planification et opérations | Documents Microsoft"
description: "Ce document vous aide à tooplan avant d’arrêter le centre de sécurité Azure et les considérations concernant les opérations quotidiennes."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Guide des opérations et de planification du Centre de sécurité Azure
Ce guide est pour les professionnels de l’informatique, architectes informatique, aux analystes en sécurité des informations et les administrateurs de cloud dont l’organisation prévoit toouse Azure Security Center.

>[!NOTE] 
>À compter de début juin 2017, centre de sécurité utiliser hello Microsoft Monitoring Agent toocollect et stocker des données. Consultez [Migration de plateforme Azure Security Center](security-center-platform-migration.md) toolearn plus. informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>

## <a name="planning-guide"></a>Guide de planification
Ce guide couvre un ensemble d’étapes et de tâches que vous pouvez suivre toooptimize que votre utilisation du centre de sécurité basée sur les exigences de sécurité de votre organisation et le modèle de gestion de cloud. tootake pleinement parti du centre de sécurité, il est important toounderstand comment différentes personnes ou équipes de votre organisation utiliser développement sécurisé de hello service toomeet, surveillance, gouvernance, et a besoin de réponse aux incidents. Hello domaines clés tooconsider lors de la planification du centre de sécurité toouse sont les suivantes :

* Rôles de sécurité et contrôles d’accès
* Stratégies et recommandations de sécurité
* Collecte et stockage des données
* Surveillance continue de la sécurité
* Réponse aux incidents

Dans la section suivante de hello, vous allez apprendre comment tooplan pour chacune de ces zones et d’appliquer ces recommandations en fonction de vos besoins.

> [!NOTE]
> Lecture [Azure Security Center Forum aux questions (FAQ)](security-center-faq.md) pour obtenir la liste des questions courantes qui peuvent également être utiles pendant hello conception et la phase de planification.
> 

## <a name="security-roles-and-access-controls"></a>Rôles de sécurité et contrôles d’accès
Selon la taille de hello et la structure de votre organisation, plusieurs personnes et les équipes peuvent utiliser des tâches de relatives à la sécurité autres centre de sécurité tooperform. Hello suivant schéma vous offre un exemple fictifs personnages leurs rôles respectifs et les responsabilités de sécurité :

![contrôleur](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Centre de sécurité permet à ces personnes toomeet ces responsabilités différentes. Par exemple :

**Jeff (propriétaire de la charge de travail cloud)**

* Gérer une charge de travail de cloud et ses ressources connexes
* Chargé de l’implémentation et de la maintenance des protections conformément à la stratégie de sécurité de l’entreprise

**Ellen (directrice informatique/responsable de la sécurité des systèmes d’information)**

* Responsable de tous les aspects de sécurité pour l’entreprise de hello
* Veut posture de sécurité de la société toounderstand hello dans les charges de travail cloud
* Toobe besoins informé des risques et des attaques principales

**David (sécurité informatique)**

* Jeux de protections de tooensure hello appropriés soient en place des stratégies de sécurité de l’entreprise
* Surveille la conformité aux stratégies
* Génère les rapports pour la direction ou les auditeurs

**Judy (opérations de sécurité)**

* Surveille et répond toosecurity alertes 24/7
* Remonter tooCloud propriétaire de la charge de travail ou un analyste de sécurité informatique

**Sam (analyste de sécurité)**

* Analyse les attaques
* Travailler avec la mise à jour tooapply de propriétaire de la charge de travail de Cloud 

Centre de sécurité utilise [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md), qui fournit des [rôles intégrés](../active-directory/role-based-access-built-in-roles.md) qui peuvent être attribuées toousers, des groupes et des services dans Azure. Lorsqu’un utilisateur ouvre le centre de sécurité, ils voient uniquement les informations liées tooresources ils ont accès. Ce qui signifie que les utilisateurs hello rôle hello du propriétaire, collaborateur ou lecteur toohello abonnement ou une ressource groupe appartenant à une ressource. Dans les rôles toothese addition, il existe deux rôles de centre de sécurité spécifiques :

- **Lecteur de sécurité**: utilisateur qui appartient toothis rôle est en mesure de tooview droits tooSecurity Center, qui inclut des recommandations, alertes, la stratégie et contrôle d’intégrité, mais il ne toomake en mesure de modifications.
- **Administrateur de la sécurité**: même comme lecteur de sécurité, mais il peut également mettre à jour stratégie de sécurité hello, ignorez les alertes et les recommandations.

rôles du centre de sécurité Hello décrites ci-dessus n’ont pas d’accéder aux zones de service tooother Azure telles que le stockage, Web et mobiles ou Internet des objets.  

> [!NOTE]
> Un utilisateur doit toobe au moins un abonnement, le propriétaire du groupe de ressources ou le collaborateur toobe toosee en mesure de centre de sécurité dans Azure. 
> 
> 

À l’aide de personnages de hello expliquées dans le diagramme précédent hello, hello RBAC suivante sont nécessaires :

**Jeff (propriétaire de la charge de travail cloud)**

* Propriétaire/collaborateur du groupe de ressources

**David (sécurité informatique)**

* Propriétaire/collaborateur de l’abonnement ou Administrateur de la sécurité

**Judy (opérations de sécurité)**

* Lecteur de l’abonnement ou de sécurité Reader tooview alertes
* Abonnement propriétaire/collaborateur ou administrateur de la sécurité requise toodismiss alertes

**Sam (analyste de sécurité)**

* Alertes liées aux abonnements lecteur tooview
* Abonnement propriétaire/collaborateur requis toodismiss alertes
* Espace de travail Access toohello peut être nécessaire

Certains autres tooconsider des informations importantes :

* Seuls les collaborateurs/propriétaires d’abonnement et les administrateurs de sécurité peuvent modifier une stratégie de sécurité
* Seuls les propriétaires et collaborateurs d’abonnement et de groupe de ressources peuvent appliquer les recommandations de sécurité pour une ressource

Lorsque vous planifiez le contrôle d’accès à l’aide de RBAC pour le centre de sécurité, être toounderstand que personne utilisant le centre de sécurité de votre organisation. ainsi que les types de tâches qu’ils effectueront, puis configurez RBAC en conséquence.

> [!NOTE]
> Nous recommandons d’attribuer hello rôle le moins permissif nécessaire pour les utilisateurs toocomplete leurs tâches. Par exemple, les utilisateurs qui suffit tooview plus d’informations sur l’état de sécurité hello de ressources, mais pas effectuer une action, telles que l’application des recommandations ou de la modification des stratégies, doivent être rôle hello du lecteur.
> 
> 

## <a name="security-policies-and-recommendations"></a>Stratégies et recommandations de sécurité
Une stratégie de sécurité définit l’ensemble de hello de contrôles, qui sont recommandés pour les ressources hello spécifié abonnement. Dans le centre de sécurité, vous définissez des stratégies en fonction de la société tooyour exigences de sécurité et de type hello d’applications ou de la sensibilité des données de salutation.

Les stratégies sont activées dans le niveau d’abonnement hello automatiquement propager tooall des groupes de ressources au sein de l’abonnement de hello comme indiqué dans hello suivant schéma :

![Stratégies de sécurité](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Si vous avez besoin de tooreview les stratégies qui ont été modifiés, vous pouvez utiliser [les journaux d’Audit Azure](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). Les modifications de stratégie y sont toujours enregistrées.
> 
> 

### <a name="security-recommendations"></a>Recommandations de sécurité
Avant de configurer des stratégies de sécurité, passez en revue chacune de hello [recommandations de sécurité](security-center-recommendations.md)et déterminer si ces stratégies sont appropriés pour vos abonnements et les groupes de ressources différents. Il est également important toounderstand action que doit entreprendre tooaddress [recommandations de sécurité](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) et la personne de votre organisation responsable de l’analyse des nouvelles recommandations et prise de hello nécessaires comme suit.

Le Centre de sécurité vous recommande de fournir les détails du contact de sécurité pour votre abonnement Azure. Ces informations seront être utilisées par Microsoft toocontact si hello MSRC Microsoft Security Response Center () détecte que votre client a accédé aux données par un tiers illégal ou non autorisé. Lecture [fournissent des détails de contact de sécurité dans le centre de sécurité Azure](security-center-provide-security-contact-details.md) pour plus d’informations sur la façon de tooenable cette recommandation.

## <a name="data-collection-and-storage"></a>Collecte et stockage des données
Centre de sécurité Azure utilise hello Microsoft Monitoring Agent – il s’agit d’hello même agent utilisé par hello Operations Management Suite et service Analytique de journal – toocollect les données de sécurité à vos machines virtuelles. Les données collectées à partir de cet agent seront stockées dans vos espaces de travail Log Analytics.

### <a name="agent"></a>Agent

Une fois la collecte de données est activée dans la stratégie de sécurité hello, hello Microsoft Monitoring Agent (pour [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) ou [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) est installé sur tous les ordinateurs virtuels de Azure et de nouveaux qui sont créés.  Si hello que déjà est hello Microsoft Monitoring Agent est installé, l’ordinateur virtuel Azure Security Center reposera hello actuel installé l’agent. processus de l’agent Hello est conçue toobe non invasif et ont un impact minimal sur les performances de la machine virtuelle.

Hello Microsoft Monitoring Agent pour Windows requiert utilisent le port TCP 443. Consultez hello [l’article de résolution des problèmes](security-center-troubleshooting-guide.md) pour plus d’informations.

Si à un moment donné vous souhaitez toodisable la collecte de données, vous pouvez la désactiver dans la stratégie de sécurité hello. Toutefois, étant donné que hello Microsoft Monitoring Agent peut être utilisé par les autres tâches de gestion Azure et de surveillance des services, l’agent de hello ne sera pas désinstallé automatiquement lorsque vous désactivez collecte de données dans le centre de sécurité. Vous pouvez la désinstaller manuellement l’agent de hello si nécessaire.

> [!NOTE]
> toofind une liste d’ordinateurs virtuels pris en charge, lire hello [Azure Security Center Forum aux questions (FAQ)](security-center-faq.md).
> 

### <a name="workspace"></a>Espace de travail

Données collectées à partir de hello que Microsoft Monitoring Agent (pour le compte Azure Security Center) sera stocké dans soit un espace journal Analytique existant associé à votre abonnement Azure ou d’un nouvel espace, tenant hello de compte géo-réplication Hello machine virtuelle. 

Bonjour portail Azure, vous pouvez parcourir toosee une liste de vos espaces de travail Analytique des journaux, y compris ceux créés par Azure Security Center. Un groupe de ressources associées sera créé pour les nouveaux espaces de travail. Les deux respecteront la convention d’affectation de noms suivante : 

* Espace de travail : *DefaultWorkspace-[ID d’abonnement]-[zone géographique]*
* Groupe de ressources : *DefaultResouceGroup-[zone géographique]*

Pour les espaces de travail créés par Azure Security Center, les données sont conservées pendant 30 jours. Pour quitter les espaces de travail, rétention est basée sur l’espace de travail hello niveau tarifaire.

> [!NOTE]
> Microsoft apporte la confidentialité de hello tooprotect engagements forts et sécurité de ces données. Microsoft respecte les instructions de sécurité et de conformité toostrict : du codage toooperating un service. Pour plus d’informations sur la gestion des données et la confidentialité, lisez [Sécurité des données d’Azure Security Center](security-center-data-security.md).
> 

## <a name="ongoing-security-monitoring"></a>Surveillance continue de la sécurité
Après la configuration initiale et l’application des recommandations du centre de sécurité, étape suivante de hello est prise en compte de processus opérationnels du centre de sécurité.

tooaccess centre de sécurité à partir de hello portail Azure, vous pouvez cliquer sur **Parcourir** et type **centre de sécurité** Bonjour **filtre** champ. vues Hello que hello utilisateur obtient varient selon les filtres toothese appliqué, exemple hello ci-dessous montre un environnement avec nombreux problèmes toobe traités :

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Centre de sécurité n’interfère pas avec les procédures de fonctionnement normales, elle passivement surveiller vos déploiements et des recommandations basées sur des stratégies de sécurité hello que vous avez activé.

Lorsque vous choisissez d’abord dans toouse centre de sécurité pour votre environnement Azure actuel, assurez-vous que vous passez en revue toutes les recommandations, ce qui peuvent être effectuées dans hello **recommandations** vignette ou par ressource (**de calcul** **Réseau**, **stockage & données**, **Application**).

Une fois que vous adressez toutes les recommandations, hello **prévention** section doit être verte pour toutes les ressources qui ont été traités. Analyse en cours à ce stade devient plus facile vous prendra uniquement des actions en fonction des modifications dans les vignettes de contrôle d’intégrité et les recommandations la sécurité des ressources hello.

Hello **détection** section est plus réactive, il s’agit des alertes concernant les problèmes qui sont soit ayant lieu à présent, ou s’est produite dans hello passée et ont été détectés par les contrôles de centre de sécurité et les systèmes tiers 3e. vignette d’alertes de sécurité Hello affiche les graphiques à barres qui représentent le nombre de hello d’alertes de détection de menaces qui ont été trouvés dans chaque jour et leur distribution parmi les catégories de gravité différent hello (faible, moyen, élevé). Pour plus d’informations sur les alertes de sécurité, consultez [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> Vous pouvez aussi tirer parti de Microsoft Power BI toovisualize vos données de centre de sécurité. Voir [Obtenir des informations à partir des données du Centre de sécurité Azure à l’aide de Power BI](security-center-powerbi.md).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Surveillance des ressources nouvelles ou modifiées
La plupart des environnements Azure sont dynamiques, avec des nouvelles ressources ajoutées ou retirées régulièrement, des configurations ou des modifications, etc. Centre de sécurité permet de vous assurer d’avoir visibilité sur l’état de la sécurité de ces nouvelles ressources hello.

Lorsque vous ajoutez de nouvelles ressources (machines virtuelles, les bases de données SQL) tooyour environnement Azure, le centre de sécurité sera automatiquement détecter ces ressources et de commencer toomonitor leur sécurité. Cela inclut également les rôles Web et les rôles de travail PaaS. Si la collecte de données est activée dans hello [stratégie de sécurité](security-center-policies.md), d’autres fonctionnalités d’analyse seront activée automatiquement pour vos ordinateurs virtuels.

![Principaux aspects](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. Pour les machines virtuelles, cliquez sur **Compute**, sous la section **Prévention**. Des problèmes avec l’activation de données ou des recommandations associées seront visible dans hello **vue d’ensemble** onglet, et **analyse les recommandations** section.
2. Hello de vue **recommandations** toosee, le cas échéant, les risques de sécurité ont été identifiés pour la ressource hello.
3. Il est très courant que lorsque les nouvelles machines virtuelles sont ajoutés tooyour environnement, seul système d’exploitation de hello est initialement installé. propriétaire de la ressource Hello peut-être certains toodeploy temps toutes les applications qui seront utilisées par ces machines virtuelles.  Dans l’idéal, vous devez savoir intention de hello finale de cette charge de travail. Il va toobe un serveur d’applications ? Selon ce que cela nouvelle charge de travail est continu toobe, vous pouvez activer des hello approprié **stratégie de sécurité**, qui est la troisième étape de hello dans ce flux de travail.
4. Comme de nouvelles ressources sont ajoutées tooyour environnement Azure, il est possible que les nouvelles alertes s’affichent dans hello **alertes de sécurité** vignette. Toujours vérifier s’il existe de nouvelles alertes dans cette vignette et prendre des mesures en fonction des recommandations de tooSecurity Center.

Vous pouvez également tooregularly moniteur hello état existant ressources tooidentify des modifications de configuration que vous avez créé des risques de sécurité, dérive à partir des lignes de base recommandées et alertes de sécurité. Démarrez au tableau de bord de centre de sécurité hello. À partir de là, vous avez trois tooreview principales zones de manière cohérente.

![Opérations](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. Hello **prévention** Panneau de la section fournit des ressources clés de tooyour accès rapide. Utilisez cette option de toomonitor calcul, de mise en réseau, stockage et les données et les Applications.
2. Hello **recommandations** Panneau de configuration vous permet de recommandations du centre de sécurité tooreview. Au cours de votre analyse en cours, vous pouvez constater que vous n’avez recommandations sur une base quotidienne, ce qui est normale puisque vous traité toutes les recommandations sur la configuration de centre de sécurité initiale hello. Pour cette raison, vous a ne peut-être pas nouvelles informations de cette section tous les jours et doit simplement tooaccess si besoin est.
3. Hello **détection** section peut changer sur une base très fréquente ou très peu fréquente. Passez toujours en revue les alertes de sécurité et prenez des mesures en fonction des recommandations du Centre de sécurité.

## <a name="incident-response"></a>Réponse aux incidents
Centre de sécurité détecte et vous avertit toothreats qu’ils se produisent. Organisations doivent analyser de nouvelles alertes de sécurité et agir en tant que nécessaire tooinvestigate davantage ou corriger les attaques de hello. Pour plus d’informations sur le fonctionnement de la détection des menaces par le Centre de sécurité, voir [Fonctionnalités de détection d’Azure Security Center](security-center-detection-capabilities.md).

Cet article n’est pas tooassist intention de hello vous créez votre propre plan de réponse aux incidents, nous allons toouse réponse de sécurité Microsoft Azure dans le cycle de vie des Cloud hello en tant que base de hello pour les étapes de la réponse aux incidents. étapes de Hello sont illustrées dans hello suivant schéma :

![Activité suspecte](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> Vous pouvez utiliser hello National Institute of Standards and Technology (NIST) [Guide de la gestion des ordinateurs sécurité Incident](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) comme un tooassist de référence vous aide à créer votre propre.
> 

Vous pouvez utiliser les alertes du centre de sécurité pendant hello suivant les étapes :

* **Détecter**: identifier une activité suspecte dans une ou plusieurs ressources. 
* **Évaluer**: effectuer hello évaluation initiale tooobtain plus d’informations sur les activités suspectes hello.
* **Diagnostiquer**: recourez hello correction étapes tooconduct hello procédure technique tooaddress hello.

Chaque alerte de sécurité fournit des informations qui peuvent être utilisées toobetter comprendre la nature hello d’attaque de hello et suggérer de limiter les risques. Certaines alertes fournissent également des liens tooeither plus d’informations ou tooother les sources d’informations dans Azure. Vous pouvez utiliser les informations de hello fournies pour approfondir l’atténuation de toobegin, et vous pouvez également rechercher des données relatives à la sécurité qui sont stockées dans votre espace de travail.

Hello suivant montre une activité suspecte de RDP se produisent :

![Activité suspecte](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Comme vous pouvez le voir, ce panneau affiche des détails concernant les temps de hello que hello attaque, hello nom d’hôte source, hello cible VM et fournit également des étapes de la recommandation. Dans certains hello circonstances les informations sur la source d’attaque de hello peuvent être vides. Pour plus d’informations sur ce type de comportement, voir [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) (Informations sur la source manquantes dans les alertes Azure Security Center).

Bonjour [comment tooLeverage hello Azure Security Center & Microsoft Operations Management Suite pour une réponse aux incidents](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) vidéo vous pouvez voir certains des démonstrations qui peuvent vous aider à toounderstand utilisation dans chaque centre de sécurité un de ces niveaux.

> [!NOTE]
> Lecture [exploitant Azure Security Center pour la réponse aux incidents](security-center-incident-response.md) pour plus d’informations sur le mode tooassist de fonctionnalités de centre de sécurité toouse pendant votre réponse aux incidents de traitement. 
> 
> 

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment tooplan pour l’adoption du centre de sécurité. toolearn en savoir plus sur le centre de sécurité, voir hello :

* [La gestion et de répondre toosecurity des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) — Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.

