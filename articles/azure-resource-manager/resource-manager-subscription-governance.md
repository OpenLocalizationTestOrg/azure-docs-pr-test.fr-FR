---
title: "pratiques aaaBest pour les entreprises déplacement tooAzure | Documents Microsoft"
description: "Décrit une structure que les entreprises peuvent utiliser tooensure un environnement sécurisé et facile à gérer."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Structure d’entreprise Azure : gouvernance normative de l’abonnement
Les entreprises adoptent plus cloud public de hello pour sa souplesse et une flexibilité. Ils utilisent toogenerate chiffre d’affaires atouts du cloud hello ou optimiser les ressources pour les entreprises hello. Microsoft Azure fournit une multitude de services d’entreprises peuvent assembler comme blocs de construction tooaddress une large gamme d’applications et de charges de travail. 

Cependant, si vous savez où toobegin est souvent difficile. Une fois les toouse Azure, posez des questions surviennent souvent :

* « Comment respecter nos obligations légales en matière de souveraineté des données dans certains pays ? »
* « Comment vérifier que quelqu'un ne modifie pas par inadvertance un système critique ? »
* « Comment savoir ce que chaque ressource prend en charge afin de les comptabiliser et de les facturer avec exactitude ? »

prospect Hello d’un abonnement vide avec n’est parfois très difficile. Cet espace peut entraver votre tooAzure de déplacement.

Cet article fournit un point de départ pour techniciens tooaddress hello nécessaire pour la gouvernance et équilibre avec hello besoin de souplesse. Il introduit le concept de hello d’une structure de l’entreprise qui aide les organisations à l’implémentation et la gestion de leurs abonnements Azure. 

## <a name="need-for-governance"></a>Besoin de gouvernance
Lorsque vous déplacez tooAzure, vous devez résoudre rubrique hello de gouvernance anticipée tooensure hello utilisation réussie du cloud hello au sein de l’entreprise de hello. Malheureusement, temps de hello et bureaucratiques de création d’un système de gouvernance complète signifie que certains groupes professionnels accédez directement toovendors sans intervention de l’informatique d’entreprise. Cette approche peut laisser toovulnerabilities ouvrir de hello entreprise si les ressources hello ne sont pas correctement gérés. caractéristiques de Hello de cloud public de hello - souplesse, la flexibilité et la tarification basée sur la consommation - sont importants groupes toobusiness tooquickly répondre aux demandes de hello de clients (internes et externes). Mais, l’informatique d’entreprise doit tooensure que les données et les systèmes sont effectivement protégés.

Dans la réalité, la structure sert toocreate utilisé hello de structure de hello. une vue de structure Hello repères de plan général de hello et fournit des points d’ancrage pour permanent toobe systèmes monté. Une structure de l’entreprise est hello même : un ensemble de contrôles flexibles et de fonctions d’Azure qui fournissent l’environnement toohello de structure et les ancres pour les services basés sur le cloud public de hello. Il fournit des générateurs de hello (informatique et de groupes) un toocreate foundation et attacher les nouveaux services.

une vue de structure Hello est basé sur les pratiques que nous avons rassemblées à partir de plusieurs contrats avec des clients de différentes tailles. Plage de ces clients à partir de petites organisations développement de solutions dans hello cloud tooFortune 500 entreprises et aux éditeurs de logiciels indépendants qui migration et développent des solutions de cloud de hello. Bonjour scaffold d’entreprise est toosupport flexible de toobe « dédiée » à la fois des charges de travail informatiques traditionnelles et les charges de travail agiles ; par exemple, les développeurs qui créent des applications de software-as-a-service (SaaS) basée sur des fonctionnalités Azure.

une vue de structure Hello entreprise est prévue toobe hello de chaque nouvel abonnement dans Azure. Il permet les administrateurs tooensure les charges de travail hello satisfait minimale des exigences de gouvernance d’une organisation sans empêcher des groupes professionnels et les développeurs à partir de leurs objectifs rapidement.

