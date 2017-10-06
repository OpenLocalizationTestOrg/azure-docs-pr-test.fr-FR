---
title: "Identité hybride : Comparaison des outils d’intégration d’annuaire | Microsoft Docs"
description: "Ceci est la page fournit une table complète qui compare hello différents outils d’intégration active qui peuvent être utilisés pour l’intégration d’annuaire."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Identité hybride : Comparaison des outils d’intégration d’annuaire
Années hello outils d’intégration d’annuaire hello ont augmenté et a évolué.  Ce document est toohelp fournissent une vue consolidée de ces outils et une comparaison des fonctionnalités hello qui sont disponibles dans chacun.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect comprend les composants hello ainsi que des fonctionnalités précédemment publiées sous le nom de Dirsync et AAD Sync. Ces outils sont en cours ne sont plus disponibles individuellement, et toutes les futures améliorations seront incluses dans les mises à jour tooAzure AD se connecter, afin que vous sachiez toujours où tooget hello dernières fonctionnalités.
> 
> DirSync et Azure AD Sync sont déconseillés. Des informations supplémentaires sont disponibles [ici](active-directory-aadconnect-dirsync-deprecated.md).
> 
> 

Utilisez hello clé suivante pour chacune des tables de hello.

● = Disponible maintenant  
FR = Version à venir  
PP = Version préliminaire publique  

## <a name="on-premises-toocloud-synchronization"></a>TooCloud synchronisation locale
| Fonctionnalité | Azure Active Directory Connect | Services de synchronisation Azure Active Directory (AAD Sync) | Outil de synchronisation Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Se connecter toosingle forêt Active Directory local |● |● |● |● |● |
| Se connecter toomultiple local forêts AD |● |● | |● |● |
| Se connecter toomultiple les organisations d’Exchange sur site |● | | | | |
| Connecter le service d’annuaire LDAP local toosingle |FR | | |● |● |
| Connecter les annuaires LDAP locaux toomultiple |FR | | |● |● |
| Se connecter tooon local AD et les annuaires LDAP locaux |FR | | |● |● |
| Se connecter toocustom systèmes (autrement dit, SQL, Oracle, MySQL, etc.) |FR | | |● |● |
| Synchronisation des attributs définis par le client (extensions de répertoire) |● | | | | |
| Se connecter tooon local HR (par exemple, SAP, Oracle e-Business, PeopleSoft) |FR | | |● |● |
| Prend en charge les connecteurs et les règles de synchronisation FIM pour la configuration des systèmes de site tooon. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>Synchronisation des clouds tooOn local
| Fonctionnalité | Azure Active Directory Connect | Services de synchronisation Azure Active Directory | Outil de synchronisation Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Écriture différée des appareils |● | |● | | |
| Écriture différée des attributs (pour un déploiement hybride Exchange) |● |● |● |● |● |
| Écriture différée des objets groupes |● | | | | |
| Écriture différée des mots de passe (à partir de la réinitialisation de mot de passe libre-service et de la modification de mot de passe) |● |● | | | |

## <a name="authentication-feature-support"></a>Prise en charge des fonctionnalités d’authentification
| Fonctionnalité | Azure Active Directory Connect | Services de synchronisation Azure Active Directory | Outil de synchronisation Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Synchronisation de mot de passe pour une forêt AD locale |● |● |● | | |
| Synchronisation de mot de passe pour plusieurs forêts AD locales |● |● | | | |
| Authentification unique à l’aide de la fédération |● |● |● |● |● |
| Écriture différée des mots de passe (à partir de la réinitialisation de mot de passe libre-service et de la modification de mot de passe) |● |● | | | |

## <a name="set-up-and-installation"></a>Configuration et installation
| Fonctionnalité | Azure Active Directory Connect | Services de synchronisation Azure Active Directory | Outil de synchronisation Azure Active Directory (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| Installation des supports sur un contrôleur de domaine |● |● |● | |
| Installation des supports à l’aide de SQL Express |● |● |● | |
| Mise à niveau facile à partir de DirSync |● | | | |
| Localisation de l’Admin UX tooWindows langues du serveur |● |● |● | |
| Localisation de l’utilisateur final UX tooWindows langues du serveur | | | |● |
| Prise en charge pour Windows Server 2008 et Windows Server 2008 R2 |● pour la synchronisation, pas pour la fédération |● |● |● |
| Prise en charge pour Windows Server 2012 et Windows Server 2012 R2 |● |● |● |● |

## <a name="filtering-and-configuration"></a>Filtrage et configuration
| Fonctionnalité | Azure Active Directory Connect | Services de synchronisation Azure Active Directory | Outil de synchronisation Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Filtrage sur les domaines et les unités organisationnelles |● |● |● |● |● |
| Filtrage sur les valeurs d’attributs des objets |● |● |● |● |● |
| Autoriser l’ensemble minimal d’attributs toobe de synchronisation (MinSync) |● |● | | | |
| Autoriser toobe de modèles de service différents ont été appliqué pour les flux d’attributs. |● |● | | | |
| Autoriser les attributs de suppression circulent d’AD tooAzure AD |● |● | | | |
| Autorisation de la personnalisation avancée pour les flux d’attributs |● |● | |● |● |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

