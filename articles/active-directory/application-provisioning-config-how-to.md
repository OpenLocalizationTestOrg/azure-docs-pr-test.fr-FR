---
title: "utilisateur de tooconfigure aaaHow approvisionnement d’une application de la galerie tooan Azure AD | Documents Microsoft"
description: "Comment vous pouvez configurer rapidement compte utilisateur riche et annulation tooapplications déjà énumérées dans la galerie d’applications Azure AD de hello"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>La configuration d’application de la galerie tooan Azure AD de l’utilisateur tooconfigure

*L’approvisionnement de comptes utilisateur* est act hello de création, mise à jour et/ou la désactivation des enregistrements de compte d’utilisateur dans le magasin de profils utilisateur local d’une application. La plupart des cloud et les applications SaaS hello utilisateurs rôles et autorisations dans leur propre magasin de profils utilisateur local est enregistré et la présence d’un enregistrement d’utilisateur dans leur magasin local *requis* pour toowork d’accès et de l’authentification unique.

Bonjour portail Azure, hello **Provisioning** onglet dans le volet de navigation gauche hello pour une application d’entreprise affiche les modes de configuration sont pris en charge pour cette application. Deux valeurs sont possibles :

## <a name="configuring-an-application-for-manual-provisioning"></a>Configuration d’une application pour l’approvisionnement manuel

*Manuel* configuration signifie que les comptes d’utilisateur doivent être créés manuellement à l’aide de méthodes de hello fournies par cette application. Cela peut impliquer une connexion à un portail d’administration pour cette application et l’ajout d’utilisateurs à l’aide d’une interface utilisateur web. Il peut également s’agir d’une feuille de calcul comportant les détails des comptes d’utilisateur, qui doit être chargée à l’aide d’un mécanisme fourni par l’application. Consultez la documentation de hello fournie par l’application hello ou application hello contact mécanismes de développeur toodetermine wat sont disponibles.

Si manuelle est seule hello affiché pour une application donnée, cela signifie qu’aucun AD Azure automatique mise en service du connecteur n’a été créé pour l’application hello. Ou bien, cela signifie que l’application hello n'est pas prise en charge hello préalable utilisateur API de gestion sur le toobuild un connecteur d’approvisionnement automatisé.

Si vous souhaitez que la prise en charge de toorequest pour la configuration automatique pour une application donnée, vous pouvez remplir une demande à <http://aka.ms/aadapprequest>.

## <a name="configuring-an-application-for-automatic-provisioning"></a>Configuration d’une application pour l’approvisionnement automatique

*Automatique* : dans le cadre d’un approvisionnement automatique, un connecteur d’approvisionnement Azure AD a été développé pour cette application. Pour plus d’informations sur hello Azure AD de configuration de service et de son fonctionnement, consultez [tooSaaS automatiser l’approvisionnement des utilisateurs et Deprovisioning Applications avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).

Pour plus d’informations sur comment tooprovision des utilisateurs spécifiques et l’application de tooan de groupes, consultez [la gestion de l’approvisionnement de comptes utilisateur pour les applications d’entreprise](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).

Hello étapes réelles des tooenable requis et configurer la configuration automatique varient en fonction de l’application hello.

>[!NOTE]
>Vous devez commencer par recherche hello toosetting spécifique didacticiel de programme d’installation de configuration pour votre application et d’après ces étapes de tooconfigure application hello et Azure AD toocreate hello connexion mise en service. 
>
>

Vous trouverez des didacticiels de l’application à [liste de didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

Un tooconsider plus important lors de la configuration de l’approvisionnement d’être tooreview et configurer les mappages d’attributs hello et flux de travail qui définissent le flux de propriétés utilisateur (ou groupe) à partir de l’application de toohello Azure AD. Cela inclut le paramètre hello « correspondance property » être toouniquely utilisé identifier et correspondent aux utilisateurs/groupes entre les systèmes de hello deux. Pour plus d’informations sur ce processus important.

## <a name="next-steps"></a>Étapes suivantes
[Personnalisation des mappages d’attributs d’approvisionnement d’utilisateurs pour les applications SaaS dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

