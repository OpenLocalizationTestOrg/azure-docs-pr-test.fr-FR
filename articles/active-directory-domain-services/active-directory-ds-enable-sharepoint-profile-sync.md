---
title: 'Services de domaine Azure Active Directory : Activer la prise en charge du service Profil utilisateur SharePoint | Microsoft Docs'
description: "Configurer la synchronisation de profil de toosupport de domaines gérés Azure Active Directory Domain Services pour SharePoint Server"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>Configurer une synchronisation de profil de domaine géré toosupport pour SharePoint Server
SharePoint Server inclut un service Profil utilisateur qui est utilisé pour la synchronisation des profils utilisateurs. tooset des hello Service de profil utilisateur, les autorisations appropriées doivent toobe d’accorder sur un domaine Active Directory. Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).

Cet article explique comment vous pouvez configurer le service de synchronisation de profil utilisateur SharePoint Server des Services de domaine Active Directory de Azure domaines gérés toodeploy hello.

## <a name="hello-aad-dc-service-accounts-group"></a>groupe de « Comptes de Service de contrôleur de domaine AAD » Hello
Un groupe de sécurité appelé «**des comptes de Service de contrôleur de domaine AAD**' n’est disponible dans l’unité d’organisation hello « Utilisateurs » sur votre domaine géré. Vous pouvez consulter ce groupe Bonjour **Active Directory Users and Computers** le composant logiciel enfichable MMC sur votre domaine géré.

![Groupe de sécurité Comptes de service de contrôleur de domaine AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

Les membres de ce groupe de sécurité sont hello délégué suivant des privilèges :
- privilège de 'répliquer des modifications répertoire Hello sur la racine de hello DSE Hello géré de domaine.
- Hello privilège « Répliquer les modifications de répertoire » sur le contexte d’appellation de Configuration hello (cn = configuration container) hello gérés domaine.

Ce groupe de sécurité est également membre du groupe intégré de hello **accès Compatible pré-Windows 2000**.

![Groupe de sécurité Comptes de service de contrôleur de domaine AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>Activer votre toosupport domaine géré synchronisation du profil utilisateur SharePoint Server
Vous pouvez ajouter le compte de service hello utilisée pour SharePoint utilisateur profil synchronisation toohello **des comptes de Service de contrôleur de domaine AAD** groupe. Par conséquent, compte de synchronisation hello obtient Active toohello de privilèges adéquats tooreplicate modifications. Cette étape de configuration permet de SharePoint Server utilisateur profil synchronisation toowork correctement.

![Comptes de service de contrôleur de domaine AAD – ajouter des membres](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Comptes de service de contrôleur de domaine AAD – ajouter des membres](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>Contenu connexe
* [Informations techniques de référence – Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)
