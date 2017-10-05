---
title: "Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation | Microsoft Docs"
description: Explique le fonctionnement et la personnalisation de la synchronisation Azure AD Connect.
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
ms.openlocfilehash: 4edac05325ad12596d982d113df0db7461124b12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation
Les services de synchronisation Azure Active Directory Connect (synchronisation Azure AD Connect) sont un composant clé d’Azure AD Connect. Ils se chargent de toutes les opérations liées à la synchronisation des données d’identité entre votre environnement local et Azure AD. Le logiciel Azure AD Connect Sync est le successeur de DirSync, de Microsoft Azure AD Sync et de Forefront Identity Manager, avec le connecteur Azure Active Directory configuré.

Cette rubrique présente le composant **Azure AD Connect Sync** (également appelé **moteur de synchronisation**) et répertorie les liens vers toutes les autres rubriques qui lui sont associées. Pour consulter les liens vers Azure AD Connect, voir [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

Le service de synchronisation se compose de deux composants, le composant local **Azure AD Connect sync** et le composant côté service dans Azure AD, appelé **service de synchronisation Azure AD Connect**. Le service est courant pour DirSync, Azure AD Sync et Azure AD Connect.

## <a name="azure-ad-connect-sync-topics"></a>Rubriques de synchronisation Azure AD Connect
| Rubrique | Sujet qu’elle aborde et quand la consulter |
| --- | --- |
| **Principes de base d’Azure AD Connect Sync** | |
| [Présentation de l’architecture](active-directory-aadconnectsync-understanding-architecture.md) |Pour ceux qui découvrent le moteur de synchronisation et veulent en savoir plus sur l’architecture et les termes utilisés. |
| [Concepts techniques](active-directory-aadconnectsync-technical-concepts.md) |Le sujet de l’architecture est brièvement abordé et les termes utilisés sont expliqués de manière succincte. |
| [Topologies pour Azure AD Connect](active-directory-aadconnect-topologies.md) |Décrit les différents scénarios et topologies pris en charge par le moteur de synchronisation. |
| **Configuration personnalisée** | |
| [Exécuter à nouveau l’Assistant Installation](active-directory-aadconnectsync-installation-wizard.md) |Explique les options à votre disposition si vous réexécutez l’Assistant Installation d’Azure AD Connect. |
| [Comprendre l’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |Décrit le modèle de configuration appelé Approvisionnement déclaratif. |
| [Comprendre les expressions d’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |Décrit la syntaxe du langage d’expression utilisé dans l’approvisionnement déclaratif. |
| [Présentation de la configuration par défaut](active-directory-aadconnectsync-understanding-default-configuration.md) |Décrit les règles prêtes à l’emploi et la configuration par défaut. Explique également comment les règles fonctionnent en parallèle pour assurer la réussite des scénarios prêts à l’emploi. |
| [Présentation des utilisateurs et des contacts](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Suite de la rubrique précédente qui explique comment les configurations associées aux utilisateurs et contacts se complètent, en particulier dans un environnement à forêts multiples. |
| [Comment modifier la configuration par défaut](active-directory-aadconnectsync-change-the-configuration.md) |Vous montre comment modifier une configuration commune pour les flux d’attributs. |
| [Meilleures pratiques pour la modification de la configuration par défaut](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Prend en charge les limitations imposées à la configuration fournie par défaut et l’insertion de modifications. |
| [Configurer le filtrage](active-directory-aadconnectsync-configure-filtering.md) |Décrit les différentes options permettant de limiter le nombre d’objets en cours de synchronisation vers Azure AD et explique comment les configurer, étape par étape. |
| **Fonctionnalités et scénarios** | |
| [Prévention des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Décrit la fonctionnalité de *prévention des suppressions accidentelles* et explique comment la configurer. |
| [Scheduler](active-directory-aadconnectsync-feature-scheduler.md) |Décrit le planificateur intégré qui importe, synchronise et exporte les données. |
| [Implémenter la synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) |Décrit le fonctionnement de la synchronisation de mot de passe, en indiquant comment l’implémenter, comment l’utiliser et comment résoudre les problèmes associés. |
| [Écriture différée des appareils](active-directory-aadconnect-feature-device-writeback.md) |Décrit le fonctionnement de l’écriture différée des appareils dans Azure AD Connect. |
| [Extensions d’annuaire](active-directory-aadconnectsync-feature-directory-extensions.md) |Explique comment étendre le schéma Azure AD avec vos propres attributs personnalisés. |
| **Service de synchronisation** | |
| [Fonctionnalités du service de synchronisation Azure AD Connect](active-directory-aadconnectsyncservice-features.md) |Décrit le service synchronisation et comment modifier les paramètres de synchronisation dans Azure AD. |
| [Résilience d’attribut en double](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Décrit comment activer et utiliser la résilience des valeurs d’attribut en double **userPrincipalName** et **proxyAddresses**. |
| **Opérations et interface utilisateur** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |Décrit l’interface utilisateur de Synchronization Service Manager, notamment les onglets [Opérations](active-directory-aadconnectsync-service-manager-ui-operations.md), [Connecteurs](active-directory-aadconnectsync-service-manager-ui-connectors.md), [Metaverse Designer](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md) (Concepteur métaverse) et [Metaverse Search](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) (Recherche métaverse). |
| [Considérations et tâches opérationnelles](active-directory-aadconnectsync-operations.md) |Décrit les problèmes liés au fonctionnement, tels que la récupération d’urgence. |
| **Procédure** | |
| [Réinitialiser le compte Azure AD](active-directory-aadconnectsync-howto-azureadaccount.md) |Décrit la réinitialisation des informations d’identification du compte de service utilisé pour se connecter à Azure AD à partir de la synchronisation d’Azure AD Connect. |
| **Plus d’informations et de références** | |
| [Ports](active-directory-aadconnect-ports.md) |Répertorie les ports que vous devez ouvrir entre le moteur de synchronisation, vos répertoires locaux et Azure AD. |
| [Attributs synchronisés avec Azure Active Directory](active-directory-aadconnectsync-attributes-synchronized.md) |Répertorie tous les attributs en cours de synchronisation entre le système AD local et Azure AD. |
| [Référence des fonctions](active-directory-aadconnectsync-functions-reference.md) |Répertorie toutes les fonctions disponibles dans l’approvisionnement déclaratif. |

## <a name="additional-resources"></a>Ressources supplémentaires
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)

