---
title: "meilleures pratiques de sécurité opérationnelle aaaAzure | Documents Microsoft"
description: Cet article fournit un ensemble de bonnes pratiques pour Azure Operational Security.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Bonnes pratiques pour Azure Operational Security
Sécurité opérationnelle Azure fait référence toohello services, des contrôles et toousers disponibles de fonctionnalités pour protéger leurs données, les applications et les autres composants dans Microsoft Azure. Sécurité opérationnelle Azure repose sur une infrastructure qui intègre les connaissances hello acquises via différentes fonctionnalités qui sont tooMicrosoft unique, y compris hello Microsoft du cycle de vie SDL (Security Development), hello Microsoft Security Response Center programme et une connaissance approfondie du paysage des menaces inquiétudes hello.

Dans cet article, nous abordons différentes bonnes pratiques relatives à la sécurité pour les bases de données Azure. Ces recommandations sont dérivées de notre expérience avec la sécurité de la base de données Azure et les expériences hello de clients comme vous-même.

Pour chaque bonne pratique, nous détaillons les éléments suivants :
-   Les meilleures pratiques de hello est
-   Raison pour laquelle vous souhaitez tooenable que les meilleures pratiques
-   Ce que peut être le résultat de hello si vous ne parvenez pas la meilleure pratique de tooenable hello
- Comment vous pouvez apprendre tooenable hello il est recommandé

Cet article Azure meilleures pratiques de sécurité opérationnelle repose sur un avis consensus et les capacités de la plateforme Azure et les ensembles de fonctionnalités, telles qu’elles existent au moment de hello que cet article a été écrit. Avis et les technologies changent au fil du temps et de cet article sera mis à jour sur un tooreflect régulièrement ces modifications.

Les bonnes pratiques pour Azure Operational Security qui sont abordées dans le cadre de cet article sont les suivantes :

-   Surveiller, gérer et protéger l’infrastructure cloud
-   Gérer l’identité et implémenter l’authentification unique (SSO)
-   Suivre les demandes, analyser les tendances d’utilisation et diagnostiquer les problèmes
-   Surveiller les services avec une solution de surveillance centralisée
-   Empêcher, détecter et répondre toothreats
-   Surveiller le réseau de bout en bout selon un scénario
-   Sécuriser le déploiement à l’aide d’outils DevOps éprouvés

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>Surveiller, gérer et protéger l’infrastructure cloud
Opérations informatiques est chargé de gérer l’infrastructure de centre de données, des applications et des données, y compris la stabilité de hello et la sécurité de ces systèmes. Toutefois, obtenir les informations de sécurité sur la fréquence à laquelle l’augmentation des environnements informatiques complexes nécessite des organisations toocobble rassemblent des données à partir de plusieurs systèmes de gestion et de sécurité.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.

[Solution de sécurité OMS et d’Audit](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) Active informatique tooactively surveiller toutes les ressources, ce qui peuvent aider à réduire l’impact de hello des incidents de sécurité. Cette solution possède des domaines de sécurité qui peuvent être utilisés pour la surveillance des ressources.

Pour plus d’informations sur OMS, consultez l’article de la hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

toohelp vous empêchez, détecter et répondre toothreats, [Operations Management Suite (OMS) Solution de sécurité et d’Audit](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) recueille et traite les données sur vos ressources, notamment :

-   Journaux des événements de sécurité
-   Suivi d’événements pour les événements Windows (ETW)
-   Événements d’audit AppLocker
-   Journal du pare-feu Windows
-   Événements Advanced Threat Analytics
-   Résultats de l’évaluation de la base de référence
-   Résultats de l’analyse anti-programme malveillant
-   Résultats de l’évaluation des correctifs/mises à jour
-   Syslog de flux de données qui est explicitement activé sur l’agent de hello


## <a name="manage-identity-and-implement-single-sign-on"></a>Gérer l’identité et implémenter l’authentification unique
[Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) est le service Microsoft de gestion des annuaires et des identités, basé sur le cloud, mutualisé.

