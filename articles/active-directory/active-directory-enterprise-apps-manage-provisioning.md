---
title: "aaaUser mise en service de gestion pour les applications d’entreprise Bonjour Azure Active Directory | Documents Microsoft"
description: "Découvrez comment toomanage utilisateur compte de configuration pour les applications d’entreprise à l’aide de hello Azure Active Directory"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>La gestion de compte d’utilisateur de configuration pour les applications d’entreprise Bonjour portail Azure
Cet article décrit comment toouse hello [portail Azure](https://portal.azure.com) catégorie de compte d’utilisateur automatique toomanage de configuration et de l’annulation du déploiement pour les applications qui prennent en charge, en particulier celles qui ont été ajoutées à partir de hello « proposées » Hello [Galerie d’applications Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). toolearn en savoir plus sur la configuration de compte automatique d’utilisateurs et de son fonctionnement, consultez [tooSaaS automatiser l’approvisionnement des utilisateurs et Deprovisioning Applications avec Azure Active Directory](active-directory-saas-app-provisioning.md).

## <a name="finding-your-apps-in-hello-portal"></a>Recherche de vos applications dans le portail de hello
Toutes les applications qui sont configurées pour l’authentification unique dans un répertoire, par un administrateur d’annuaire à l’aide de hello [Galerie d’applications Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), peuvent être affichées et gérées dans hello [portail Azure](https://portal.azure.com). Vous trouverez les applications Hello Bonjour **plus Services** &gt; **des Applications d’entreprise** section du portail de hello. Les applications d’entreprise sont des applications qui sont déployées et utilisées au sein de votre organisation.

![Panneau Applications d’entreprise][0]

En sélectionnant hello **toutes les applications** lien sur hello gauche affiche une liste de toutes les applications qui ont été configurés, y compris les applications qui avaient été ajoutées à partir de la galerie de hello. La sélection d’une application charge panneau des ressources hello pour cette application, où les rapports peuvent être affichés pour cette application et divers paramètres peuvent être gérés.

Configuration des paramètres de compte d’utilisateur peut être géré en sélectionnant **Provisioning** sur hello gauche.

![Panneau de ressources d’application][1]

## <a name="provisioning-modes"></a>Modes d’approvisionnement
Hello **Provisioning** panneau commence par un **Mode** menu, qui affiche les modes de configuration sont pris en charge pour une application d’entreprise et leur permet de toobe configuré. les options disponibles Hello sont les suivantes :

* **Automatique** -cette option apparaît si Azure AD prend en charge la configuration automatique basée sur les API et/ou l’annulation du déploiement d’application toothis de comptes utilisateur. Ce mode affiche une interface qui guide les administrateurs dans la configuration des API de gestion de l’application Azure AD tooconnect toohello utilisateur, la création de mappages de compte et de flux de travail qui définissent le flux de données de compte d’utilisateur entre Azure AD et application Hello et la gestion des service de configuration d’Azure AD hello.
* **Manuel** -cette option ne s’affiche si Azure AD ne prend pas en charge la configuration automatique d’application toothis de comptes utilisateur. Cette option signifie que les enregistrements de compte d’utilisateur stockés dans une application hello doivent être gérés à l’aide d’un processus externe, en fonction de hello utilisateur gestion et configuration de fonctionnalités fournies par l’application (par exemple, l’approvisionnement juste à temps SAML).

## <a name="configuring-automatic-user-account-provisioning"></a>Configuration de l’approvisionnement automatique de comptes d’utilisateur
En sélectionnant hello **automatique** option affiche un écran est divisé en quatre sections :

### <a name="admin-credentials"></a>Admin Credentials (Informations d’identification de l’administrateur)
Il s’agit où les informations d’identification de hello requises pour l’API de gestion d’utilisateur de l’application Azure AD tooconnect toohello sont entrées. entrée Hello requise varie en fonction de l’application hello. toolearn sur les types d’informations d’identification hello et configuration requise pour des applications spécifiques, consultez hello [didacticiel de configuration pour cette application spécifique](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning).

En sélectionnant hello **tester la connexion** bouton permet de vous, les informations d’identification de hello tootest grâce à Azure AD essayez tooconnect toohello application d’approvisionnement d’application à l’aide des informations d’identification hello fourni.

### <a name="mappings"></a>Mappages
Il s’agit dans laquelle les administrateurs peuvent afficher et modifier le flux d’attributs utilisateur entre Azure AD et l’application cible hello lors de la mise en service ou de la mise à jour des comptes d’utilisateur.

Il existe un ensemble préconfiguré de mappages entre les objets utilisateur Azure AD et les objets utilisateur de chaque application SaaS. Certaines applications gèrent d’autres types d’objets, tels que des groupes ou des contacts. Sélectionnez une de ces mappages dans la table de hello montre éditeur de mappage de hello toohello droite, où elles peuvent être affichées et personnalisées.

![Panneau de ressources d’application][2]

Les personnalisations prises en charge sont notamment les suivantes :

* Activation et désactivation des mappages pour des objets spécifiques, tels que de l’objet utilisateur de l’application de hello Azure AD utilisateur objet toohello SaaS.
* Modifier les attributs de flux à partir de l’objet de l’application toohello hello Azure AD utilisateur objet utilisateur. Pour plus d’informations sur le mappage d’attributs, voir [Présentation des types de mappages d’attributs](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types).
* Hello filtre mise en service des actions réalisées par Azure AD sur hello cible l’application. Au lieu de Azure AD-synchroniser entièrement les objets, vous pouvez limiter les actions hello effectuées. Par exemple, si vous sélectionnez uniquement **Mettre à jour**, Azure AD met à jour les comptes d’utilisateur d’une application et n’en crée pas de nouveaux. Si vous sélectionnez uniquement **Créer**, Azure crée des comptes d’utilisateur, mais ne met pas à jour les comptes existants. Cette fonctionnalité permet à administrateurs toocreate des mappages différents pour le compte de flux de travail de création et la mise à jour.

### <a name="settings"></a>Paramètres
Cette section permet aux administrateurs toostart et stop hello service de configuration d’Azure AD pour l’application hello sélectionné, ainsi que l’approvisionnement hello désactivez éventuellement cache redémarrer le service de hello.

Si la mise en service est activé pour hello première fois pour une application, activer hello service en modifiant hello **état d’approvisionnement** trop**sur**. Alors hello Azure AD configuration service tooperform une synchronisation initiale, où il lit les utilisateurs hello affectés Bonjour **utilisateurs et groupes** section, interroge l’application cible de hello pour eux et qu’il exécute ensuite hello approvisionnement les actions définies dans hello Azure AD **mappages** section. Pendant ce processus, hello configuration service stocke les données mises en cache sur les comptes d’utilisateur qu’il gère, donc non managée des comptes dans hello cibler les applications qui ont été jamais dans l’étendue pour l’attribution ne sont pas affectés par les opérations de l’annulation du déploiement. Après hello la synchronisation initiale, hello configuration service automatiquement synchronise les objets utilisateur et groupe sur un intervalle de dix minutes.

Modification hello **état d’approvisionnement** trop**hors** simplement les pauses hello service d’approvisionnement. Dans cet état, Azure ne pas créer, mettre à jour ou supprimer des objets utilisateur ou groupe dans une application hello. Modification de tooon de hello état précédent provoque une toopick de service hello où elle s’était arrêtée.

En sélectionnant hello **effacer l’état en cours et redémarrez la synchronisation** case à cocher et l’enregistrement s’arrête hello service d’approvisionnement, vidages hello mis en cache sur les comptes Azure AD gère redémarre les services hello et effectue hello synchronisation initiale à nouveau. Cette option permet d’administrateurs toostart hello est mise en service du processus de déploiement de nouveau.

### <a name="synchronization-details"></a>Détails de la synchronisation
Cette section fournit des détails d’ajout sur opération hello Hello service de configuration, y compris les première et la dernière fois hello service d’approvisionnement hello exécuté sur application hello et le nombre d’objets utilisateur et de groupe est géré.

Des liens sont fournis toohello **mise en service de rapport d’activité**, qui fournit un journal de tous les utilisateurs et les groupes créés, mis à jour et supprimée entre Azure AD et application de cible hello et toohello **erreur de configuration rapport** qui fournit plus de messages d’erreur pour l’utilisateur et groupe qui a échoué toobe lire, créé, mis à jour ou supprimé des objets. 

##<a name="feedback"></a>Commentaires

Nous espérons que vous appréciez votre expérience Azure AD. Gardez les commentaires hello à venir ! Valider des idées pour améliorer et vos commentaires Bonjour **portail d’administration** section de notre [forum de commentaires](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Nous sommes très heureux sur la création de nouveautés tous les jours et utilisez votre tooshape des conseils et définir ce que nous créer ensuite.


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