> [!IMPORTANT]
> La gouvernance est Réussite toohello essentiel d’Azure. Cette cible de l’article hello implémentation technique d’une structure de l’entreprise mais ne concerne que les processus plus vaste hello et relations entre les composants de hello. Gouvernance de la stratégie circulent à partir de la partie supérieure de hello vers le bas et est déterminée par le hello entreprise souhaite tooachieve. Naturellement, la création d’un modèle de gouvernance hello pour Azure comprend des représentants de l’informatique, mais plus important encore, il doit avoir forte représentation sous forme de leaders de groupe et gestion des risques et de sécurité. En fin de hello, une structure de l’entreprise est sur l’atténuation entreprise risque toofacilitate mission et ses objectifs d’une organisation.
> 
> 

Hello suivant l’image décrit les composants de hello de vue de structure hello. foundation de Hello s’appuie sur un plan solid des départements, des comptes et des abonnements. les piliers Hello se composent de stratégies du Gestionnaire de ressources et les normes d’affectation de noms forts. autres Hello une vue de structure hello core provient des fonctions d’Azure et des fonctionnalités qui permettent à un environnement sécurisé et facile à gérer.

![composants d’une structure](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure a évolué rapidement depuis son lancement en 2008. Cette croissance requis équipes d’ingénierie de Microsoft toorethink leur approche pour gérer et déployer des services. modèle de gestionnaire de ressources Azure Hello a été introduit dans 2014 et remplace le modèle de déploiement classique hello. Le Gestionnaire de ressources permet aux organisations toomore facilement déployer, d’organiser et contrôler les ressources Azure. Resource Manager comprend la parallélisation lors de la création de ressources pour un déploiement plus rapide de solutions complexes et interdépendantes. Il inclut également le contrôle d’accès granulaire et des ressources de tootag hello possibilité avec des métadonnées. Microsoft recommande de créer toutes les ressources via le modèle de gestionnaire de ressources hello. une vue de structure Hello entreprise est explicitement conçu pour le modèle de gestionnaire de ressources hello.
> 
> 

## <a name="define-your-hierarchy"></a>Définition de votre hiérarchie
Hello de vue de structure hello repose inscription d’entreprise de Azure hello (et hello Enterprise Portal). inscription d’entreprise de Hello définit la forme de hello et utiliser des services Azure au sein d’une entreprise et est la structure de gouvernance hello core. Dans le contrat d’entreprise hello, les clients ne peuvent toofurther subdiviser environnement hello dans les services, les comptes et enfin, les abonnements. Un abonnement Azure est l’unité de base hello où toutes les ressources sont contenues. Il définit également plusieurs limites au sein d’Azure, par exemple le nombre de cœurs, de ressources, etc.

![hiérarchie](./media/resource-manager-subscription-governance/agreement.png)

Chaque entreprise est différente et hiérarchie hello dans l’image précédente de hello permet une grande flexibilité dans l’organisation au sein de la société de hello Azure. Avant d’implémenter les conseils hello contenues dans ce document, vous devez votre hiérarchie de modèle et comprendre l’impact de hello sur la facturation, de l’accès aux ressources et de complexité.

Hello trois modèles courants pour les inscriptions Azure sont :

* Hello **fonctionnel** modèle
  
    ![functional](./media/resource-manager-subscription-governance/functional.png)
* Hello **division** modèle 
  
    ![business](./media/resource-manager-subscription-governance/business.png)
* Hello **géographique** modèle
  
    ![geographic](./media/resource-manager-subscription-governance/geographic.png)

Vous appliquez une vue de structure hello en hello abonnement tooextend niveau hello exigences de gouvernance de l’entreprise de hello dans un abonnement de hello.

## <a name="naming-standards"></a>Normes d’attribution de noms
Hello convient en premier lieu de la vue de structure hello est conventions d’appellation standard. Les normes d’affectation de noms bien conçues activer tooidentify des ressources dans le portail hello, sur une facture et dans les scripts. Vous disposez déjà probablement de conventions d’attribution de noms pour l’infrastructure locale. Lorsque vous ajoutez un environnement de tooyour Azure, vous devez étendre ceux tooyour des normes d’affectation de noms des ressources Azure. Norme faciliter une gestion plus efficace de l’environnement hello à tous les niveaux.

> [!TIP]
> Pour les conventions de dénomination :
> * Passez en revue et adopter lorsque cela est possible hello [modèles et des pratiques recommandées](../guidance/guidance-naming-conventions.md). Ce guide vous permet de déterminer une norme d’attribution de noms explicite.
> * Utilisez la casse mixte (camelCasing) pour les noms des ressources (par exemple, myResourceGroup et vnetNetworkName). Remarque : Il existe certaines ressources, telles que les comptes de stockage, où la seule option de hello est toouse minuscules (et aucun autre caractère spécial).
> * Envisagez d’utiliser Azure Resource Manager tooenforce de stratégies (décrites dans la section suivante de hello) normes d’affectation de noms.
> 
> Hello précédents conseils vous aider à implémenter une convention d’affectation de noms cohérente.

## <a name="policies-and-auditing"></a>Stratégies et audit
deuxième pilier de Hello de vue de structure hello implique la création de [Azure Resource Manager stratégies](resource-manager-policy.md) et [l’audit de journal d’activité hello](resource-group-audit.md). Stratégies du Gestionnaire de ressources vous fournissent des risques de toomanage possibilité hello dans Azure. Vous pouvez définir des stratégies qui garantissent la souveraineté des données en limitant, en appliquant ou en auditant certaines actions. 

* La stratégie est un système **d’autorisation** par défaut. Pour contrôler les actions par définition et assignation tooresources stratégies refuser ou auditer les actions sur les ressources.
* Les stratégies sont décrites par des définitions de stratégie dans un langage de définition de stratégie (conditions if-then).
* Vous créez des stratégies avec des fichiers au format JSON (Javascript Object Notation). Après avoir défini une stratégie, vous lui étendue particulière de tooa : abonnement, groupe de ressources ou une ressource.

Les stratégies ont plusieurs actions qui permettent un scénario de tooyour approche affinée. actions de Hello sont :

* **Refuser**: demande de ressource de blocs hello
* **Audit**: permet de demande de hello mais ajoute un journal d’activité toohello ligne (qui peut être utilisé tooprovide alertes ou les runbooks tootrigger)
* **Ajouter**: ajoute des informations toohello ressource spécifiée. Par exemple, s’il n’existe pas de balise « CostCenter » sur une ressource, ajoutez cette balise avec une valeur par défaut.

### <a name="common-uses-of-resource-manager-policies"></a>Utilisations courantes de stratégies Resource Manager
Stratégies de gestion de ressources Azure sont un outil puissant hello boîte à outils Azure. Ils permettent de tooavoid les coûts imprévus, tooidentify un centre de coût pour les ressources par un marquage et tooensure cette conformité conditions sont remplies. Lorsque les stratégies sont combinées avec les fonctionnalités d’audit intégrées hello, vous pouvez mode solutions complexes et flexibles. Les stratégies permettent aux entreprises tooprovide des contrôles pour les charges de travail « Informatiques traditionnelles » et « Agile » les charges de travail ; par exemple, développement d’applications de client. les modèles les plus courants Hello que nous voyons pour les stratégies sont :

* **Géo-conformité/données souveraineté** -Azure présente les régions Bonjour. Les entreprises souhaitent souvent toocontrol où les ressources sont créés (si souveraineté de données tooensure ou simplement les ressources tooensure sont créés toohello fermer les clients des ressources de hello).
* **Gestion des coûts** : un abonnement Azure peut contenir des ressources de nombreux types et à différentes échelles. Les sociétés souhaitent souvent tooensure cette norme abonnements Évitez d’utiliser des ressources inutilement volumineux, ce qui peuvent coûter des centaines de dollars par mois ou plus.
* **Par défaut de gouvernance via des balises requis** -nécessitant des balises est l’une des fonctionnalités hautement souhaitée et les plus courantes de hello. À l’aide de stratégies du Gestionnaire de ressources Azure entreprises sont en mesure de tooensure qu’une ressource est correctement légendée. Hello balises plus courantes sont : type de service, propriétaire de la ressource et l’environnement (par exemple - production, test et développement)

**Exemples**

Abonnement de type « informatique traditionnelle » pour les applications métier

* Application de balises de type service et propriétaire à toutes les ressources
* Restreindre la création de ressources toohello la région Amérique du Nord
* Restreindre hello capacité toocreate machines virtuelles de série G et les Clusters HDInsight

Environnement « Agile » pour une division de création d’applications cloud

* configuration requise de toomeet données souveraineté, autoriser la création de hello des ressources uniquement dans une région spécifique.
* Appliquez la balise d’environnement à toutes les ressources. Si une ressource est créée sans la balise, ajouter hello **environnement : inconnu** toohello ressource de balise.
* Auditez lorsque les ressources sont créées en dehors de l’Amérique du Nord, mais n’empêchez pas
* l’audit lorsque des ressources onéreuses sont créées.

> [!TIP]
> utilisation la plus courante de stratégies du Gestionnaire de ressources entre plusieurs organisations Hello est toocontrol *où* ressources peuvent être créés et *que* types de ressources peuvent être créés. De plus de contrôles tooproviding *où* et *que*, nombreuses entreprises utilisent des stratégies tooensure ressources ont toobill de métadonnées appropriées hello pour la consommation. Nous vous recommandons d’appliquer des stratégies au niveau d’abonnement hello pour :
> 
> * la conformité géographique/la souveraineté des données ;
> * la gestion des coûts ;
> * les balises nécessaires (déterminées selon les besoins métier, notamment BillTo et propriétaire de l’application).
> 
> Vous pouvez appliquer des stratégies supplémentaires à des niveaux inférieurs de l’étendue.
> 
> 

### <a name="audit---what-happened"></a>Audit - que s’est-il passé ?
tooview le fonctionne de votre environnement, vous devez tooaudit l’activité des utilisateurs. La plupart des types de ressources dans Azure créent des journaux de diagnostic que vous pouvez analyser par le biais d’un outil de journal ou dans Azure Operations Management Suite. Vous pouvez collecter des journaux d’activité entre plusieurs tooprovide abonnements un département ou une vue de l’entreprise. Les enregistrements d’audit sont un outil de diagnostic important et un événement de tootrigger mécanisme essentiel Bonjour environnement Azure.

Journaux d’activité à partir des déploiements de gestionnaire de ressources permettent de toodetermine hello **operations** qui a eu lieu et qui a effectué les. Les journaux d’activité peuvent être collectés et agrégés à l’aide d’outils tels que Log Analytics.

## <a name="resource-tags"></a>Balises de ressource
Les utilisateurs de votre organisation ajoutent l’abonnement aux ressources de toohello, il devient tooassociate plus en plus importante des ressources avec le service approprié de hello, client et l’environnement. Vous pouvez attacher tooresources de métadonnées via [balises](resource-group-using-tags.md). Vous utilisez des balises tooprovide plus d’informations sur la ressource de hello ou un propriétaire de hello. Balises vous permettent de toonot uniquement d’agrégation et les ressources du groupe de différentes manières, mais utilisent ces données à des fins hello de rétrofacturation. Vous pouvez baliser des ressources avec des paires clé-valeur de too15. 

Les balises de ressources sont flexibles et doivent être attachés toomost ressources. Exemples de balises de ressources courantes :

* BillTo
* Service (ou unité commerciale)
* Environnement (production, déploiement intermédiaire, développement)
* Couche (couche Web, couche Application)
* Propriétaire de l’application
* ProjectName

![tags](./media/resource-manager-subscription-governance/resource-group-tagging.png)

Pour plus d’exemples de balises, consultez la rubrique [Conventions d’affectation de noms recommandées pour les ressources Azure](../guidance/guidance-naming-conventions.md).

> [!TIP]
> Envisagez une stratégie qui impose de balisage pour les éléments suivants :
> 
> * Groupes de ressources
> * Storage
> * Machines virtuelles
> * Environnements de service d’applications/serveurs web
> 
> Cette stratégie marquage identifie entre vos abonnements, les métadonnées sont nécessaires pour hello Professionnel, financier, sécurité, gestion des risques et la gestion globale de l’environnement de hello. 

## <a name="resource-group"></a>Groupe de ressources
Le Gestionnaire de ressources vous permet de tooput ressources en groupes explicites pour l’affinité de facturation ou naturel de gestion. Comme mentionné précédemment, Azure dispose de deux modèles de déploiement. Bonjour classiques classique, unité de gestion de base hello a été abonnement de hello. Il était difficile toobreak vers le bas des ressources au sein d’un abonnement ayant entraîné la création d’un grand nombre d’abonnements toohello. Avec le modèle de gestionnaire de ressources hello, nous avons vu introduction hello des groupes de ressources. Les groupes de ressources sont des conteneurs de ressources qui ont un cycle de vie commun ou partagent un attribut tel que « tous les serveurs SQL » ou « Application A ».

Groupes de ressources ne peut pas être contenues dans l’autre et de ressources peuvent appartenir uniquement le groupe de ressources tooone. Vous pouvez appliquer certaines actions à toutes les ressources dans un groupe de ressources. Par exemple, la suppression d’un groupe de ressources supprime toutes les ressources dans le groupe de ressources hello. En règle générale, vous placez un ensemble de l’application ou le système associé dans hello même groupe de ressources. Par exemple, une application à trois niveaux appelée Application Web de Contoso contiendrait les serveur web de hello, serveur d’applications et SQL server dans hello même groupe de ressources.

> [!TIP]
> Vous permettent d’organiser vos groupes de ressources peut-être différer des charges de travail « L’informatique traditionnel » trop charges de travail « Agile informatiques » :
> 
> * « Traditionnel informatique » les charges de travail sont généralement regroupés par des éléments dans hello même cycle de vie, par exemple, une application. Le regroupement par application permet de gestion des applications individuelles.
> * « Agile informatique « charges de travail ont tendance à toofocus sur les applications de cloud des clients externes. groupes de ressources Hello doivent refléter les couches hello de déploiement (par exemple, la couche Web, de niveau de l’application) et de gestion.
> 
> Comprendre votre charge de travail vous aide à développer une stratégie de groupe de ressources.

## <a name="role-based-access-control"></a>Contrôle d’accès en fonction du rôle
Vous sont demandez probablement « qui doit avoir accès tooresources ? » et « comment contrôler cet accès ? ». Autoriser ou interdire l’accès toohello portail Azure et contrôle tooresources d’accès dans le portail de hello sont cruciales. 

Lorsque Azure a été initialement publiée, l’accès aux contrôles tooa abonnement ont été base : administrateur ou Coadministrateur. Abonnement tooa d’accès dans hello classique modèle impliqué accès tooall hello ressources du portail de hello. Cette absence d’un contrôle affiné led prolifération toohello des abonnements tooprovide un niveau de contrôle d’accès raisonnable pour une inscription à Azure.

Cette prolifération d’abonnements n’est plus nécessaire. Avec le contrôle d’accès basé sur un rôle, vous pouvez affecter des utilisateurs rôles toostandard (par exemple, commun « lecture » et les types de « writer » des rôles). Vous pouvez également définir des rôles personnalisés.

> [!TIP]
> contrôle d’accès en fonction du rôle tooimplement :
> * Connecter votre identité d’entreprise du store (généralement Active Directory) tooAzure Active Directory à l’aide de hello outil AD Connect.
> * Contrôle hello Admin/Coadministrateur d’un abonnement à l’aide d’une identité gérée. **Ne pas** affecter Admin/Co-admin tooa nouvel abonnement propriétaire. Au lieu de cela, utilisez RBAC rôles tooprovide **propriétaire** droits tooa groupe ou une personne.
> * Ajoutez le groupe de tooa d’utilisateurs d’Azure (par exemple, Application X propriétaires) dans Active Directory. Utiliser hello synchronisés tooprovide groupe membres hello droits appropriés toomanage hello ressource groupe contenant l’application hello.
> * Suivez le principe hello d’octroi hello **moindre privilège** toodo requis hello attendu de travail. Par exemple :
>   * Groupe de déploiement : Un groupe qui est en mesure de toodeploy que les ressources.
>   * Gestion d’ordinateurs virtuels : Un groupe de VMs en mesure de toorestart (pour les opérations)
> 
> Ces conseils vous aident à gérer l’accès utilisateur au sein de votre abonnement.

## <a name="azure-resource-locks"></a>Verrous de ressource Azure
Quand votre organisation ajoute un abonnement de toohello core services, il devient tooensure plus en plus important que ces services sont disponibles tooavoid interruption de service. [Verrous de ressources](resource-group-lock-resources.md) vous activer les opérations de toorestrict sur les ressources de valeur élevée où suppression ou leur modification aurait un impact significatif sur vos applications ou d’une infrastructure cloud. Vous pouvez appliquer des verrous tooa abonnement, groupe de ressources ou ressource. En règle générale, vous appliquez des ressources de toofoundational de verrous, telles que les réseaux virtuels, les passerelles et les comptes de stockage. 

Les verrous de ressource prennent actuellement en charge deux valeurs : CanNotDelete et ReadOnly. CanNotDelete signifie que les utilisateurs (avec les droits appropriés hello) peuvent toujours lire ou modifier une ressource, mais ne peut le supprimer. ReadOnly signifie que les utilisateurs autorisés ne peuvent pas supprimer ou modifier une ressource.

toocreate ou supprimer les verrous de gestion, vous devez avoir accès trop`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` actions.
Rôles intégrés hello uniquement propriétaire et administrateur de l’accès utilisateur sont accordées à ces actions.

> [!TIP]
> Les options de réseau principal doivent être protégées par des verrous. La suppression accidentelle d’une passerelle VPN de site à site serait désastreux tooan abonnement Azure. Azure ne vous autorise pas toodelete un réseau virtuel est en cours d’utilisation, mais l’application plus de restrictions est utile pour des raisons de. 
> 
> * Réseau virtuel : CanNotDelete
> * Groupe de sécurité réseau : CanNotDelete
> * Stratégies : CanNotDelete
> 
> Les stratégies sont également gestion toohello essentiel des contrôles appropriés. Nous vous conseillons d’appliquer un **CanNotDelete** verrouiller toopolices qui sont en cours d’utilisation.

## <a name="core-networking-resources"></a>Ressources de réseau principal
Accès tooresources peuvent être externes ou internes (dans le réseau de l’entreprise hello) (via hello internet). Il est facile pour les utilisateurs dans votre organisation tooinadvertently put ressources place incorrect de hello et potentiellement ouvrir toomalicious accès. Comme avec les appareils locaux, les entreprises doivent ajouter tooensure contrôles appropriés que les utilisateurs Azure décisions hello appropriées. Pour la gouvernance de l’abonnement, nous identifions des ressources principales qui fournissent le contrôle d’accès de base. ressources principales du Hello sont constitués de :

* Les **réseaux virtuels** sont des objets Conteneur de sous-réseaux. S’il est absolument nécessaire, il est souvent utilisé lors de la connexion des applications toointernal des ressources d’entreprise.
* **Groupes de sécurité réseau** sont similaires tooa pare-feu et de fournir de la façon dont une ressource peut « communiquer » avec des règles de réseau hello. Ils fournissent un contrôle granulaire sur la façon / si un sous-réseau (ou un ordinateur virtuel) peut se connecter toohello Internet ou autres sous-réseaux dans hello même réseau virtuel.

![réseau principal](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> Pour la mise en réseau :
> * Créer des réseaux virtuels dédiés tooexternal côté les charges de travail et les charges de travail interne. Cette approche réduit les risques de hello de placement des ordinateurs virtuels qui sont destinés à des charges de travail internes dans un espace en vis-à-vis externe par inadvertance.
> * Configurer l’accès de toolimit de groupes de sécurité réseau. Au minimum, bloquer toohello d’accès internet à partir de réseaux virtuels internes et réseau d’entreprise toohello accès bloc à partir de réseaux virtuels externes.
> 
> Ces conseils vous aident à mettre en œuvre des ressources de mise en réseau sécurisées.

### <a name="automation"></a>Automatisation
La gestion individuelle des ressources prend du temps et sujette aux erreurs dans certaines opérations. Azure fournit diverses fonctionnalités d’automatisation, notamment Azure Automation, Logic Apps et Azure Functions. [Azure Automation](../automation/automation-intro.md) permet aux administrateurs toocreate et définir des tâches courantes de toohandle procédures opérationnelles dans la gestion des ressources. Vous créez des runbooks à l’aide d’un éditeur de code PowerShell ou d’un éditeur graphique. Vous pouvez générer des flux de travail complexes à plusieurs étapes. Azure Automation est souvent utilisé toohandle des tâches courantes telles que les ressources non utilisées d’arrêt ou de la création de ressources dans un déclencheur spécifique de réponse tooa sans avoir besoin d’une intervention humaine.

> [!TIP]
> Pour l’automatisation :
> * Créer un compte Azure Automation et passez en revue les hello runbook disponibles (graphique et commande de ligne) disponibles dans hello [galerie de runbooks](../automation/automation-runbook-gallery.md).
> * Importer et personnaliser des runbooks clés pour votre usage personnel.
> 
> Un scénario courant consiste à tooStart/arrêt hello capacité virtuels selon une planification. Il n’y exemple procédures opérationnelles qui sont disponibles dans la galerie de hello gérer ce scénario et à apprendre comment tooexpand il.
> 
> 

## <a name="azure-security-center"></a>Azure Security Center
Peut-être un des plus grande adoption de toocloud des blocages hello a été préoccupations de hello sur la sécurité. Gestionnaires des risques informatiques et les services de sécurité doivent tooensure que les ressources dans Azure sont sécurisées. 

Hello [Azure Security Center](../security-center/security-center-intro.md) fournit une vue centralisée de l’état de la sécurité des ressources dans les abonnements hello hello et fournit des recommandations qui permettent d’éviter les compromis de ressources. Elle peut activer des stratégies plus précis (par exemple, application stratégies toospecific groupes de ressources qui permettent de hello entreprise tootailor risque toohello posture qu'ils résolvent). Enfin, le centre de sécurité Azure est une plateforme ouverte qui permet aux partenaires de Microsoft et logiciels fournisseurs toocreate logiciel qui se connecte au centre de sécurité Azure tooenhance de ses fonctionnalités. 

> [!TIP]
> L’Azure Security Center est activé par défaut dans chaque abonnement. Toutefois, vous devez activer la collecte des données à partir d’ordinateurs virtuels tooallow Azure Security Center tooinstall son agent et commencer la collecte des données.
> 
> ![la collection de données](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Maintenant que vous avez appris à propos de la gouvernance de l’abonnement, il est temps toosee ces recommandations dans la pratique. Voir la rubrique [Examples of implementing Azure subscription governance](resource-manager-subscription-examples.md) (Exemples d’implémentation de la gouvernance des abonnements Azure).

