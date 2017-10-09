---
title: "aaaScenarios et des exemples pour la gouvernance de l’abonnement | Documents Microsoft"
description: "Fournit des exemples de façon tooimplement gouvernance de l’abonnement Azure pour les scénarios courants."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Exemples d’implémentation d’une structure d’entreprise Azure
Cette rubrique fournit des exemples de comment une entreprise peut implémenter les recommandations hello pour un [une vue de structure Azure enterprise](resource-manager-subscription-governance.md). Elle utilise une société fictive nommée Contoso tooillustrate meilleures pratiques pour les scénarios courants.

## <a name="background"></a>Arrière-plan
Contoso est une société dans le monde entier qui fournit des solutions de chaîne d’approvisionnement pour les clients de tous les éléments d’un modèle de package tooa « Software as a Service » modèle déployé localement.  Ils développent des logiciels monde hello avec des centres de développement significatifs en Inde, hello États-Unis et Canada.

partie de ISV Hello de société de hello est divisé en plusieurs unités commerciales indépendantes qui gèrent des produits dans une entreprise importantes. Chaque unité commerciale a ses propres développeurs, chefs de produit et architectes.

division de Services de technologie d’entreprise (ETS) Hello offre des capacités d’informatique centralisée et gère plusieurs centres de données où les divisions hébergent leurs applications. En même temps que la gestion des centres de données hello, hello organisation de ETS fournit et gère la collaboration centralisée (par exemple, la messagerie et des sites Web) et les services de téléphonie/réseau. Elle gère également les charges de travail côté client pour les divisions commerciales plus petites qui ne disposent pas de personnel d’exploitation.

Hello suivant personnages est utilisé dans cette rubrique :

* Dave est administrateur de ETS Azure hello.
* Alice est directeur du développement Contoso de centre de profit de chaîne logistique hello.

Contoso doit toobuild line of business application et une application côté client. Il a décidé d’applications de hello toorun sur Azure. Dave lit hello [gouvernance de l’abonnement normative](resource-manager-subscription-governance.md) rubrique, et est maintenant prêt tooimplement recommandations de hello.

## <a name="scenario-1-line-of-business-application"></a>Scénario 1 : application métier
La génération d’un code de source gestion toobe système (BitBucket) utilisée par les développeurs pour Bonjour est contoso.  application Hello utilise l’Infrastructure en tant que Service (IaaS) pour l’hébergement et se compose de serveurs web et un serveur de base de données. Les développeurs accéder aux serveurs dans leurs environnements de développement, mais ils ne doivent accéder aux serveurs toohello dans Azure. Contoso ETS veut tooallow propriétaire de l’application hello et l’application hello équipe toomanage. application Hello est uniquement disponible sur le réseau d’entreprise de Contoso. Dave doit tooset d’abonnement de hello pour cette application. abonnement de Hello héberge également d’autres logiciels liés au développement Bonjour futures.  

### <a name="naming-standards--resource-groups"></a>Normes d’attribution de noms et groupes de ressources
Dave crée un abonnement à des outils de développement toosupport qui sont communes à toutes les divisions hello. Il doit toocreate des noms explicites pour l’abonnement de hello et les groupes de ressources (pour application hello et réseaux de hello). Il crée hello abonnement et ressources des groupes suivants :

| Item | Nom | Description |
| --- | --- | --- |
| Abonnement |Contoso ETS DeveloperTools Production |Prend en charge des outils de développement courants |
| Groupe de ressources |rgBitBucket |Contient le serveur web d’application hello et le serveur de base de données |
| Groupe de ressources |rgCoreNetworks |Contient des réseaux virtuels hello et connexion à la passerelle de site à site |

### <a name="role-based-access-control"></a>Contrôle d’accès en fonction du rôle
Après la création de son abonnement, Dave veut tooensure qui hello équipes appropriés et propriétaires d’applications peuvent accéder à leurs ressources. Dave tient compte du fait que chaque équipe a des exigences différentes. Il utilise des groupes de hello qui ont été synchronisés à partir d’Active Directory (AD) tooAzure Active Directory de Contoso local et fournit le niveau des équipes de toohello accès hello.

