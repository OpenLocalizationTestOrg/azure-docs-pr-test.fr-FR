---
title: "aaaAzure AD Connect et la fédération | Documents Microsoft"
description: "Cette page est un emplacement central hello toute la documentation sur les opérations AD FS qui utilisent Azure AD Connect."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Fédération avec Azure AD Connect
Azure Active Directory (Azure AD) Connect vous permet de configurer la fédération avec Active Directory Federation Services (AD FS) et Azure AD au niveau local. Avec dans fédération, vous pouvez activer toosign utilisateurs dans tooAzure basée sur Active Directory avec leur mot de passe local et de services, tandis que sur le réseau d’entreprise de hello, sans avoir à tooenter leurs mots de passe à nouveau. En utilisant l’option de fédération hello avec AD FS, vous pouvez déployer une nouvelle installation des services AD FS, ou vous pouvez spécifier une installation existante dans une batterie de serveurs Windows Server 2012 R2.

Cette rubrique est hello accueil pour plus d’informations sur les fonctionnalités liées à la fédération pour Azure AD Connect. Il répertorie les liens tooall les rubriques connexes. Pour les liens tooAzure AD Connect, consultez [intégrer vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect : rubriques sur la fédération
| Rubrique | Qu’il couvre et à quel moment tooread il |
|:--- |:--- |
| **Options de connexion de l’utilisateur via Azure AD Connect** | |
| [Présentation des options de connexion de l’utilisateur](active-directory-aadconnect-user-signin.md) |En savoir plus sur les options de connexion utilisateur différents et comment ils affectent l’expérience utilisateur hello signe dans Azure. |
| **Installation d’AD FS avec Azure AD Connect** | |
| [Configuration requise](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Consultez les conditions préalables de hello pour réussir l’installation AD FS via Azure AD Connect. |
| [Configurer une batterie de serveurs AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Installation d’une nouvelle batterie de serveurs AD FS avec Azure AD Connect |
| [Fédérer avec Azure AD à l’aide d’un ID de connexion de substitution](active-directory-aadconnect-federation-management.md#alternateid) | Configurer la fédération à l’aide d’un ID de connexion de substitution  |
| **Modifier la configuration hello AD FS** | |
| [Réparation hello approbation](active-directory-aadconnect-federation-management.md#repairthetrust) |Approbation en cours de réparation hello entre locaux AD FS et Office 365/Azure. |
| [Ajouter un nouveau serveur AD FS](active-directory-aadconnect-federation-management.md#addadfsserver) |Extension d’une batterie de serveurs AD FS avec l’ajout d’un serveur AD FS après l’installation initiale |
| [Ajouter un nouveau serveur de proxy d’application web AD FS](active-directory-aadconnect-federation-management.md#addwapserver) |Extension d’une batterie de serveurs AD FS avec l’ajout d’un serveur proxy d’application web après l’installation initiale. |
| [Ajouter un nouveau domaine fédéré](active-directory-aadconnect-federation-management.md#addfeddomain) |Ajouter un autre domaine toobe fédéré avec Azure AD. |
| [Mettre à jour le certificat SSL de hello](active-directory-aadconnectfed-ssl-update.md)| Mettre à jour du certificat SSL de hello pour une batterie de serveurs AD FS. |
| **Autre configuration de fédération** | |
| [Fédérer plusieurs instances d’Azure AD avec une seule instance d’AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Fédérer plusieurs instances d’Azure AD avec une seule batterie de serveurs AD FS| 
| [Ajouter un logo/une illustration personnalisée de la société](active-directory-aadconnect-federation-management.md#customlogo) |Modifier l’expérience de connexion hello en spécifiant le logo hello personnalisé qui s’affiche sur hello AD FS-page de connexion. |
| [Ajout d’une description de connexion](active-directory-aadconnect-federation-management.md#addsignindescription) |Modifier la description de la connexion hello sur la page de connexion hello AD FS. |
| [Modification des règles de revendication AD FS](active-directory-aadconnect-federation-management.md#modclaims) |Modifier ou ajouter des règles de revendication dans AD FS qui correspondent de configuration de la synchronisation tooAzure AD Connect. |


## <a name="additional-resources"></a>Ressources supplémentaires
* [Fédérer deux Azure AD avec un seul AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Déploiement des services AD FS dans Azure](active-directory-aadconnect-azure-adfs.md)
* [Déploiement des services AD FS haute disponibilité par-delà les frontières dans Azure avec Azure Traffic Manager](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
