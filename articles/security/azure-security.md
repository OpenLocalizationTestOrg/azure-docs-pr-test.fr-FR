---
title: "aaaIntroduction tooAzure sécurité | Documents Microsoft"
description: "Découvrez Azure Security, ses services et son fonctionnement."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>Introduction tooAzure sécurité
## <a name="overview"></a>Vue d'ensemble
Nous savons que la sécurité est une tâche dans le cloud de hello et combien il est important que vous trouvez des informations précises et actuelles sur la sécurité Azure. Un des hello meilleures raisons toouse Azure pour vos applications et services est parti tootake de sa large gamme d’outils de sécurité et des fonctions. Ces outils et les fonctions permettent de rendre des solutions sécurisées toocreate possible sur la plateforme Azure sécurisé de hello. Microsoft Azure assure la confidentialité, l’intégrité et la disponibilité des données client, tout en permettant la gestion transparente des responsabilités.

toohelp vous de mieux comprendre collection hello des contrôles de sécurité implémenté dans Microsoft Azure à partir du client hello et des opérations Microsoft perspectives, ce livre blanc, « Introduction tooAzure sécurité », est écrit tooprovide un vision détaillée de sécurité hello disponible avec Microsoft Azure.

### <a name="azure-platform"></a>Plateforme Azure
Azure est une plateforme de services de cloud public qui prend en charge un large éventail de systèmes d’exploitation, de langages de programmation, d’infrastructures, d’outils, de bases de données et d’appareils. Elle permet d’exécuter des conteneurs Linux avec l’intégration de Docker, de créer des applications avec JavaScript, Python, .NET, PHP, Java et Node.js, de créer des serveurs principaux pour des appareils iOS, Android et Windows.

Services de cloud public Azure prend en charge hello mêmes technologies des millions de développeurs et professionnels de l’informatique s’appuient sur déjà et faites confiance. Lorsque vous générez sur ou migrez les ressources informatiques à, un fournisseur de services de cloud public vous recourez tooprotect des capacités de cette organisation vos applications et les données avec les contrôles de hello et les services de hello ils sécuriser toomanage hello de votre nuage ressources.

L’infrastructure Azure est conçu de tooapplications d’installation pour l’hébergement des millions de clients simultanément, et fournit une base digne de confiance sur lesquelles les entreprises capable de répondre aux impératifs de sécurité.

En outre, Azure vous offre un large éventail de toocontrol de capacité hello et les options de sécurité configurables leur afin que vous pouvez personnaliser les exigences uniques de sécurité toomeet hello des déploiements de votre organisation. Ce document vous permet de comprendre comment les fonctionnalités de sécurité d’Azure peuvent vous aider à répondre à ces besoins.

> [!Note]
> Hello principal de ce document porte sur les contrôles des clients que vous pouvez utiliser toocustomize et augmenter la sécurité de vos applications et services.
>
> Nous fournissent des informations de vue d’ensemble, mais pour plus d’informations sur la façon dont Microsoft sécurise hello plateforme Azure lui-même, consultez les informations fournies dans hello [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx).

### <a name="abstract"></a>Résumé
Au départ, les migrations de cloud public pilotées par tooinnovate économies et l’agilité de coût. La sécurité a été considérée comme un problème majeur pendant longtemps, voire un frein à la migration cloud public. Toutefois, sécurité de cloud public est passée majeur tooone concernent des pilotes hello pour la migration de cloud. Raisonnement Hello derrière cela est hello supérieure permet grand cloud public fournisseurs tooprotect des applications de service hello de données et des composants de nuage.

L’infrastructure Azure est conçu de tooapplications de fonctionnalité hello pour l’hébergement des millions de clients simultanément, et fournit une base fiable sur laquelle entreprises peuvent répondre aux besoins de leur sécurité. En outre, Azure vous offre un large éventail de toocontrol de capacité hello et les options de sécurité configurables les afin que vous pouvez personnaliser les exigences uniques de hello toomeet sécurité de vos déploiements de toomeet votre service informatique stratégies de contrôle et respecter tooexternal réglementaires.

Ce document décrit toosecurity d’approche de Microsoft au sein de la plateforme de cloud de Microsoft Azure hello :
* Fonctionnalités de sécurité implémentées par toosecure hello infrastructure Azure, les données client et les applications Microsoft.
* Azure services et la sécurité fonctionnalités disponible tooyou toomanage hello sécurité des Services de hello et vos données au sein de vos abonnements Azure.

## <a name="summary-azure-security-capabilities"></a>Résumé des fonctionnalités de sécurité Azure
suivant de table Hello fournit une brève description des fonctionnalités de sécurité hello implémentés par Microsoft toosecure hello infrastructure Azure, les données des clients et des applications sécurisées.
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>Sécurité fonctionnalités implémentées tooSecure hello plateforme Azure :
fonctionnalités Hello répertoriées qui suivent sont fonctionnalités que vous pouvez consulter assurance de hello tooprovide que hello que plateforme Azure est gérée de manière sécurisée. Des liens sont indiqués pour permettre d’explorer davantage comment Microsoft traite les questions de confiance des clients dans quatre domaines : plateforme sécurisée, confidentialité et contrôles, conformité et transparence.