Dave attribue hello suivant des rôles pour l’abonnement de hello :

| Rôle | Trop d’assigné| Description |
| --- | --- | --- |
| [Propriétaire](../active-directory/role-based-access-built-in-roles.md#owner) |ID géré à partir de l’AD Contoso |Cet ID est contrôlé avec un accès Just in Time (JIT) par le biais de l’outil de gestion des identités de Contoso et garantit que l’accès propriétaire à l’abonnement est entièrement audité. |
| [Gestionnaire de sécurité](../active-directory/role-based-access-built-in-roles.md#security-manager) |Service de gestion de la sécurité et des risques |Ce rôle permet toolook les utilisateurs à hello Azure Security Center et l’état de hello des ressources de hello. |
| [Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md#network-contributor) |Équipe réseau |Ce rôle permet hello Site tooSite VPN Contoso réseau équipe toomanage et hello des réseaux virtuels. |
| *Rôle personnalisé* |Propriétaire de l’application |Dave crée un rôle qui accorde des ressources de toomodify hello capacité dans le groupe de ressources hello. Pour en savoir plus, consultez la rubrique [Rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](../active-directory/role-based-access-control-custom-roles.md) |

### <a name="policies"></a>Stratégies
Dave a hello suivant les exigences pour la gestion des ressources de l’abonnement de hello :

* Outils de développement hello prenant en charge les développeurs sur Bonjour, il ne souhaite que les utilisateurs tooblock à partir de la création de ressources dans n’importe quelle région. Toutefois, il doit tooknow où les ressources sont créées.
* Il doit surveiller les coûts. Par conséquent, qu’il veut tooprevent propriétaires d’applications de créer des machines virtuelles inutilement coûteux.  
* Car cette application permet aux développeurs de nombreuses unités commerciales, qu’il veut tootag chaque ressource dont le propriétaire est unité et application hello entreprise. À l’aide de ces balises, ETS puissiez facturer les équipes appropriés hello.

Il crée des éléments suivants de hello [stratégies du Gestionnaire de ressources](resource-manager-policy.md):

| Champ | Résultat | Description |
| --- | --- | --- |
| location |audit |Audit de création de ressources hello dans n’importe quelle région hello |
| type |deny |Refuser la création de machines virtuelles de série G |
| tags |deny |Exiger la balise de propriétaire de l’application |
| tags |deny |Exiger la balise du centre de coût |
| tags |append |Ajouter le nom de la balise **division** et la valeur de la balise **ETS** tooall ressources |

### <a name="resource-tags"></a>Balises de ressource
Dave sait qu’il doit toohave des informations spécifiques sur le centre de coût hello bill tooidentify hello pour l’implémentation de BitBucket hello. En outre, Dave souhaite tooknow que tous hello ressources ETS propriétaire.

Il ajoute les éléments suivants de hello [balises](resource-group-using-tags.md) toohello groupes de ressources et de ressources.

| Nom de la balise | Valeur de la balise |
| --- | --- |
| ApplicationOwner |nom Hello de personne hello qui gère cette application. |
| CostCenter |Centre de coût Hello du groupe de hello payer pour hello consommation Azure. |
| BusinessUnit |**ETS** (hello division associée hello abonnement) |

### <a name="core-network"></a>Réseau principal
Hello ETS Contoso informations équipe de gestion des risques et passe en revue de Dave proposées plan toomove hello application tooAzure. Ils veulent tooensure application hello n’est pas exposée toohello internet.  Dave a également les applications de développeur qui seront déplacé tooAzure Bonjour futures. Ces applications nécessitent des interfaces publiques.  toomeet ces exigences, il fournit à la fois des réseaux virtuels internes et externes et un accès de toorestrict de groupe de sécurité réseau.

Il crée hello suivant des ressources :

| Type de ressource | Nom | Description |
| --- | --- | --- |
| Réseau virtuel |vnInternal |Utilisé avec hello BitBucket application et est connecté via le réseau d’entreprise de tooContoso ExpressRoute.  Un sous-réseau (sbBitBucket) fournit l’application hello avec un espace d’adresse IP spécifique. |
| Réseau virtuel |vnExternal |Disponible pour des applications futures qui nécessitent des points de terminaison accessible au pusblic. |
| Groupe de sécurité réseau |nsgBitBucket |Permet de s’assurer que hello surface d’attaque de cette charge de travail est réduite en autorisant les connexions uniquement sur le port 443 pour le sous-réseau de hello où application hello réside (sbBitBucket). |

### <a name="resource-locks"></a>Verrous de ressources
Dave reconnaît que la connectivité hello à partir du réseau virtuel interne toohello du Contoso réseau d’entreprise doit être protégée à partir de n’importe quel script versatiles ou une suppression accidentelle.

Il crée des éléments suivants de hello [verrou de ressource](resource-group-lock-resources.md):

| Type de verrou | Ressource | Description |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |Empêche les utilisateurs à partir des sous-réseaux ou réseaux hello suppression, mais n’empêche pas l’ajout de hello de nouveaux sous-réseaux. |

### <a name="azure-automation"></a>Azure Automation
Dave n’a rien tooautomate pour cette application. Même s’il a créé un compte Azure Automation, il ne l’utilisera pas au cours des étapes initiales.

### <a name="azure-security-center"></a>Azure Security Center
Gestion des services informatiques de Contoso doit tooquickly identifier et gérer les menaces. Ils veulent également toounderstand quels sont les problèmes éventuels.  

toofulfill ces exigences, Dave Active hello [Azure Security Center](../security-center/security-center-intro.md)et fournit le rôle de gestionnaire de sécurité d’accès toohello.

## <a name="scenario-2-customer-facing-app"></a>Scénario 2 : application destinée aux clients
direction d’entreprise Hello dans le centre de profit chaîne hello approvisionnement a identifié engagement de tooincrease différentes possibilités avec les clients de Contoso à l’aide d’une carte de fidélité. Équipe de d’Alice doit créer cette application et décide que Azure augmente leur toomeet possibilité hello les besoins de l’entreprise. Alice fonctionne avec Dave ETS tooconfigure deux abonnements pour le développement et le fonctionnement de cette application.

### <a name="azure-subscriptions"></a>Abonnements Azure
Dave se connecte toohello Azure Enterprise Portal et voit que ce service de chaîne d’approvisionnement hello existe déjà.  Toutefois, que ce projet est le premier projet de développement hello pour l’équipe de chaîne d’approvisionnement hello dans Azure, Dave reconnaît besoin hello pour un nouveau compte pour l’équipe de développement d’Alice.  Il crée hello un compte « R & D » pour l’équipe et assigne tooAlice d’accès. Alice se connecte via hello portail Azure et crée deux abonnements : serveurs de développement hello un toohold et un toohold hello production.  Elle suit les normes d’affectation de noms hello précédemment établie lors de la création de hello suivant des abonnements :

| Utilisation de l’abonnement | Nom |
| --- | --- |
| Développement |SupplyChain ResearchDevelopment LoyaltyCard Development |
| Production |SupplyChain Operations LoyaltyCard Production |

### <a name="policies"></a>Stratégies
Dave Alice discuter application hello et identifier que cette application sert uniquement aux clients dans la région Amérique du Nord hello.  Alice et son équipe de plan de toouse Azure environnement de Service d’Application et application de hello toocreate SQL Azure. Ils peuvent doivent toocreate virtuels pendant le développement.  Alice souhaite tooensure son les développeurs ayant des ressources hello nécessaires tooexplore et examiner les problèmes sans extrayant des ETS.

Pourquoi **abonnement de développement**, ils créent hello suivant de stratégie :

| Champ | Résultat | Description |
| --- | --- | --- |
| location |audit |Création de hello des ressources de hello dans n’importe quelle région de l’audit. |

Elles ne limitent pas de type hello de référence (SKU), qu'un utilisateur peut créer dans le développement, et ils ne nécessitent pas de balises pour les groupes de ressources ou des ressources.

Pourquoi **abonnement de production**, ils créent hello suivant des stratégies :

| Champ | Résultat | Description |
| --- | --- | --- |
| location |deny |Refuser la création de hello toutes les ressources en dehors des centres de données hello des États-Unis. |
| tags |deny |Exiger la balise de propriétaire de l’application |
| tags |deny |Exiger une balise de service. |
| tags |append |Ajouter un groupe de ressources tooeach balise qui indique l’environnement de production. |

Elles ne limitent pas de type hello de référence (SKU), qu'un utilisateur peut créer en production.

### <a name="resource-tags"></a>Balises de ressource
Dave sait qu’il doit toohave des informations spécifiques tooidentify hello correcte des groupes de facturation et de la propriété. Il définit des balises de ressources pour les groupes de ressources et les ressources.

| Nom de la balise | Valeur de la balise |
| --- | --- |
| ApplicationOwner |nom Hello de personne hello qui gère cette application. |
| department |Centre de coût Hello du groupe de hello payer pour hello consommation Azure. |
| EnvironmentType |**Production** (même si l’abonnement hello comprend **Production** dans le nom de hello, y compris cette balise permet de faciliter l’identification en examinant les ressources dans le portail de hello ou sur facture de hello.) |

### <a name="core-networks"></a>Réseaux principaux
Hello ETS Contoso informations équipe de gestion des risques et passe en revue de Dave proposées plan toomove hello application tooAzure. Ils veulent tooensure qui hello d’application de la carte de fidélité est correctement isolée et protégée dans un réseau DMZ.  toofulfill cette exigence, Alice et Dave créer un réseau virtuel externe et un Bonjour tooisolate de groupe réseau sécurité application de la carte de fidélité hello Contoso réseau d’entreprise.  

Pourquoi **abonnement de développement**, ils créent :

| Type de ressource | Nom | Description |
| --- | --- | --- |
| Réseau virtuel |vnInternal |Sert d’environnement de développement de carte de fidélité Contoso hello et est connecté via le réseau d’entreprise de tooContoso ExpressRoute. |

Pourquoi **abonnement de production**, ils créent :

| Type de ressource | Nom | Description |
| --- | --- | --- |
| Réseau virtuel |vnExternal |Héberge l’application de carte de fidélité hello et n’est pas connecté directement tooContoso's ExpressRoute. Code qui est transmise via leur système de Code Source directement les services PaaS toohello. |
| Groupe de sécurité réseau |nsgBitBucket |Permet de s’assurer que hello surface d’attaque de cette charge de travail est réduite en autorisant uniquement les communications entrantes sur le port TCP 443.  Contoso examine également une éventuelle protection supplémentaire par le biais d’un pare-feu d’applications web. |

### <a name="resource-locks"></a>Verrous de ressources
Dave Alice conférer et déterminer les verrous des ressources tooadd sur certaines ressources clés hello hello environnement tooprevent une suppression accidentelle pendant un push de code malintentionné.

Ils créent hello suivant verrou :

| Type de verrou | Ressource | Description |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |personnes tooprevent de supprimer le réseau virtuel de hello ou sous-réseaux. verrou de Hello n’empêche pas l’ajout de hello de nouveaux sous-réseaux. |

### <a name="azure-automation"></a>Azure Automation
Alice et son équipe de développement ont environnement de hello toomanage runbooks étendue pour cette application. les runbooks Hello autorisent hello Ajout/Suppression de nœuds pour l’application hello et d’autres tâches de DevOps.

toouse ces procédures opérationnelles, elles permettent [Automation](../automation/automation-intro.md).

### <a name="azure-security-center"></a>Azure Security Center
Gestion des services informatiques de Contoso doit tooquickly identifier et gérer les menaces. Ils veulent également toounderstand quels sont les problèmes éventuels.  

toofulfill permet à ces exigences, Dave Azure Security Center. Il garantit que hello Azure Security Center est hello ressources et fournit l’accès toohello les équipes de sécurité et DevOps.

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la création de modèles du Gestionnaire de ressources, consultez [meilleures pratiques pour la création de modèles Azure Resource Manager](resource-manager-template-best-practices.md).

