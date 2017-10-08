---
title: aaaUnderstand architecture Azure Active Directory | Documents Microsoft
description: "Explique ce qu’un locataire Azure AD est et comment toomanage Azure via Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Comprendre l’architecture Azure Active Directory
Azure permet d’Active Directory (Azure AD) vous toosecurely gérer l’accès tooAzure services et ressources pour vos utilisateurs. Azure AD comprend une suite complète de fonctionnalités de gestion des identités. Pour plus d’informations sur les fonctionnalités d’Azure AD, voir [Qu’est Azure Active Directory ?](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis)

Avec Azure AD, vous pouvez créer et gérer des utilisateurs et groupes et activer les autorisations tooallow et refuser l’accès tooenterprise ressources. Pour plus d’informations sur la gestion d’identité, consultez [hello notions de base de gestion des identités Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Architecture Azure AD
Architecture distribuée géographiquement de d’Azure AD combine surveillance étendue, de la redirection automatique, de basculement et restauration nous permettre de clients tooour toodeliver hautes disponibilité et les performances.

Hello suivant d’éléments de l’architecture est traité dans cet article :
 *  Conception de l’architecture de service
 *  Extensibilité 
 *  Disponibilité continue
 *  Centres de données

### <a name="service-architecture-design"></a>Conception de l’architecture de service
Hello toobuild de façon plus courantes un système évolutif, hautement disponible et riches en données s’effectue via des indépendants des blocs de construction ou d’unités d’échelle pour la couche de données hello Azure AD, les unités d’échelle sont appelées *partitions*. 

couche de données Hello a plusieurs services frontaux qui fournissent la fonctionnalité de lecture-écriture. diagramme de Hello ci-dessous montre comment les composants hello d’une partition de répertoire unique sont distribués dans l’ensemble des centres de données géographiquement distribuée. 

  ![Partitions à répertoire unique](./media/active-directory-architecture/active-directory-architecture.png)

les composants de Hello de l’architecture d’Azure AD incluent un réplica principal et les réplicas secondaires.

**Réplica principal**

Hello *réplica principal* reçoit tous les *écrit* de partition hello auquel il appartient. Une opération d’écriture tooa immédiatement répliquées de réplica secondaire dans un autre centre de données avant de retourner l’appelant de toohello de réussite, afin de garantir la durabilité des écritures de géo-redondant.

**Réplicas secondaires**

Toutes les *lectures* de répertoire sont traitées à partir des *réplicas secondaires*, qui se trouvent dans des centres de données répartis entre différentes zones géographiques. Il existe plusieurs réplicas secondaires, car les données sont répliquées de manière asynchrone. Lectures de répertoire, telles que les demandes d’authentification, sont traitées à partir de centres de données qui sont des clients de tooour fermer. les réplicas secondaires Hello sont responsables de l’évolutivité de lecture.

### <a name="scalability"></a>Extensibilité

L’évolutivité est la capacité hello un toomeet de tooexpand service besoins de performances. Écrire l’évolutivité en partitionnant les données hello. Évolutivité de lecture est obtenue par la réplication de données d’une partition toomultiple ces derniers dispersées Bonjour.

Demandes à partir d’applications d’annuaire sont généralement routé toohello de centre de données qu’ils sont physiquement le plus proche. Écritures sont la cohérence de lecture-écriture tooprovide toohello redirigé en toute transparence réplica principal. Réplicas secondaires étendent considérablement échelle hello de partitions, car les répertoires de hello sont généralement les lectures à servir la plupart du temps de hello.

Applications d’annuaire connectent toohello le plus proche de centres de données. Cela améliore les performances, et par conséquent la montée en charge devient possible. Dans la mesure où une partition d’annuaire peut avoir plusieurs réplicas secondaires, réplicas secondaires peuvent être placés clients d’Active Directory toohello plus proche. Uniquement annuaire interne composants de service qui sont le réplica principal actif de hello gourmandes en écriture cible directement.

### <a name="continuous-availability"></a>Disponibilité continue

Disponibilité (ou un temps d’activité) définit la capacité hello un tooperform système sans interruption. tooAzure de clé Hello d’AD haute disponibilité est que nos services peuvent rapidement se déplacer le trafic entre plusieurs centres de données de dispersé géographiquement. Chaque centre de données est indépendant, ce qui permet les modes d’échec décorrélés.

Conception des partitions d’Azure AD est simplifié toohello comparés enterprise conception Active Directory, qui est essentielle pour la mise à l’échelle de système de hello. Nous avons adopté une conception maître unique qui inclut un processus de basculement du réplica principal soigneusement orchestré et déterministe.

**Tolérance de panne**

Un système est plus disponible s’il s’agit des échecs de toohardware, de réseau et de logiciels à tolérance de panne. Pour chaque partition de répertoire de hello, il existe un réplica principal hautement disponible : réplica principal de hello. Uniquement les partitions toohello écritures sont effectuées dans ce réplica. Ce réplica est en permanence et étroitement surveillés et les écritures peuvent être décalées immédiatement tooanother réplica (qui devient hello nouveau réplica principal) si une défaillance est détectée. Pendant le basculement, une perte de disponibilité de l’écriture de 1 à 2 minutes est possible. La disponibilité de lecture n’est pas affectée pendant cette période.

Les opérations de lecture (lequel plus nombreuses que les écritures par ordre de grandeur nombreux) ne va pas toosecondary réplicas. Étant donné que les réplicas secondaires sont idempotents, une perte de tout un réplica sur une partition donnée est facilement compensée en dirigeant hello lectures tooanother réplica, généralement hello même centre de données.

**Durabilité des données**

Une écriture est validée durablement tooat au moins deux tooit données centres préalable accusée. Cela se produit par tout d’abord valider écriture hello sur hello principal, puis immédiatement réplication hello écriture tooat au moins un autre centre de données. Ainsi, un risque de perte catastrophique de hello données center hébergement hello principal n’entraîne pas de perte de données.

Azure AD conserve un zéro [temps de récupération (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) d’émission de jeton et du répertoire lit et écrit dans l’ordre de hello de minutes (5 minutes) RTO pour le répertoire. Nous maintenons également un [objectif de point de récupération (RPO)](https://en.wikipedia.org/wiki/Recovery_point_objective) égal à 0 et sans perte de données lors des basculements.

### <a name="data-centers"></a>Centres de données

Les réplicas d’Azure AD sont stockés dans les centres de données situés dans l’ensemble de Bonjour. Pour plus d’informations,voir [Centres de données Azure](https://azure.microsoft.com/en-us/overview/datacenters).

Azure AD fonctionne entre les centres de données avec hello suivant caractéristiques :

 * L’authentification, graphique et autres services Active Directory se trouvent derrière hello service de passerelle. Hello passerelle gère l’équilibrage de charge de ces services. Elle basculera automatiquement si des serveurs défaillants sont détectés par les sondes d’intégrité transactionnelles. Selon ces sondes d’intégrité, hello passerelle achemine dynamiquement le trafic toohealthy des centres de données.
 * Pour *lit*, répertoire de hello a des réplicas secondaires et les services frontaux correspondants dans une configuration actif / actif dans plusieurs centres de données. En cas de défaillance d’un centre de données, le trafic sera automatiquement routé tooa des centres de données.
 *  Pour *écrit*, hello active sera basculement (principale) réplica principal dans les centres de données via planifié (nouveau réplica principal est synchronisée tooold principal) ou des procédures de basculement en cas d’urgence. Durabilité des données est obtenue en répliquant toute validation tooat au moins deux des centres de données.

**Cohérence des données**

modèle d’annuaire Hello est un des cohérence éventuelle. Un problème classique avec la réplication asynchrone des systèmes distribués est que les données de salutation retournées à partir d’un réplica « spécifique » ne soient pas des toodate. 

Azure AD fournit une cohérence de lecture-écriture pour les applications qui ciblent un réplica secondaire en routant réplica toohello écritures et extraction de façon synchrone hello réécrit réplica toohello.

Application écrit à l’aide de hello API d’Azure AD Graph sont extraits à partir de la maintenance d’affinité tooa directory réplique par souci de cohérence en lecture-écriture. Hello service Azure AD Graph gère une session logique, qui présente le réplica secondaire d’affinité tooa utilisé pour les lectures ; affinité est capturée dans un « jeton de réplica « hello service graphique met en cache à l’aide d’un cache distribué. Ce jeton est ensuite utilisé pour les opérations suivantes dans hello même session logique. 

 >[!NOTE]
 >Écritures sont répliquées immédiatement les lectures toohello réplica secondaire toowhich hello logique de la session ont été émis.
 >

**Protection de la sauvegarde**

répertoire de Hello implémente des suppressions récupérables, au lieu de suppressions de disque durs, pour les utilisateurs et les locataires pour la récupération en cas de suppressions accidentelles par un client simple. Si votre administrateur client accidentellement supprime les utilisateurs, ils peuvent facilement annuler et restaurer les utilisateurs hello supprimé. 

Azure AD implémente les sauvegardes quotidiennes de toutes les données et peut, par conséquent, restaurer avec autorité les données dans le cas de suppressions logiques ou de corruptions. Notre niveau de données employant des codes de correction d’erreur, il peut détecter les erreurs et corriger automatiquement certains types d’erreurs de disque.

**Mesures et analyses**

L’exécution d’un service haute disponibilité requiert des mesures et des capacités d’analyse hautes performances. Azure AD analyse et signale en permanence les mesures d’intégrité des services clés et les critères de réussite pour chacun de ses services. Nous développons et affinons en permanence les mesures, surveillant et alertant pour chaque scénario au sein de chaque service Azure AD, mais aussi sur tous les autres services.

Si un service Azure AD ne fonctionne pas comme prévu, nous entrent immédiatement en fonctionnalités de toorestore action aussi rapidement que possible. Bonjour assure le suivi de la métrique Azure AD plus important est la rapidité avec laquelle nous pouvons détecter et atténuer un client ou live problème de site. Nous investir surveillance lourdement dans et alertes toominimize temps toodetect (TTD cible : < 5 minutes) et opérationnelle toominimize temps toomitigate (cible de commercialisation : < 30 minutes).

**Opérations sécurisées**

Nous utilisons des contrôles opérationnels, tels que l’authentification multifacteur (MFA) pour toute opération, ainsi que l’audit de toutes les opérations. En outre, nous utilisons un élévation de juste-à-temps système toogrant temporaire accès nécessaires pour toute tâche opérationnel sur demande en continu. Pour plus d’informations, consultez [hello approuvé de Cloud](https://azure.microsoft.com/en-us/support/trust-center).

## <a name="next-steps"></a>Étapes suivantes
[Guide du développeur Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