[Azure AD](https://azure.microsoft.com/services/active-directory/) inclut également une suite complète de fonctionnalités de [gestion d’identité](https://docs.microsoft.com/azure/security/security-identity-management-overview), comme [l’authentification multifacteur](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), l’inscription d’appareil, la gestion de mot de passe libre-service, la gestion de groupes libre-service, la gestion des comptes privilégiés, le contrôle d’accès en fonction du rôle, la surveillance de l’utilisation de l’application, ainsi que la création d’audits complets, la surveillance de la sécurité et la création d’alertes.

Hello suivant de fonctionnalités peut protéger les applications cloud, rationaliser les processus informatiques, réduire les coûts et permettent de garantir que les objectifs de la conformité d’entreprise sont remplies :

-   Gestion des identités et des accès pour le cloud de hello
-   Simplifier l’application de cloud tooany utilisateur access
-   Protégez les données et les applications sensibles
-   Offrir le libre-service à vos employés
-   Intégrer à Azure Active Directory

### <a name="identity-and-access-management-for-hello-cloud"></a>Gestion des identités et des accès pour le cloud de hello
Azure Active Directory (Azure AD) est un vaste [solution cloud de gestion des identités et des accès](https://www.microsoft.com/cloud-platform/identity-management), ce qui vous donne un ensemble robuste de fonctionnalités toomanage utilisateurs et groupes. Il permet de sécuriser l’accès tooon local et cloud d’applications, y compris les services web de Microsoft comme Office 365 et la plupart des logiciels non Microsoft comme une application de service (SaaS).
toolearn plus tooenable protection d’identité dans Azure AD, voir [l’activation de Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable).

### <a name="simplify-user-access-tooany-cloud-app"></a>Simplifier l’application de cloud tooany utilisateur access
[Activer l’authentification unique sur](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) toosimplify toothousands de l’accès utilisateur des applications de cloud à partir des appareils iOS, Android, Windows et Mac. Les utilisateurs peuvent lancer des applications de cloud depuis un panneau d’accès web personnalisé ou d’une application mobile à l’aide des informations d’identification de leur entreprise. Utilisez toogo de module de Proxy d’Application hello Azure AD au-delà des applications SaaS et publier des local web applications tooprovide hautement sécurisé accès à distance et l’authentification unique.

### <a name="protect-sensitive-data-and-applications"></a>Protégez les données et les applications sensibles
Activer [Azure multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) tooprevent non autorisé accéder tooon locaux et cloud des applications en fournissant un niveau supplémentaire d’authentification. Protégez votre entreprise et réduisez les menaces potentielles à l’aide d’alertes et d’une surveillance de la sécurité, ainsi que de rapports basés sur un apprentissage automatique qui identifient les comportements d’accès incohérents.

### <a name="enable-self-service-for-your-employees"></a>Offrir le libre-service à vos employés
Déléguer des employés de tooyour des tâches importantes, telles que la réinitialisation des mots de passe et la création et la gestion des groupes. [Activez la réinitialisation et la modification du mot de passe en libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), ainsi que la gestion de groupes en libre-service avec Azure AD.

### <a name="integrate-with-azure-active-directory"></a>Intégrer à Azure Active Directory
Étendre [Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) et n’importe quel autre locales répertoires tooAzure AD tooenable l’authentification unique pour toutes les applications basées sur le cloud. Attributs de l’utilisateur peuvent être l’annuaire du cloud tooyour automatiquement synchronisées à partir de tous les types de répertoires locaux.

toolearn plus d’informations sur l’intégration d’Azure Active Directory et comment tooenable, lisez l’article de hello [intégrer vos annuaires locaux avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>Suivre les demandes, analyser les tendances d’utilisation et diagnostiquer les problèmes
[L’analyse du stockage Azure](https://docs.microsoft.com/azure/storage/storage-analytics) effectue la journalisation et fournit les données d’indicateurs de performance d’un compte de stockage. Vous pouvez utiliser cette tootrace des demandes de données, analyser les tendances d’utilisation et diagnostiquer les problèmes avec votre compte de stockage.

Les métriques de Storage Analytics sont activées par défaut pour les nouveaux comptes de stockage. Vous pouvez activer la journalisation et configurer des métriques et la journalisation dans hello portail Azure ; Pour plus d’informations, consultez [surveiller un compte de stockage Bonjour Azure portal](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Vous pouvez également activer Analytique de stockage par programme via l’API REST de hello ou de la bibliothèque cliente de hello. Utilisez hello Set Service Properties opération tooenable stockage Analytique individuellement pour chaque service.

Pour des instructions détaillées sur l’utilisation de stockage Analytique et les autres outils tooidentify, diagnostiquer et résoudre les problèmes liés au stockage Azure, consultez [moniteur, diagnostiquer et résoudre les problèmes de Microsoft Azure Storage](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting).

toolearn plus d’informations sur l’intégration d’Azure Active Directory et comment tooenable, lisez l’article de hello [activation et configuration d’Analytique de stockage](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN).

## <a name="monitoring-services"></a>Surveillance des services
Les applications cloud sont complexes, et se composent de nombreux éléments mobiles. L’analyse fournit des données tooensure que votre application reste opérationnel et en cours d’exécution dans un état sain. Cela permet également vous toostave désactivé des problèmes potentiels ou de dépanner au-delà de celles. En outre, vous pouvez utiliser l’analyse données toogain des informations détaillées relatives à votre application. Ces connaissances peuvent vous aider à tooimprove des performances des applications ou facilité de maintenance, ou automatiser des actions qui nécessiteraient sinon une intervention manuelle.

### <a name="monitor-azure-resources"></a>Surveiller les ressources Azure
[Moniteur de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) est service de plateforme hello qui fournit une source unique pour l’analyse des ressources Azure. Dans le Gestionnaire d’Azure, vous pouvez visualiser, interroger, Router, archiver et agir en conséquence les métriques hello et journaux provenant des ressources dans Azure. Vous pouvez travailler avec ces données à l’aide du Panneau de portail analyse hello, [applets de commande PowerShell analyse](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [inter-plateformes CLI](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), ou [API REST de Azure analyse](https://msdn.microsoft.com/library/dn931943.aspx).

### <a name="enable-autoscale-with-azure-monitor"></a>Activer la mise à l’échelle automatique avec Azure Monitor
Activer [mise à l’échelle de Azure moniteur](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) s’applique uniquement machines toovirtual identiques (mise), services de cloud computing, les plans de service d’application et les environnements app service.

### <a name="manage-roles-permissions-and-security"></a>Gérer la sécurité et les autorisations des rôles
De nombreuses équipes doivent toostrictly [réguler l’accès toomonitoring](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) paramètres et données. Par exemple, si des membres de l’équipe qui travaillent exclusivement sur l’analyse (ingénieurs du support technique, les ingénieurs de devops) ou si vous utilisez un fournisseur de services gérés, vous pouvez toogrant les accès tooonly données d’analyse tout en limitant leur toocreate possibilité, modifier, ou supprimer des ressources.

Cela montre comment tooquickly s’appliquent à un utilisateur de tooa du contrôle RBAC rôle intégré dans Azure ou créer votre propre rôle personnalisé pour un utilisateur ayant besoin de surveillance des autorisations limitées. Il décrit ensuite les considérations de sécurité pour vos ressources de moniteur de Windows Azure et comment vous pouvez limiter l’accès toohello données qu’ils contiennent.

## <a name="prevent-detect-and-respond-toothreats"></a>Empêcher, détecter et répondre toothreats
Détection des menaces de sécurité Center fonctionne en collectant automatiquement les informations de sécurité à partir des ressources Azure, hello réseau et les solutions de partenaire connecté. Il analyse cette information, corrélation souvent des informations provenant de plusieurs sources, les menaces tooidentify. Alertes de sécurité sont définies dans le centre de sécurité ainsi que des recommandations sur la tooremediate hello menace.

-   [Configurez une stratégie de sécurité](https://docs.microsoft.com/azure/security-center/security-center-policies) pour votre abonnement Azure.
-   Hello d’utilisation [recommandations dans le centre de sécurité](https://docs.microsoft.com/azure/security-center/security-center-recommendations) toohelp vous protégez vos ressources Azure.
-   Passez en revue et gérez vos [alertes de sécurité](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) actuelles.

[Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) vous aide à vous empêchez, détectez et répondre toothreats avec une meilleure visibilité et contrôler hello la sécurité de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

Centre de sécurité offre des fonctions de prévention, de détection et de réponse qui sont générées dans tooAzure de menace efficace et facile à utiliser. Ses fonctionnalités principales sont les suivantes :

-   Comprendre l’état de la sécurité dans le cloud
-   Contrôler la sécurité dans le cloud
-   Déployer des solutions de sécurité dans le cloud intégrées en toute simplicité
-   Détecter les menaces et réagir rapidement

### <a name="understand-cloud-security-state"></a>Comprendre l’état de la sécurité dans le cloud
Utilisez Azure Security Center tooget une vue centralisée de l’état de sécurité hello de toutes vos ressources Azure. Un coup de œil, vérifiez que les contrôles de sécurité appropriés hello sont en place et correctement configuré et identifient rapidement toutes les ressources qui nécessitent votre attention.

### <a name="take-control-of-cloud-security"></a>Contrôler la sécurité dans le cloud
Définir [des stratégies de sécurité](https://docs.microsoft.com/azure/security-center/security-center-policies) pour vos abonnements Azure selon tooyour société de sécurité de cloud a besoin, adaptés toohello le type d’applications ou de la sensibilité des données de salutation dans chaque abonnement. Utilisez des propriétaires de ressources prédéfinis de recommandations tooguide tout au long des processus de hello de l’implémentation de contrôles requis : prendre le hasard hello en dehors de la sécurité du cloud.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>Déployer des solutions de sécurité dans le cloud intégrées en toute simplicité
[Activez des solutions de sécurité](https://docs.microsoft.com/azure/security-center/security-center-partner-integration) proposées par Microsoft et ses partenaires, notamment les pare-feu et logiciels anti-programme malveillant les plus performants du secteur. Utilisation simplifiée des solutions de sécurité toodeploy provisionnement : modifications même réseau sont configurées pour vous. Les événements de sécurité émis par des solutions partenaires sont collectés automatiquement pour l’analyse et la création d’alertes.

### <a name="detect-threats-and-respond-fast"></a>Détecter les menaces et réagir rapidement
Anticipez les menaces existantes et futures dans le cloud avec une approche intégrée et pilotée par l’analytique. En associant le savoir-faire et les [renseignements de Microsoft en matière de menaces](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) à l’échelle mondiale à des informations sur des événements liés à la sécurité cloud au sein de vos déploiements Azure, Security Center vous permet de détecter les menaces réelles au plus tôt, et réduit le nombre de faux-positifs. Alertes de sécurité cloud vous permettent de connaître de campagne d’attaque hello, y compris les événements connexes et ressources concernés et proposent des solutions tooremediate émet et récupérer rapidement.

## <a name="end-to-end-scenario-based-network-monitoring"></a>Surveiller le réseau de bout en bout selon un scénario
Les clients créent un réseau de bout en bout dans Azure en orchestrant et composant diverses ressources réseau telles qu’un réseau virtuel, ExpressRoute, Application Gateway, des équilibrages de charge, etc. Analyse est disponible sur chacune des ressources du réseau hello.

[Observateur de réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) est un service régional qui vous permet de toomonitor et diagnostiquer des conditions à un niveau de scénario de réseau dans, vers et à partir d’Azure. Diagnostic de réseau et les outils de visualisation disponibles avec l’Observateur réseau vous aider à comprendre, de diagnostiquer et de mieux réseau de tooyour insights dans Azure.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>Automatisez la surveillance réseau à distance avec la capture de paquets
Surveiller et diagnostiquer les problèmes de mise en réseau sans connexion tooyour virtual machines virtuelles à l’aide de l’Observateur de réseau. Déclencheur [capture des paquets](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) en définir des alertes et obtenir des informations de performances tooreal lors de l’accès au niveau du paquet hello. Quand vous identifiez un problème, vous pouvez l’examiner en détail pour effectuer de meilleurs diagnostics.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>Obtenez des insights sur votre trafic réseau à l’aide des journaux de flux
Acquérez une meilleure compréhension du modèle de trafic de votre réseau à l’aide des [journaux de flux de groupes de sécurité réseau](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview). Les informations fournies par les journaux de flux vous aident à recueillir des données sur la conformité, l’audit et la surveillance de votre profil de sécurité réseau.

### <a name="diagnose-vpn-connectivity-issues"></a>Diagnostiquez les problèmes de connectivité d’un VPN
Observateur réseau fournit vous hello capacité trop[diagnostiquer les problèmes courants de passerelle VPN et les connexions](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity). Ce qui permet de problème de hello tooidentify, mais aussi toouse hello détaillées toohelp créé davantage examiner les journaux.

toolearn plus d’informations sur l’Observateur de réseau tooconfigure et comment tooenable, lisez l’article de hello [configurer Observateur réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="secure-deployment-using-proven-devops-tools"></a>Sécuriser le déploiement à l’aide d’outils DevOps éprouvés
Il existe quelques hello liste des pratiques de DevOps Azure dans cet espace de Cloud Microsoft, ce qui permet aux entreprises et aux équipes de productivité et efficace.

-   **Infrastructure en tant que Code (IaC) :** Infrastructure en tant que Code est un ensemble de techniques et pratiques, ce qui aident les professionnels de l’informatique supprimer charge hello associé à la génération de tooday jour hello et gestion de l’infrastructure modulaire. Il permet aux professionnels de l’informatique toobuild et gérer leur environnement serveur moderne de façon très similaire à celui comment les développeurs de logiciels générer et mettre à jour le code de l’application. Pour Azure, nous avons [Azure Resource Manager]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) permet tooprovision vos applications à l’aide d’un modèle déclaratif. Dans un modèle unique, vous pouvez déployer plusieurs services ainsi que leurs dépendances. Vous utilisez hello même modèle toorepeatedly déployer votre application au cours de chaque étape du cycle de vie application hello.
-   **Intégration continue et déploiement :** vous pouvez configurer vos projets d’équipe Visual Studio Online trop[automatiquement générer et déployer](https://www.visualstudio.com/docs/build/overview) tooAzure web des applications ou services de cloud computing. Visual Studio Online déploie automatiquement les fichiers binaires de hello après avoir effectué une tooAzure build après chaque archivage de code. commande de Package toohello équivalent dans Visual Studio est Hello processus de génération de package décrites ici et procédure de publication hello est toohello équivalentes des commandes de publication dans Visual Studio.
-   **Gestion des versions :** Visual Studio [Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview) est une excellente solution pour l’automatisation du déploiement en plusieurs étapes et hello de la gestion des processus de publication. Créer déploiement continu pipelines toorelease rapide, simple et souvent. Grâce à Release Management, vous pouvez automatiser une très grande partie du processus de mise en production et avoir des workflows d’approbation prédéfinis. Déployer localement et toohello de cloud computing, étendre et personnaliser en fonction des besoins.
-   **Surveillance du niveau de performance des applications :** détectez et résolvez les problèmes, et améliorez en permanence vos applications. Diagnostiquer rapidement les problèmes dans votre application en ligne. Comprendre comment vos utilisateurs l’utilisent. Configuration se fait simple ajout de code JS et une entrée webconfig, et vous voyez les résultats minutes dans le portail hello avec tous les détails de hello. [App insights](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) aide les entreprises pour accélérer la détection de problèmes et de mise à jour.
-   **Charger les tests et la mise à l’échelle :** nous pouvons trouver des problèmes de performances dans notre toomake que notre application est toujours disponible ou de toocater toohello besoins et de qualité de déploiement application tooimprove. Assurez-vous que votre application peut gérer le trafic de votre prochaine campagne de marketing ou de lancement. Commencez à exécuter des [tests de charge](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) informatiques en un minimum de temps avec Visual Studio Online.

## <a name="next-steps"></a>Étapes suivantes
- Découvrez-en plus sur [Azure Operational Security](https://docs.microsoft.com/azure/security/azure-operational-security).
- tooLearn plus [Operations Management Suite | Sécurité et conformité](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Prise en main de la solution Security and Audit Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started)
