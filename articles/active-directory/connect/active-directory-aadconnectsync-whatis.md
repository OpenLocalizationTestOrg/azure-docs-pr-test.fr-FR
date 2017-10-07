---
title: "Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation | Microsoft Docs"
description: Explique comment fonctionne de la synchronisation Azure AD Connect et toocustomize.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation
services de synchronisation Azure Active Directory Connect (synchronisation d’Azure AD Connect) Hello est un composant principal d’Azure AD Connect. Il prend en charge de toutes les opérations de hello sont les données d’identité associées toosynchronize entre votre environnement local et le Azure AD. Synchronisation Azure AD Connect est le successeur hello de Forefront Identity Manager DirSync et Azure AD Sync avec hello configuré par le connecteur Active Directory.

Cette rubrique est hello pour **synchronisation Azure AD Connect** (également appelé **moteur de synchronisation**) et les listes des liens tooall autres tooit connexes de rubriques. Pour les liens tooAzure AD Connect, consultez [intégrer vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

le service de synchronisation Hello comprend deux composants, hello local **synchronisation Azure AD Connect** composant et hello côté service dans Azure AD appelé **service de synchronisation Azure AD Connect**. service de Hello est courant pour la synchronisation d’annuaire Azure AD Sync et Azure AD Connect.

## <a name="azure-ad-connect-sync-topics"></a>Rubriques de synchronisation Azure AD Connect
| Rubrique | Qu’il couvre et à quel moment tooread |
| --- | --- |
| **Principes de base d’Azure AD Connect Sync** | |
| [Présentation de l’architecture hello](active-directory-aadconnectsync-understanding-architecture.md) |Pour ceux qui sont de nouveau moteur de synchronisation toohello et souhaitez toolearn sur l’architecture de hello et de termes hello utilisés. |
| [Concepts techniques](active-directory-aadconnectsync-technical-concepts.md) |Une version abrégée de rubrique d’architecture hello et brièvement explique hello termes utilisés. |
| [Topologies pour Azure AD Connect](active-directory-aadconnect-topologies.md) |Décrit les hello différents scénarios et topologies hello synchronisation moteur prend en charge. |
| **Configuration personnalisée** | |
| [Exécution hello installation de l’Assistant nouveau](active-directory-aadconnectsync-installation-wizard.md) |Explique les options que vous disposez quand vous réexécutez Assistant d’installation Bonjour Azure AD Connect. |
| [Comprendre l’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |Décrit le modèle de configuration hello appelé approvisionnement déclaratif. |
| [Comprendre les expressions d’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |Décrit la syntaxe hello pour le langage d’expression hello utilisé dans l’approvisionnement déclaratif. |
| [Présentation de la configuration par défaut hello](active-directory-aadconnectsync-understanding-default-configuration.md) |Décrit les règles d’out-of-box hello et la configuration par défaut de hello. Décrit également comment les règles de hello fonctionnent ensemble pour hello out-of-box scénarios toowork. |
| [Présentation des utilisateurs et des contacts](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Continue sur la rubrique précédente de hello et décrit la configuration hello pour les utilisateurs et contacts fonctionne ensemble, en particulier dans un environnement à forêts multiples. |
| [Comment toomake un toohello de modification de configuration par défaut](active-directory-aadconnectsync-change-the-configuration.md) |Vous guide dans le flux des toomake un tooattribute de modification de configuration courantes. |
| [Meilleures pratiques pour la modification de la configuration par défaut de hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Limitations de prise en charge et pour effectuer la configuration d’out-of-box toohello de modifications. |
| [Configurer le filtrage](active-directory-aadconnectsync-configure-filtering.md) |Décrit les différentes options de hello pour la procédure toolimit dans lequel les objets sont en cours de synchronisation tooAzure AD et procédure pas à pas tooconfigure ces options. |
| **Fonctionnalités et scénarios** | |
| [Prévention des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Décrit les hello *empêcher des suppressions accidentelles* fonctionnalité et comment tooconfigure il. |
| [Scheduler](active-directory-aadconnectsync-feature-scheduler.md) |Décrit le Planificateur intégré hello, qui est de l’importation, synchronisation et exportation de données. |
| [Implémenter la synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) |Décrit le fonctionne de la synchronisation de mot de passe, comment tooimplement et comment toooperate et résoudre les problèmes. |
| [Écriture différée des appareils](active-directory-aadconnect-feature-device-writeback.md) |Décrit le fonctionnement de l’écriture différée des appareils dans Azure AD Connect. |
| [Extensions d’annuaire](active-directory-aadconnectsync-feature-directory-extensions.md) |Décrit comment tooextend hello schéma Active Directory Azure avec vos propres attributs personnalisés. |
| **Service de synchronisation** | |
| [Fonctionnalités du service de synchronisation Azure AD Connect](active-directory-aadconnectsyncservice-features.md) |Décrit le côté service de synchronisation hello et comment toochange synchroniser les paramètres dans Azure AD. |
| [Résilience d’attribut en double](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Décrit comment tooenable et utiliser **userPrincipalName** et **proxyAddresses** résilience de valeurs d’attribut en double. |
| **Opérations et interface utilisateur** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |Décrit les hello UI Synchronization Service Manager, y compris [Operations](active-directory-aadconnectsync-service-manager-ui-operations.md), [connecteurs](active-directory-aadconnectsync-service-manager-ui-connectors.md), [Concepteur de métaverse](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), et [recherche de métaverse](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) onglets. |
| [Considérations et tâches opérationnelles](active-directory-aadconnectsync-operations.md) |Décrit les problèmes liés au fonctionnement, tels que la récupération d’urgence. |
| **Procédure** | |
| [Réinitialiser le compte de hello Azure AD](active-directory-aadconnectsync-howto-azureadaccount.md) |Informations d’identification de hello tooreset hello du compte de service utilisation tooconnect à partir d’Azure AD Connect tooAzure de synchronisation Active Directory. |
| **Plus d’informations et de références** | |
| [Ports](active-directory-aadconnect-ports.md) |Listes de ports vous doivent tooopen entre le moteur de synchronisation hello, vos annuaires locaux et Azure AD. |
| [Attributs synchronisés tooAzure Active Directory](active-directory-aadconnectsync-attributes-synchronized.md) |Répertorie tous les attributs en cours de synchronisation entre le système AD local et Azure AD. |
| [Référence des fonctions](active-directory-aadconnectsync-functions-reference.md) |Répertorie toutes les fonctions disponibles dans l’approvisionnement déclaratif. |

## <a name="additional-resources"></a>Ressources supplémentaires
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)

