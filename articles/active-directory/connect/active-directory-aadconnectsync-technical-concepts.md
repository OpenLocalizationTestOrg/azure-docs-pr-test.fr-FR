---
title: "Azure AD Connect Sync : Concepts techniques | Microsoft Docs"
description: Explique les concepts de techniques de hello de synchronisation Azure AD Connect.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Azure AD Connect Sync : Concepts techniques
Cet article est un résumé de la rubrique de hello [présentation de l’architecture](active-directory-aadconnectsync-technical-concepts.md).

Azure AD Connect Sync repose sur une plateforme de synchronisation de méta-annuaire solide.
Hello les sections suivantes présente les concepts de hello la synchronisation de méta-annuaires.
S’appuyant sur MIIS, ILM et FIM, hello Azure Active Directory Sync Services fournit plateforme hello pour les sources de connexion toodata, synchronisation des données entre des sources de données, ainsi que hello et annulation des identités.

![Concepts techniques](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Hello les sections suivantes fournit plus de détails sur hello suivant des aspects du Service de synchronisation FIM de hello :

* Connecteur
* Flux d’attributs
* Espace de connecteur
* Métaverse
* Approvisionnement

## <a name="connector"></a>Connecteur
modules de code Hello toocommunicate utilisé avec un annuaire connecté sont appelés liens (anciennement (MAs) des agents de gestion).

Ceux-ci sont installés sur l’ordinateur hello synchronisation Azure AD Connect. les connecteurs Hello fournissent hello capacité sans agent tooconverse à l’aide de protocoles système distants au lieu de compter sur le déploiement de hello d’agents spécialisés. Cela se traduit par une réduction des risques et de la durée de déploiement, en particulier quand il s’agit de systèmes et d’applications critiques.

Dans l’image hello ci-dessus, connecteur de hello est synonyme de l’espace de connecteur hello mais englobe toutes les communications avec le système externe de hello.

Hello connecteur est responsable de toutes les importent et exporter des fonctionnalités toohello système évite aux développeurs d’avoir toounderstand comment tooconnect tooeach système en mode natif lorsque vous utilisez des transformations de données toocustomize approvisionnement déclaratif.

Les importations et exportations ne se produisent lors de la planification, permet davantage d’isolation des modifications qui se produisent dans le système de hello, étant donné que les modifications se propagent pas automatiquement source de données connectée toohello. En outre, les développeurs peuvent créer leurs propres connecteurs pour se connecter toovirtually n’importe quelle source de données.

## <a name="attribute-flow"></a>Flux d’attributs
Hello métaverse est vue hello consolidé de toutes les identités jointes à partir des espaces connecteurs voisins. Dans la figure hello ci-dessus, flux d’attribut est représenté par des lignes fléchées pour les flux entrant et sortant. Flux d’attribut consiste à hello copie ou de transformation des données à partir d’un système tooanother et tous les attributs de flux (entrants ou sortants).

Flux d’attribut se produit entre l’espace de connecteur de hello et hello métaverse bidirectionnelle des opérations de synchronisation (complète ou delta) sont planifiée toorun.

Le flux d’attributs se produit uniquement quand ces synchronisations sont exécutées. Les flux d’attributs sont définis dans des règles de synchronisation. Il peut s’agir d’entrantes (ISR dans l’image hello ci-dessus) ou sortantes (OSR dans l’image hello ci-dessus).

## <a name="connected-system"></a>Système connecté
Système connecté (également appelé annuaire connecté) fait référence le système distant de toohello Azure synchronisation AD Connect s’est connecté tooand lecture et écriture tooand de données d’identité à partir de.

## <a name="connector-space"></a>Espace de connecteur
Chaque source de données connectée est représentée comme un sous-ensemble filtré des objets de hello et les attributs dans l’espace de connecteur hello.
Ainsi, toooperate de service de synchronisation hello localement sans le système distant de hello besoin toocontact hello lors de la synchronisation des objets de hello et restreint l’interaction tooimports et exporte uniquement.

Lors de la source de données hello et le connecteur de hello ont hello capacité tooprovide une liste des modifications (importation delta), puis hello efficacité opérationnelle augmente considérablement que seules les modifications apportées depuis la dernière interrogation. hello cycle est échangés. espace de connecteur Hello isole la source de données connectée hello de propagation automatique par nécessitant que cette planification du connecteur hello importe et exporte des changements. Cette garantie accorde la tranquillité d’esprit lors du test, l’aperçu ou confirmation de la prochaine mise à jour de hello.

## <a name="metaverse"></a>Métaverse
Hello métaverse est vue hello consolidé de toutes les identités jointes à partir des espaces connecteurs voisins.

Comme les identités sont liées entre elles et autorité est affectée pour divers attributs via les mappages de flux d’importation, objet de métaverse central hello commence tooaggregate les informations à partir de plusieurs systèmes. À partir de ce flux d’attribut objet, les mappages véhiculent des systèmes d’information toooutbound.

Objets sont créés quand un système faisant autorité les projette dans hello métaverse. Dès que toutes les connexions sont supprimées, l’objet de métaverse hello est supprimé.

Objets hello métaverse ne peut pas être modifiées directement. Toutes les données dans l’objet de hello doivent être utilisées via les flux d’attribut. Hello métaverse gère des connecteurs persistants pour chaque espace connecteur. Ces connecteurs ne nécessitent pas de réévaluation pour chaque exécution de la synchronisation. Cela signifie que la synchronisation Azure AD Connect n’est pas toolocate hello correspondant à distance objet chaque fois. Cela évite hello tooattributes de modifications tooprevent agents coûteux qui serait normalement responsable de la mise en corrélation des objets de hello.

Lorsque nouvelles sources de données qui peuvent avoir des objets préexistants toobe géré, les utilisations de synchronisation Azure AD Connect un processus appelé une jointure règle tooevaluate les candidats potentiels avec le tooestablish un lien.
Une fois le lien de hello est établie, cette évaluation ne se reproduit pas et le flux d’attribut normal peut se produire entre la source de données connectée distante hello et hello métaverse.

## <a name="provisioning"></a>Approvisionnement
Lorsqu’une source d’autorité projette un nouvel objet dans le métaverse hello un nouvel objet d’espace connecteur peut être créé dans un autre connecteur représentant une source de données connectée.

Cela établit intrinsèquement un lien, et le flux d’attributs peut se produire de manière bidirectionnelle.

Chaque fois qu’une règle détermine qu’un nouvel objet d’espace connecteur doit toobe créé, il est appelé mise en service. Toutefois, étant donné que cette opération a lieu uniquement dans l’espace de connecteur hello, il ne s’applique pas dans la source de données connectée hello jusqu'à ce qu’une exportation est effectuée.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Azure AD Connect Sync : personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