| [Plateforme sécurisée](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [Confidentialité et contrôles](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[Conformité](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [Transparence](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [Cycle de développement de sécurité](https://www.microsoft.com/en-us/sdl/), audits internes | [Gérer vos données de tout temps hello](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [Centre de gestion de la confidentialité](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Comment Microsoft sécurise les données client dans les services Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| [Formation obligatoire sur les mesures de sécurité, vérifications de la formation](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc) |  [Contrôler l’emplacement des données](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [Hub des contrôles communs](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub) |[Comment Microsoft gère l’emplacement des données dans les services Azure](http://azuredatacentermap.azurewebsites.net/)|
| [Test de pénétration](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc), [détection d’intrusion, DDoS](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen), [audits et journalisation](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [Fournir l’accès aux données selon vos conditions](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [Hello Cloud Services échéance Diligence liste de vérification](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[Qui dans Microsoft peut accéder à vos données dans quelles conditions](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [Centre de données ultramoderne](https://www.microsoft.com/en-us/cloud-platform/global-datacenters), sécurité physique, [réseau sécurisé](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [Réponse mise en œuvre toolaw](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [Conformité par service, site et secteur](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Comment Microsoft sécurise les données client dans les services Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)|
|  [Réponse aux incidents de sécurité](http://aka.ms/SecurityResponsepaper), [responsabilité partagée](http://aka.ms/sharedresponsibility) |[Normes de confidentialité strictes](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [Passer en revue la certification des services Azure, concentrateur de transparence](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>Fonctionnalités de sécurité offertes par Azure tooSecure de données et d’Application
Selon le modèle de service de cloud hello, il incombe variable pour qui est responsable de la gestion de la sécurité hello de l’application hello ou un service. Il existe des fonctions disponibles dans tooassist de plateforme Azure hello vous répondre à ces responsabilités grâce à des fonctionnalités intégrées et les solutions qui peuvent être déployées dans un abonnement Azure de partenaire.

les fonctionnalités intégrées Hello sont organisées dans les zones fonctionnelles de six (6) : opérations, Applications, stockage, mise en réseau, de calcul et identité. Des détails supplémentaires sur les fonctionnalités de hello et fonctions disponibles dans hello plateforme Azure dans ces domaines six (6) sont fournies par le biais des informations de synthèse.

## <a name="operations"></a>Opérations
Cette section contient des informations supplémentaires sur les fonctionnalités clés des opérations de sécurité et des informations de synthèse sur ces fonctionnalités.

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Tableau de bord Sécurité et audit d’Operations Management Suite
Hello [solutions OMS sécurité et Audit](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) fournit une vue globale de votre organisation posture de sécurité informatique avec [requêtes de recherche intégrées](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/) pour les problèmes importants qui requièrent votre attention. Hello [sécurité et Audit](https://technet.microsoft.com/library/mt484091.aspx) tableau de bord est l’écran d’accueil hello pour tous les éléments liés toosecurity d’OMS. Il permet de comprendre principales hello état de sécurité de vos ordinateurs. Il inclut également hello capacité tooview tous les événements de hello dernières 24 heures, 7 jours, ou n’importe quel autre intervalle de temps personnalisé.

En outre, vous pouvez configurer OMS sécurité et conformité trop[automatiquement exécuter des actions spécifiques](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/) lorsqu’un événement spécifique est détecté.

### <a name="azure-resource-manager"></a>Azure Resource Manager
[Le Gestionnaire de ressources Azure ](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) vous permet de toowork des ressources de hello dans votre solution en tant que groupe. Vous pouvez déployer, mettre à jour ou supprimer toutes les ressources hello pour votre solution dans une opération unique et coordonnée. Vous utilisez un [modèle Azure Resource Manager](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/) de déploiement pouvant fonctionner dans différents environnements (environnements de test, intermédiaire et de production). Gestionnaire de ressources fournit la sécurité, l’audit et le balisage des fonctionnalités toohelp gérer vos ressources après le déploiement.

Déploiements de basées sur un modèle de gestionnaire de ressources Azure d’améliorer la sécurité de hello des solutions déployées dans Azure, car les contrôler les paramètres de sécurité standard et peut être intégré dans des déploiements basées sur un modèle standardisés. Cela réduit le risque de hello d’erreurs de configuration de sécurité qui peut avoir lieu pendant les déploiements de manuels.

### <a name="application-insights"></a>Application Insights
[Application Insights](https://docs.microsoft.com/azure/application-insights/) est un service de gestion des performances des applications (APM) extensible destiné aux développeurs web. Application Insights vous permet de surveiller vos applications web dynamiques et de détecter automatiquement les anomalies des performances. Il inclut toohelp d’outils puissants analytique vous diagnostiquez des problèmes et toounderstand ce que les utilisateurs effectuent réellement avec vos applications. Il analyse votre application tout temps hello qu’il est en cours d’exécution, pendant le test et une fois que vous avez publié ou déployé.

Application Insights crée des graphiques et des tableaux qui vous montre, par exemple, les heures de la journée, vous obtenez la plupart des utilisateurs, comment est de l’application hello réactive, et des services et qu'il est pris en charge par n’importe quel externe qui il dépend.

S’il existe des incidents, les échecs ou les problèmes de performances, vous pouvez rechercher dans les données de télémétrie hello dans la cause de détail toodiagnose hello. Et le service de hello envoie des messages électroniques si des modifications sont effectuées dans la disponibilité de hello et les performances de votre application. Application Insight devient donc un outil de sécurité utile car elle permet de disponibilité de hello dans un triangle de sécurité de disponibilité, intégrité et la confidentialité de hello.

### <a name="azure-monitor"></a>Azure Monitor
[Moniteur de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) offre une visualisation, requête, routage, génération d’alertes, à l’échelle automatique et l’automatisation des données à la fois à partir de hello infrastructure Azure ([le journal d’activité](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) et chaque ressource Azure ([ Journaux de diagnostic](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)). Vous pouvez utiliser le moniteur de Windows Azure tooalert vous sur les événements liés à la sécurité qui sont générés dans les journaux Azure.

### <a name="log-analytics"></a>Log Analytics
[Ouvrez une session Analytique](https://azure.microsoft.com/documentation/services/log-analytics/) dans le cadre du [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) – fournit une solution de gestion informatique sur site et infrastructure de nuage de tiers (par exemple, AWS) en outre tooAzure ressources. Les données à partir du moniteur de Azure peuvent être acheminées directement tooLog Analytique afin de voir les journaux et les métriques pour votre environnement complet dans un seul emplacement.

Analytique de journal peut être un outil utile dans les analyses d’investigation et autres analyses de sécurité, comme outil de hello permet de vous tooquickly recherche de grandes quantités de relatives à la sécurité des entrées avec une approche de requête souple. Par ailleurs, des [journaux pare-feu et proxy locaux peuvent être exportés dans Azure et mis à disposition pour des analyses dans Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall).

### <a name="azure-advisor"></a>Azure Advisor
[Assistant Azure](https://docs.microsoft.com/azure/advisor/) est un consultant personnalisé de cloud qui vous permet de toooptimize vos déploiements Azure. Il analyse les données de télémétrie d’utilisation et la configuration de vos ressources. Puis il recommande des solutions toohelp améliorer hello [performances](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations), [sécurité](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations), et [haute disponibilité](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations) de vos ressources lors de la recherche pour les opportunités trop[réduire votre Azure globale dépenses](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations). Azure Advisor fournit des recommandations en termes de sécurité, qui peuvent améliorer sensiblement votre sécurité globale pour les solutions que vous déployez dans Azure. Ces recommandations sont tirées de l’analyse de la sécurité effectuée par [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro).

### <a name="azure-security-center"></a>Azure Security Center
[Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) vous aide à vous empêchez, détectez et répondre toothreats avec une meilleure visibilité et contrôler hello la sécurité de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

En outre, Azure Security Center aide aux opérations de sécurité en vous fournissant un tableau de bord qui présente les alertes et les recommandations qui peuvent être traitées immédiatement. Souvent, vous pouvez corriger les problèmes liés à un seul clic dans la console du centre de sécurité Azure hello.
## <a name="applications"></a>Applications
section de Hello fournit des informations supplémentaires concernant les fonctionnalités clés de l’application sécurité et des informations sur ces fonctionnalités.

### <a name="web-application-vulnerability-scanning"></a>Analyse de la vulnérabilité des applications web
Un des hello plus simple façons tooget main des tests pour des vulnérabilités sur votre [application de Service d’applications](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) est toouse hello [intégration à Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) analyse sur des vulnérabilités en un clic tooperform votre application. Vous pouvez afficher les résultats des tests hello dans un rapport facile à comprendre et découvrez comment toofix chaque problème de sécurité avec des instructions pas à pas.

### <a name="penetration-testing"></a>Test de pénétration
Si vous préférez tooperform votre propre intrusion des tests ou souhaitez toouse une autre suite de l’analyseur ou fournisseur, vous devez suivre hello [intrusion Azure tester le processus d’approbation](https://security-forms.azure.com/penetration-testing/terms) et d’obtenir ce type de préalable tooperform hello souhaité tests.

### <a name="web-application-firewall"></a>Pare-feu d’application web
Hello pare-feu d’applications web (WAF) dans [passerelle d’Application Azure](https://azure.microsoft.com/services/application-gateway/) vous aide à protéger les applications web à partir des attaques courantes basée sur le web telles que l’injection SQL, les attaques de script entre sites et le piratage de session. Il est fourni préconfiguré avec la protection contre les menaces identifiées par hello [ouvrir Web Application sécurité projet (OWASP avoir) en tant que hello top 10 vulnérabilités courantes](https://msdn.microsoft.com/library/).

### <a name="authentication-and-authorization-in-azure-app-service"></a>Authentification et autorisation dans Azure App Service
[Application Service authentification / autorisation](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) est une fonctionnalité qui fournit un moyen pour toosign de votre application dans les utilisateurs afin que vous n’avez pas toochange code sur le serveur principal d’application hello. Il fournit un moyen simple de tooprotect votre application et travailler avec des données par l’utilisateur.

### <a name="layered-security-architecture"></a>Architecture de sécurité multiniveau
Dans la mesure où les [environnements App Service](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro) fournissent un environnement d’exécution isolé déployé dans un [réseau virtuel Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview), les développeurs peuvent créer une architecture de sécurité multiniveau offrant différents niveaux d’accès réseau pour chaque couche Application. Une volonté commune est toohide API principaux à partir d’un accès général à Internet et autoriser uniquement les toobe API appelée par les applications web en amont. [Groupes de sécurité (NSG) réseau](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/) peut être utilisé sur les sous-réseaux de réseau virtuel Azure contenant les environnements App Service toorestrict accès public tooAPI applications.

### <a name="web-server-diagnostics-and-application-diagnostics"></a>Diagnostics de serveur web et diagnostics d’application
Applications de Service d’applications web fournissent des fonctionnalités de diagnostic enregistrées les informations de serveur web de hello et application web de hello. Ces informations sont réparties, en toute logique, en [diagnostics de serveur web](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) et en [diagnostics d’application](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx). Le serveur web inclut deux avancées majeures dans le diagnostic des problèmes et leur résolution sur les sites et dans les applications.

première nouvelle fonctionnalité Hello est informations d’état en temps réel sur les pools d’applications, les processus de travail, les sites, domaines d’application et les demandes en cours d’exécution. avantages de nouvelle deuxième Hello sont hello des événements de suivi détaillés qui effectuent le suivi d’une demande tout au long du processus de demande et de réponse complet hello.

collection de hello tooenable de ces événements de trace, IIS 7 peut être journaux de trace complète capture tooautomatically configuré, au format XML, pour toute demande spécifique basé sur les codes de réponse de temps écoulé ou d’erreur.

#### <a name="web-server-diagnostics"></a>Diagnostics de serveur web
Vous pouvez activer ou désactiver hello suivant les types de journaux :

-   Messages d’erreur détaillés : informations d’erreur détaillées pour les codes d’état HTTP qui indiquent un échec (code d’état 400 ou supérieur). Il peut contenir des informations qui peuvent aider à déterminer pourquoi les serveur hello a renvoyé un code d’erreur hello.

-   Échec de suivi des demandes - des informations détaillées sur les demandes ayant échoué, y compris une trace de hello IIS composants utilisés tooprocess hello demande et de durée hello dans chaque composant. Cela peut être utile si vous essayez de performances de site tooincrease ou Isolez la cause une toobe d’erreur HTTP spécifique retourné.

-   Web journalisation du serveur - informations sur les transactions HTTP en utilisant le format de fichier journal étendu hello W3C. Cela est utile lors de la détermination des métriques d’un site global comme nombre hello de demandes traitées ou nombre de requêtes qui proviennent d’une adresse IP spécifique.

#### <a name="application-diagnostics"></a>diagnostics d’application
[Diagnostics d’application](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) vous permet de toocapture les informations produites par une application web. Applications ASP.NET peuvent utiliser hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) classe toolog informations toohello application diagnostics se connecter. Dans Application Diagnostics, il existe deux principaux types d’événements, ceux liés tooapplication performances et celles ayant trait à des erreurs et échecs de tooapplication. Hello échecs et les erreurs peuvent être divisés en problèmes de connectivité, de sécurité et d’échec. Les problèmes d’échec sont problème tooa généralement associées avec le code d’application hello.

Dans Diagnostic d’application, vous pouvez afficher les événements regroupés comme suit :

-   Tout (affiche tous les événements)
-   Erreurs d’application (affiche les événements d’exception)
-   Performances (affiche les événements de performance)

## <a name="storage"></a>Storage
section de Hello fournit des informations supplémentaires concernant les fonctionnalités clés de stockage Azure sécurité et des informations sur ces fonctionnalités.

### <a name="role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle
Vous pouvez sécuriser un compte de stockage en utilisant le contrôle d’accès en fonction du rôle (RBAC). Restreindre l’accès basé sur hello [devez tooknow](https://en.wikipedia.org/wiki/Need_to_know) et [moindre privilège](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principes de sécurité est impérative pour les organisations qui souhaitent utiliser les stratégies de sécurité tooenforce pour accéder aux données. Ces droits d’accès sont accordées en attribuant hello toogroups du rôle RBAC approprié et les applications à une certaine étendue. Vous pouvez utiliser [rôles RBAC intégrés](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles), telles que contributeur du compte de stockage, tooassign privilèges toousers. Accéder aux clés de stockage de toohello pour un compte de stockage à l’aide de hello [Azure Resource Manager](https://docs.microsoft.com/azure/storage/storage-security-guide) modèle peut être contrôlé via le contrôle d’accès en fonction du rôle (RBAC).

### <a name="shared-access-signature"></a>Signature d’accès partagé
A [signature d’accès partagé (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) fournit tooresources accès délégué dans votre compte de stockage. Hello SAS signifie que vous pouvez accorder à qu'un client limitée tooobjects autorisations dans votre compte de stockage pour une période spécifiée et avec un jeu d’autorisations spécifié. Vous pouvez accorder ces autorisations limitées sans avoir tooshare vos clés d’accès de compte.

### <a name="encryption-in-transit"></a>Chiffrement en transit
Le chiffrement en transit est un mécanisme de protection des données transmises sur des réseaux. Le stockage Azure vous permet de sécuriser les données à l’aide des éléments suivants :
-   Le [chiffrement au niveau du transport](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit) (HTTPS, par exemple) lorsque vous transférez des données vers ou à partir de Stockage Azure.

-   Le [chiffrement câblé](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares), par exemple le [chiffrement SMB 3.0](https://docs.microsoft.com/azure/storage/storage-security-guide) pour les [partages de fichiers Azure](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files).

-   Chiffrement côté client, tooencrypt les données de salutation avant leur transfert dans le stockage et les données de salutation toodecrypt après leur transfert hors stockage.

### <a name="encryption-at-rest"></a>Chiffrement au repos
Pour de nombreuses organisations, le chiffrement des données au repos est une étape obligatoire du processus de gestion de la confidentialité, de la conformité et de la souveraineté des données. Trois fonctionnalités de la sécurité du stockage Azure fournissent un chiffrement des données « au repos ».

-   [Chiffrement du Service Storage](https://docs.microsoft.com/azure/storage/storage-service-encryption) vous permet de toorequest que service de stockage hello chiffrer automatiquement des données lors de l’écriture de tooAzure stockage.

-   [Le chiffrement côté client](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) fournit également la fonctionnalité hello du chiffrement au repos.

-   [Le chiffrement des disques Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) vous permet des disques tooencrypt hello du système d’exploitation et des disques de données utilisées par une machine virtuelle IaaS.

### <a name="storage-analytics"></a>Storage Analytics
[L’analyse du stockage Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) effectue la journalisation et fournit les données d’indicateurs de performance d’un compte de stockage. Vous pouvez utiliser cette tootrace des demandes de données, analyser les tendances d’utilisation et diagnostiquer les problèmes avec votre compte de stockage. Stockage Analytique enregistre des informations détaillées sur le service de stockage tooa demandes réussies et ayant échoué. Ces informations peuvent être utilisées toomonitor des requêtes individuelles et les problèmes de toodiagnose avec un service de stockage. Les demandes sont enregistrées sur la base du meilleur effort. Hello, les types de demandes authentifiées suivants est enregistré :
-   Demandes ayant réussi.

-   Demandes ayant échoué, y compris les erreurs de délai d'expiration, limitation, réseau, autorisation et autres erreurs.

-   Demandes utilisant une signature d'accès partagé (SAS), y compris les demandes ayant réussi et ayant échoué.

-   Demande des données tooanalytics.

### <a name="enabling-browser-based-clients-using-cors"></a>Activation de clients basés sur le navigateur à l’aide de CORS
[Partage de ressources Cross-Origin (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) est un mécanisme qui permet des domaines toogive autre autorisation pour accéder aux ressources de l’autre. Hello Agent utilisateur envoie tooensure en-têtes supplémentaires que le code JavaScript de hello chargé à partir d’un domaine peut tooaccess les ressources situés dans un autre domaine. domaine de ce dernier Hello répond ensuite avec les en-têtes supplémentaires autoriser ou refuser l’accès de domaine d’origine hello tooits ressources.

Les services de stockage Azure prend désormais en charge CORS afin qu’une fois que vous définissez les règles CORS hello pour le service de hello, une demande authentifiée effectuée au service de hello à partir d’un autre domaine soit évaluée toodetermine si elle est autorisée selon les règles de toohello que vous avez spécifié.
## <a name="networking"></a>Mise en réseau
section de Hello fournit des informations supplémentaires concernant les fonctionnalités clées dans le réseau Azure sécurité et des informations sur ces fonctionnalités.

### <a name="network-layer-controls"></a>Contrôles de la couche réseau
Contrôle d’accès réseau est act hello de limitation de tooand de connectivité à partir des appareils ou des sous-réseaux et représente hello principaux de sécurité réseau. objectif de Hello de contrôle d’accès réseau est toomake assurer que vos machines virtuelles et les services sont accessibles tooonly utilisateurs et périphériques toowhich auxquels vous souhaitez les.

#### <a name="network-security-groups"></a>Network Security Group
A [groupe de sécurité réseau (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) est une base pare-feu et filtrage des paquets avec état permet l’accès toocontrol vous selon un [5-tuple](https://www.techopedia.com/definition/28190/5-tuple). Les groupes de sécurité réseau n’effectuent pas d’inspection de la couche d’application ni de contrôles d’accès authentifiés. Ils peuvent être utilisés toocontrol trafic entre sous-réseaux au sein d’un réseau virtuel Azure et le trafic entre un réseau virtuel Azure et les hello Internet.

#### <a name="route-control-and-forced-tunneling"></a>Contrôle du routage et tunneling forcé
Hello capacité toocontrol comportement de routage sur vos réseaux virtuels Azure est une fonctionnalité de contrôle de sécurité et d’accès réseau critiques. Par exemple, si vous souhaitez toomake assurer que tous les tooand le trafic à partir de votre réseau virtuel Azure traverse ce dispositif de sécurité virtuel, vous devez toocontrol en mesure de toobe et personnalisez le comportement de routage. Pour ce faire, vous pouvez configurer des itinéraires définis par l’utilisateur dans Azure.

[Itinéraires définis par l’utilisateur](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) permettent de toocustomize des chemins d’accès entrants et sortants pour le trafic vers et depuis des ordinateurs virtuels individuels ou des sous-réseaux tooinsure hello plus sécurisé possible d’itinéraire. [Le tunneling forcé](https://www.petri.com/azure-forced-tunneling) est un mécanisme que vous pouvez utiliser tooensure vos services ne sont pas autorisées tooinitiate un toodevices de connexion sur Internet de hello.

Cela est différent d’est en mesure de tooaccept les connexions entrantes et répond ensuite toothem. Serveurs web frontaux doivent toorequests toorespond à des hôtes Internet et pour le trafic provenant d’Internet est autorisé entrant toothese web des serveurs hello peut répondre.

Le tunneling forcé est couramment utilisés tooforce le trafic sortant toohello Internet toogo par l’intermédiaire de proxys de sécurité locale et les pare-feu.

#### <a name="virtual-network-security-appliances"></a>Appliances de sécurité de réseau virtuel
Tandis que les groupes de sécurité réseau, les itinéraires définis par l’utilisateur et le tunneling forcé vous fournissent un niveau de sécurité au niveau des couches de transport et de réseau hello Hello [modèle OSI](https://en.wikipedia.org/wiki/OSI_model), il peut arriver lorsque vous souhaitez que la sécurité tooenable à des niveaux supérieurs de pile de Hello. Vous pouvez accéder à ces fonctionnalités avancées de sécurité réseau via une solution d’appliance de sécurité réseau de partenaire Azure. Vous pouvez trouver des solutions de sécurité de réseau partenaire Azure plus récente de hello en visitant hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) et en recherchant « sécurité » et « sécurité réseau. »

### <a name="azure-virtual-network"></a>Réseau virtuel Azure

Un réseau virtuel Azure (VNet) est une représentation de votre propre réseau dans le cloud de hello. Il s’agit d’une isolation logique de hello réseau Azure fabric dédié tooyour abonnement. Vous pouvez contrôler entièrement les blocs d’adresses IP hello, les paramètres DNS, les stratégies de sécurité et les tables d’itinéraires au sein de ce réseau. Vous pouvez segmenter votre réseau virtuel en sous-réseaux et placer des machines virtuelles IaaS Azure et/ou des [services cloud (instances de rôle PaaS)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) sur des réseaux virtuels Azure.

En outre, vous pouvez vous connecter hello réseau virtuel tooyour sur réseau local à l’aide de hello [les options de connectivité](https://docs.microsoft.com/azure/vpn-gateway/) disponibles dans Azure. Fondamentalement, vous pouvez développer votre tooAzure réseau, avec un contrôle complet sur les blocs d’adresses IP avec avantage hello d’échelle de l’entreprise Qu'azure fournit.

La mise en réseau Azure prend en charge différents scénarios d’accès à distance sécurisé, entres autres :

-   [Connecter des stations de travail individuelles tooan réseau virtuel Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [Se connecter tooan de réseau local sur le réseau virtuel Azure avec un réseau privé virtuel](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [Se connecter tooan de réseau local sur le réseau virtuel Azure avec une liaison WAN dédiée](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [Connecter des réseaux virtuels Azure tooeach autres](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>Passerelle VPN
toosend le trafic réseau entre votre réseau virtuel Azure et votre site local, vous devez créer une passerelle VPN pour votre réseau virtuel Azure. Une [passerelle VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) est un type de passerelle de réseau virtuel qui envoie le trafic chiffré à travers une connexion publique. Vous pouvez également utiliser le trafic toosend de passerelles VPN entre réseaux virtuels Azure sur hello l’infrastructure de réseau Azure.

### <a name="express-route"></a>ExpressRoute
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) est une liaison WAN dédiée qui vous permet d’étendre vos réseaux locaux dans hello cloud de Microsoft sur une connexion privée dédiée facilitée par un fournisseur de connectivité.

![ExpressRoute](./media/azure-security/azure-security-fig1.png)

Grâce à ExpressRoute, vous pouvez établir des services de cloud computing tooMicrosoft de connexions, tels que Microsoft Azure, Office 365, CRM Online. La connectivité peut provenir d'un réseau universel (IP VPN), d’un réseau Ethernet point à point ou d’une interconnexion virtuelle via un fournisseur de connectivité dans un centre de colocalisation.

Les connexions ExpressRoute ne pas dépasser hello Internet public et par conséquent, peut être considéré comme plus sûr que les solutions VPN. Ainsi, toooffer de connexions ExpressRoute plus la fiabilité, débits plus importants, latences moindres et une sécurité accrue par rapport aux connexions classiques sur Internet de hello.


### <a name="application-gateway"></a>Application Gateway
Microsoft [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) intègre [Application Delivery Controller (ADC)](https://en.wikipedia.org/wiki/Application_delivery_controller) en tant que service, offrant diverses fonctionnalités d’équilibrage de charge de couche 7 pour votre application.

![Application Gateway](./media/azure-security/azure-security-fig2.png)

Il vous permet de productivité de batterie de serveurs web toooptimize en raison du déchargement du processeur intensif SSL arrêt toohello Application Gateway (également appelé « Déchargement SSL » ou « Le pontage SSL »). Il fournit également des autres fonctionnalités de routage de couche 7, y compris la distribution alternée de trafic entrant d’affinité de session basée sur un cookie, le routage basé sur le chemin d’accès URL et hello capacité toohost plusieurs sites Web derrière une passerelle d’Application unique. La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.

Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement.

L’application offre de nombreuses fonctionnalités Application Delivery Controller (ADC), notamment l’équilibrage de charge HTTP, l’affinité de session basée sur les cookies, le déchargement [SSL (Secure Sockets Layer)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell), les sondes d’intégrité personnalisées, la prise en charge de plusieurs sites, etc.

### <a name="web-application-firewall"></a>Pare-feu d’applications web
Pare-feu d’applications Web est une fonctionnalité de [passerelle d’Application Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) qui assure la protection tooweb les applications qui utilisent la passerelle d’application pour les fonctions de contrôle de remise d’Application (ADC) standard. Pare-feu d’applications Web pour ce faire les protège contre la plupart des hello OWASP avoir top 10 web vulnérabilités courantes.

![Pare-feu d’applications web](./media/azure-security/azure-security-fig1.png)

-   Protection contre les injections de code SQL

-   Protection contre les attaques web courante comme l’injection de commande, les dissimulations de requêtes HTTP, la séparation de réponse HTTP et les attaques RFI (Remote File Inclusion)

-   Protection contre les violations de protocole HTTP

-   Protection contre les anomalies de protocole HTTP comme un agent-utilisateur hôte manquant et les en-têtes Accept

-   Protection contre les robots, les crawlers et les scanneurs

-   Détection des erreurs de configuration d’application courantes (par exemple, Apache, IIS, etc.)


Un tooprotect de pare-feu d’applications web centralisée contre les attaques de web simplifie la gestion de la sécurité et donne une meilleure application de toohello d’assurance contre les menaces d’intrusion hello. Une solution WAF peut réagir également de menace pour la sécurité tooa plus rapide par la mise à jour corrective une vulnérabilité connue à un emplacement central par rapport à la sécurisation de chacune des applications web individuelles. Une application existante passerelles peuvent être convertis, passerelle d’application tooan avec pare-feu d’applications web.
### <a name="traffic-manager"></a>Traffic Manager
Microsoft [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) vous permet de distribution de hello toocontrol du trafic utilisateur pour les points de terminaison de service dans différents centres de données. Les points de terminaison de service pris en charge par Traffic Manager incluent des machines virtuelles Azure, des applications web et des services cloud. Vous pouvez également utiliser Traffic Manager avec des points de terminaison externes non-Azure. Traffic Manager utilise hello système DNS (Domain Name) toodirect client demande du point de terminaison plus approprié toohello selon un [méthode de routage du trafic](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) et l’intégrité de hello de points de terminaison hello.

Traffic Manager fournit une gamme de routage du trafic méthodes toosuit différents besoins des applications, l’intégrité du point de terminaison [analyse](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)et un basculement automatique. Traffic Manager est résilient toofailure, y compris échec hello d’un ensemble de la région Azure.
### <a name="azure-load-balancer"></a>Azure Load Balancer
[Équilibrage de charge Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) offre une haute disponibilité et les performances réseau tooyour applications. Il s’agit d’un équilibreur de charge Layer-4 (TCP, UDP) qui distribue le trafic entrant parmi des instances saines de services définis dans un jeu à charge équilibrée. Azure Load Balancer peut être configuré pour :

-   La charge des machines de solde entrants Internet trafic toovirtual. Cette configuration est appelée [équilibrage de charge avec accès par Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   équilibrer le trafic entre des machines virtuelles dans un réseau virtuel, entre des machines virtuelles dans les services cloud ou entre des ordinateurs locaux et des machines virtuelles dans un réseau virtuel entre différents locaux. Cette configuration est appelée [équilibrage de charge interne](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview). 

- Machine virtuelle spécifique de transférer le trafic externe tooa

### <a name="internal-dns"></a>DNS interne
Vous pouvez gérer la liste hello des serveurs DNS utilisés dans un réseau virtuel dans le portail de gestion de hello, ou dans le fichier de configuration de réseau hello. Client peut ajouter des serveurs DNS de too12 pour chaque réseau virtuel. Lors de la spécification des serveurs DNS, il est important tooverify que vous répertoriez les serveurs DNS du client hello correctes afin que l’environnement du client. Les listes de serveurs DNS ne fonctionnent pas sur le modèle du tourniquet (round-robin). Elles sont utilisées dans l’ordre de hello qu’elles sont spécifiées. Si hello premier serveur DNS de liste de hello est en mesure de toobe atteint, hello utilise ce serveur DNS, que serveur DNS de hello est fonctionne correctement ou non. toochange hello ordre des serveurs DNS pour le réseau virtuel du client, supprimez les serveurs DNS hello à partir de la liste de hello et les ajouter dans l’ordre de hello que le client veut. DNS prend en charge l’aspect de disponibilité hello de triangle de sécurité « CIA » hello.

### <a name="azure-dns"></a>DNS Azure
Hello [Domain Name System](https://technet.microsoft.com/library/bb629410.aspx), ou DNS, est responsable de la traduction (ou la résolution de) un site Web ou un service name tooits adresse IP. [DNS Azure](https://docs.microsoft.com/azure/dns/dns-overview) est un service d’hébergement pour les domaines DNS qui offre une résolution de noms à l’aide de l’infrastructure Microsoft Azure. En hébergeant vos domaines dans Azure, vous pouvez gérer votre serveur DNS les enregistrements à l’aide de hello même des informations d’identification, les API, outils et facturation en tant que vos autres services Azure. DNS prend en charge l’aspect de disponibilité hello de triangle de sécurité « CIA » hello.
### <a name="log-analytics-nsgs"></a>Groupes de sécurité réseau Log Analytics
Vous pouvez activer hello suivant des catégories du journal de diagnostic pour les groupes de sécurité réseau :
-   Événement : Contient des entrées pour le groupe de sécurité réseau, les règles sont tooVMs appliqués et les rôles d’instance en fonction de l’adresse MAC. état Hello pour ces règles est collecté toutes les 60 secondes.

-   Compteur de règles : contient des entrées pour le nombre de fois où chaque règle de groupe de sécurité réseau est appliqué toodeny ou autoriser le trafic.

### <a name="azure-security-center"></a>Azure Security Center
Centre de sécurité vous permet d’empêcher, détecter et répondre toothreats et fournit le renforcer visibilité et contrôler, de sécurité de vos ressources Azure hello. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité. Les recommandations relatives au réseau se concentrent autour des pare-feu, des groupes de sécurité réseau, de la configuration des règles de trafic entrant, et bien plus encore.

Les recommandations disponibles pour le réseau sont les suivantes :

-   [Ajouter un pare-feu de la génération suivante](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) vous recommande d’ajouter un pare-feu de la génération suivante (Conviction) à partir d’un tooincrease de partenaire Microsoft votre protections de sécurité

-   [Acheminer le trafic via Conviction](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only) recommande que vous configurez des règles de groupe (NSG) de sécurité qui force le trafic entrant tooyour machine virtuelle via votre Conviction du réseau.

-   [Activer des groupes de sécurité réseau sur les sous-réseaux ou les machines virtuelles](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups) Recommande d’activer des groupes de sécurité réseau sur les sous-réseaux ou les machines virtuelles.

-   [Restreindre l’accès via un point de terminaison accessible sur Internet](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints) Recommande de configurer des règles de trafic entrant pour les groupes de sécurité réseau.


## <a name="compute"></a>Calcul

section de Hello fournit des informations supplémentaires concernant les fonctionnalités clées dans cette zone et résumé d’informations sur ces fonctionnalités.

### <a name="antimalware--antivirus"></a>Logiciels anti-programmes malveillants et antivirus
Avec Azure IaaS, vous pouvez utiliser les logiciels anti-programme malveillant à partir des fournisseurs de sécurité telles que Microsoft, Symantec, Trend Micro, McAfee et Kaspersky tooprotect vos machines virtuelles à partir de fichiers malveillants, de logiciels de publicité et d’autres menaces. [Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) pour Azure Cloud Services et machines virtuelles offre une fonctionnalité de protection qui permet d’identifier et de supprimer les virus, logiciels espions et autres logiciels malveillants. Microsoft Antimalware fournit des alertes configurables vous avertissant lorsque connu tooinstall de tentatives de logiciels malveillants ou indésirables lui-même ou s’exécuter sur vos systèmes Azure. Microsoft Antimalware peut également être déployé à l’aide d’Azure Security Center.

### <a name="hardware-security-module"></a>Module de sécurité matériel
Chiffrement et authentification n’améliorent pas de sécurité, sauf si les clés hello eux-mêmes sont protégées. Vous pouvez simplifier la gestion de hello et la sécurité de vos clés secrètes critiques et les clés en les stockant dans [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). Le coffre de clés fournit hello option toostore vos clés dans les normes de matériel sécurité certifiés tooFIPS de modules (HSM) 140-2 niveau 2. Vos clés de chiffrement SQL Server pour la sauvegarde ou le [chiffrement transparent des données](https://msdn.microsoft.com/library/bb934049.aspx) peuvent toutes être stockées dans Key Vault avec les clés ou secrets de vos applications. Autorisations et accéder aux éléments de toothese protégé sont gérées via [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

### <a name="virtual-machine-backup"></a>Sauvegarde de machine virtuelle
[Sauvegarde Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) est une solution qui protège les données de vos applications, sans investissement en capital et avec des frais de fonctionnement minimaux. Erreurs d’application peuvent endommager vos données et les erreurs humaines peuvent introduire des bogues dans vos applications qui peuvent entraîner des problèmes de toosecurity. Avec Sauvegarde Azure, vos machines virtuelles exécutant Windows et Linux sont protégées.

### <a name="azure-site-recovery"></a>Azure Site Recovery
Une partie importante de votre organisation [entreprise la continuité des activités/récupération d’urgence (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) stratégie est de déterminer comment les charges de travail d’entreprise tookeep et applications des et en cours d’exécution lors de la planification et les arrêts se produisent. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) aide à coordonner la réplication, le basculement et la récupération des charges de travail et des applications afin qu’elles soient disponibles à partir d’un site secondaire si votre site principal tombe en panne.

### <a name="sql-vm-tde"></a>SQL VM TDE
Le chiffrement [TDE (Transparent data encryption)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault) et le chiffrement au niveau des colonnes (CLE) sont des fonctionnalités de chiffrement de serveur SQL. Cette forme de chiffrement nécessite store et les clients toomanage hello des clés de chiffrement utilisé pour le chiffrement.

Hello service d’Azure Key Vault (AKV) est conçue tooimprove hello sécurité et gestion de ces clés dans un emplacement sécurisé et hautement disponible. Hello connecteur SQL Server permet à SQL Server toouse ces clés à partir d’Azure Key Vault.

Si vous exécutez SQL Server avec les ordinateurs locaux, voici les étapes que vous pouvez suivre tooaccess coffre de clés Azure à partir de votre ordinateur local, SQL Server. Mais pour SQL Server dans des machines virtuelles Azure, vous pouvez gagner du temps en utilisant la fonctionnalité d’Azure Key Vault Integration hello. Avec quelques tooenable d’applets de commande Azure PowerShell cette fonctionnalité, vous pouvez automatiser hello configuration nécessaire pour un tooaccess SQL VM votre coffre de clés.

### <a name="vm-disk-encryption"></a>Chiffrement de disque de machine virtuelle
[Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) est une nouvelle fonctionnalité qui vous permet de chiffrer vos disques de machine virtuelle IaaS Windows et Linux. Il s’applique hello industry standard BitLocker fonctionnalité de Windows et de la fonctionnalité d’exploration de données-Crypt hello du chiffrement de volume tooprovide Linux pour hello du système d’exploitation et des disques de données hello. solution de Hello est intégrée à Azure Key Vault toohelp contrôler et de gérer les clés de chiffrement de disque hello et les secrets dans votre abonnement de coffre de clés. solution de Hello garantit également que toutes les données sur les disques de machine virtuelle hello sont chiffrées au repos dans votre stockage Azure.

### <a name="virtual-networking"></a>Réseau virtuel
Les machines virtuelles nécessitent une connectivité réseau. toosupport cette exigence, Azure nécessite toobe d’ordinateurs virtuels connecté tooan réseau virtuel Azure. Un réseau virtuel Azure est une construction logique reposant sur l’infrastructure du réseau Azure physique hello. Chaque [réseau virtuel logique Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) est isolé des autres réseaux virtuels Azure. Cette isolation permet de s’assurer que le trafic réseau dans vos déploiements n’est pas accessible tooother les clients de Microsoft Azure.

### <a name="patch-updates"></a>Mises à jour correctives
Les mises à jour fournissent la base de hello pour rechercher et résoudre les problèmes potentiels et simplifier les processus de gestion des mises à jour logicielles hello, à la fois en réduisant le nombre de hello de mises à jour logicielles que vous devez déployer dans votre entreprise et en augmentant votre toomonitor de capacité conformité.

### <a name="security-policy-management-and-reporting"></a>Gestion des stratégies de sécurité et création de rapports
[Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) vous aide à empêcher, détecter et répondre toothreats et fournit l’augmentation de la visibilité et contrôler, sécurité hello de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

### <a name="azure-security-center"></a>Azure Security Center
Centre de sécurité vous permet d’empêcher, détecter et répondre toothreats avec une meilleure visibilité et un contrôle accru de la sécurité hello de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

## <a name="identify-and-access-management"></a>Gestion des identités et accès

La sécurisation des systèmes, applications et données commencent par les contrôles d’accès basés sur l’identité. Hello identité et accès aux fonctionnalités de gestion qui sont intégrées dans les produits et services Microsoft business aider à protéger vos informations personnelles et d’organisation contre tout accès, tout en les rendant disponibles toolegitimate utilisateurs où et quand ils en ont besoin.

### <a name="secure-identity"></a>Identité sécurisée
Microsoft utilise plusieurs technologies et pratiques de sécurité sur ses produits et services toomanage identités et des accès.
-   [L’authentification multifacteur](https://azure.microsoft.com/services/multi-factor-authentication/) requiert les utilisateurs toouse plusieurs méthodes pour l’accès, localement et dans le cloud de hello. Elle fournit une authentification forte avec un éventail d’options de vérification conviviales tout en proposant aux utilisateurs un processus de connexion simple.

-   [Microsoft Authenticator](https://aka.ms/authenticator) fournit une expérience Multi-Factor Authentication conviviale, qui fonctionne avec les comptes Microsoft Azure Active Directory et Microsoft et qui prend en charge les appareils wearable et les approbations par empreinte digitale.

-   [Application de stratégie de mot de passe](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/) augmente hello sécurité des mots de passe traditionnels en imposant des exigences de longueur et de complexité forcés une rotation périodique, et les tentatives de verrouillage de compte après l’échec d’authentification.

-   [L’authentification basée sur les jetons](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) permet l’authentification via Active Directory Federation Services (AD FS) ou des systèmes de jetons sécurisés tiers.

-   [Contrôle d’accès basé sur un rôle (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/) toogrant accès en fonction de l’utilisateur hello permet de rôle, rendant toogive facilement les utilisateurs que hello quantité d’accès dont ils ont besoin tooperform leurs tâches. Vous pouvez personnaliser le contrôle RBAC en fonction du modèle d’entreprise et de la tolérance au risque de votre organisation.

-   [Gestion d’identité (identité hybride) intégrée](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/) vous permet de contrôler toomaintain accès des utilisateurs entre les plateformes de cloud et les centres de données internes, la création d’une identité d’utilisateur unique pour l’authentification et d’autorisation tooall ressources.

### <a name="secure-apps-and-data"></a>Sécuriser les applications et données
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/), une identité et accès cloud solution de gestion complète, permet de sécuriser l’accès toodata dans les applications sur site et dans le cloud de hello et simplifie la gestion de hello des groupes et utilisateurs. Il combine des services d’annuaire essentiels, Avancé de gouvernance des identités, la sécurité et gestion des accès aux applications et facilite la tâche aux développeurs toobuild basée sur la stratégie de gestion des identités dans leurs applications. tooenhance votre Azure Active Directory, vous pouvez ajouter des fonctions payées à l’aide des éditions d’Azure Active Directory de base, Premium P1 et P2 de Premium hello.

| Fonctionnalités gratuites/courantes     | Fonctionnalités de base    |Fonctionnalités de Premium P1 |Fonctionnalités de Premium P2 | Azure Active Directory Join - Fonctionnalités propres à Windows 10|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [Objets d’annuaire](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects), [utilisateur/groupe d’administration (ajout/mise à jour/suppression) / utilisateur en fonction de configuration, l’inscription de périphérique](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration), [Single Sign-On (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso), [libre-service Modification de mot de passe pour les utilisateurs du cloud](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users), [Connect (moteur de synchronisation qui s’étend sur site répertoires tooAzure Active Directory)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory), [sécurité / rapports d’utilisation](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [Approvisionnement/gestion des accès par groupe](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning), [Réinitialisation du mot de passe en libre-service pour les utilisateurs du cloud](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users), [Image de l’entreprise (personnalisation des pages de connexion/volet d’accès)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization), [Proxy d’application](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy), [SLA de 99,9 %](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999) |  [Gestion d’applications et de groupes libre-service/ajout d’applications libre-service/groupes dynamiques](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group), [Réinitialisation, modification et déverrouillage de mot de passe libre-service avec écriture différée locale](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back), [Multi-Factor Authentication (dans le cloud et localement (serveur MFA))](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server), [CAL MIM + serveur MIM](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server), [Cloud App Discovery](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery), [Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health), [Substitution automatique des mots de passe pour les comptes de groupe](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts)|     [Identity Protection](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection), [Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure)|    [Joindre un tooAzure appareil AD, l’authentification unique de bureau, Microsoft Passport pour Azure AD, récupération Bitlocker de l’administrateur](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery), [MDM-inscription automatique, récupération libre-service Bitlocker, les appareils tooWindows 10 autres administrateurs local via Azure Jointure d’Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [Cloud App Discovery](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis) est une fonctionnalité premium d’Azure Active Directory qui vous permet de tooidentify les applications cloud qui sont utilisées par les employés hello dans votre organisation.

- [Azure Active Directory Identity Protection](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/) est un service de sécurité qui utilise Azure Active Directory d’anomalie détection fonctionnalités tooprovide une vue consolidée événements à risque et des vulnérabilités potentielles qui pourraient affecter votre identités de l’organisation.

- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds/) vous permet de toojoin machines virtuelles Azure tooa domaine sans hello devez toodeploy les contrôleurs de domaine. Les utilisateurs se connecter à l’aide de leurs informations d’identification Active Directory d’entreprise toothese machines virtuelles et peuvent accéder en toute transparence aux ressources.

- [Azure B2C Active Directory](https://azure.microsoft.com/services/active-directory-b2c/) est un service de gestion des identités global, hautement disponible pour les applications pour les consommateurs qui peuvent mettre à l’échelle toohundreds de millions d’identités et s’intègrent à plusieurs mobiles et web plateformes. Vos clients peuvent se connecter tooall vos applications par le biais des expériences personnalisables qui utilisent des comptes de médias sociaux existant, ou vous pouvez créer de nouvelles informations d’identification autonome.

- [Azure Collaboration B2B d’Active Directory](https://aka.ms/aad-b2b-collaboration) est une solution d’intégration partenaire sécurisé qui prend en charge de vos relations intersociétés en activant partenaires tooaccess vos applications d’entreprise et les données sélective à l’aide de leurs autogéré identités.

- [Azure Active Directory Join](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/) vous permet de tooextend cloud fonctionnalités tooWindows 10 des appareils pour la gestion centralisée. Il rend possible pour les utilisateurs tooconnect toohello d’entreprise ou organisation cloud via Azure Active Directory et simplifie l’accès tooapps et des ressources.

- Le [proxy d’application Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) offre une authentification unique (SSO) et un accès à distance sécurisé pour les applications web hébergées en local.

## <a name="next-steps"></a>Étapes suivantes
- [Prise en main de la sécurité de Microsoft Azure](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Services Azure et les fonctionnalités que vous pouvez utiliser toohelp sécurisent vos services et les données dans Azure

- [Centre de sécurité Azure](https://azure.microsoft.com/services/security-center/)

Empêcher, détecter et répondre toothreats avec une meilleure visibilité et un contrôle sur la sécurité de hello de vos ressources Azure

- [Surveillance de l’intégrité de la sécurité dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

Hello capacités d’analyse dans le centre de sécurité Azure toomonitor respect des stratégies.
