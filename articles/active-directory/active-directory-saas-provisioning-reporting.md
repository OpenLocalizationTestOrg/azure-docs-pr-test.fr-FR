---
title: "Création de rapports sur le compte d’utilisateur automatique de Azure Active Directory mise en service des applications de tooSaaS | Documents Microsoft"
description: "Découvrez comment toocheck hello état des travaux d’approvisionnement de compte automatique de l’utilisateur et tootroubleshoot hello l’approvisionnement des utilisateurs individuels."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>Didacticiel : Création de rapports sur l’approvisionnement automatique de comptes d’utilisateur


Azure Active Directory comprend un [compte d’utilisateur de service de configuration](active-directory-saas-app-provisioning.md) qui permet d’automatiser hello approvisionnement mise hors service des comptes d’utilisateur dans les applications SaaS et d’autres systèmes, à des fins de hello du cycle de vie des identités de bout en bout gestion. Azure AD prend en charge utilisateur pré-intégrées configuration des connecteurs pour toutes les applications de hello et des systèmes dans la section « A » de hello Hello [Galerie d’applications Azure AD](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).

Cet article décrit comment état de hello toocheck de l’approvisionnement des travaux après qu’ils ont été définies et le tootroubleshoot hello l’approvisionnement des utilisateurs individuels et des groupes.

## <a name="overview"></a>Vue d'ensemble

Configuration des connecteurs sont principalement définis et configurés à l’aide de hello [portail de gestion Azure](https://portal.azure.com), par hello suivant [a fourni la documentation](active-directory-saas-tutorial-list.md) pour l’application hello où l’utilisateur compte approvisionnement est souhaitée. Une fois configurés et opérationnels, les travaux d’approvisionnement pour une application peuvent faire l’objet de rapports créés à l’aide de l’une des deux méthodes suivantes :

* **Portail de gestion Azure** -cet article décrit principalement la récupération des informations de rapport hello [portail de gestion Azure](https://portal.azure.com), qui fournit à la fois un rapport de synthèse de configuration, ainsi que de configuration détaillées l’audit des journaux pour une application donnée.

* **API de l’audit** -Azure Active Directory fournit également un API qui permet la récupération par programmation des hello détaillées de configuration d’audit des journaux d’Audit. Consultez [l’audit Azure Active Directory référence de l’API](active-directory-reporting-api-audit-reference.md) pour toousing spécifique de documentation cette API. Alors que cet article ne couvre pas spécifiquement comment toouse hello API, il détaille les types hello d’événements qui sont enregistrés dans le journal d’audit de hello de configuration.

### <a name="definitions"></a>Définitions

Cet article utilise hello suivant les termes du contrat, défini ci-dessous :

* **Système source** -référentiel hello d’utilisateurs qui hello du service de configuration d’Azure AD se synchronise à partir de. Azure Active Directory est le système source de hello pour majorité hello de pré-intégrées configuration des connecteurs, cependant, il existe quelques exceptions près (exemple : synchronisation de trafic entrant de Workday).

* **Système cible** -référentiel hello d’utilisateurs qui hello du service de configuration d’Azure AD se synchronise sur. Il s’agit généralement d’une application SaaS (exemples : Salesforce, ServiceNow, Google Apps, Dropbox for Business), mais dans certains cas peut être un système local, tel qu’Active Directory (exemple : synchronisation de trafic entrant de Workday tooActive active).


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>Mise en route de la configuration des rapports à partir du portail de gestion Azure hello

tooget mise en service des informations d’état pour une application donnée, commencez par lancer hello [portail de gestion Azure](https://portal.azure.com) et Application d’entreprise toohello pour lequel l’option de configuration est configurée de navigation. Par exemple, si vous configurez des utilisateurs tooLinkedIn élever, détails de l’application hello navigation chemin d’accès toohello est :

**Azure Active Directory &gt; Applications d’entreprise &gt; Toutes les applications &gt; LinkedIn Elevate**

À ce stade, vous pouvez accéder à la fois rapport de synthèse de provisionnement hello et journaux d’audit de la configuration hello, deux décrites ci-dessous.


### <a name="provisioning-summary-report"></a>Rapport de synthèse sur l’approvisionnement

Hello rapport Résumé de configuration est visible dans hello **Provisioning** pour l’onglet compte tenu de l’application. Il se trouve dans la section des détails de synchronisation hello sous **paramètres**et fournit hello informations suivantes :

* Hello nombre total d’utilisateurs et groupes qui ont été synchronisées et sont actuellement dans la portée pour la configuration entre hello source et système cible de hello.

* Hello dernière hello synchronisation a été exécutée. Les synchronisations se produisent généralement toutes les 20 à 40 minutes après l’achèvement d’une synchronisation complète.

* Indique si une synchronisation initiale complète a été effectuée.

* Ou non hello processus de déploiement a été placé en quarantaine, et quelle raison hello pour l’état de mise en quarantaine hello est par exemple, (toocommunicate échec avec le système cible en raison d’informations d’identification d’administrateur de tooinvalid)

Hello rapport Résumé de configuration doit être hello première place administrateurs aspect toocheck sur le bon fonctionnement de la tâche d’approvisionnement hello hello.

 ![Rapport de synthèse](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>Journaux d’audit de l’approvisionnement
Toutes les activités effectuées par hello configuration de service sont enregistrées dans les journaux d’audit hello Azure AD, qui peuvent être consultées dans hello **journaux d’Audit** onglet sous hello **l’approvisionnement de comptes** catégorie. Les types d’événements d’activité journalisés sont les suivants :

* **Importer des événements** -un événement « importation » est enregistré chaque fois que service d’approvisionnement hello AD Azure récupère des informations sur un utilisateur ou un groupe à partir d’un système source ou le système cible. Pendant la synchronisation, les utilisateurs sont récupérés à partir du système source de hello de tout d’abord, avec résultats hello enregistrés en tant que « importer » des événements. Hello correspondance d’ID d’utilisateurs de hello récupéré est ensuite interrogée sur hello cible système toocheck s’ils existent, avec les résultats hello également enregistrés comme « importer » des événements. Ces événements enregistrent tous les attributs utilisateur mappés et leurs valeurs qui ont été vu par le service d’approvisionnement hello Azure AD au moment de hello d’événement de hello. 

* **Événements de règle de synchronisation** - ces événements de rapports sur les résultats des règles de mappage d’attribut hello hello et les filtres d’étendue, configuré les données utilisateur a été importées et évaluées à partir des systèmes source et cible de hello. Par exemple, si un utilisateur dans un système source est considéré comme toobe dans l’étendue de l’approvisionnement et toonot présumé existe dans le système cible de hello, cet événement rapporte qu’hello utilisateur configuré dans le système cible de hello. 

* **Exporter les événements** -un événement « export » est enregistré chaque fois que service d’approvisionnement hello AD Azure écrit un utilisateur au compte ou groupe objet tooa système cible. Ces événements enregistrent tous les attributs d’utilisateur et leurs valeurs qui ont été écrits par hello service de configuration d’Azure AD au moment de hello d’événement de hello. Si une erreur s’est produite lors de l’écriture hello utilisateur compte ou groupe objet toohello système cible, il sera affiché ici.

* **Traiter les événements de tiers de confiance** -vendus avec le processus se produisent lorsque hello configuration service rencontre un échec lors de la tentative d’une opération et commence tooretry opération de hello sur un intervalle de temporisation de temps. Un événement escrow est enregistré à chaque abandon d’une opération d’approvisionnement.

Lorsque vous examinez les événements de configuration pour un utilisateur individuel, hello normalement se produisent dans cet ordre :

1. Événement d’importation : utilisateur est récupéré à partir du système source de hello.

2. Événement d’importation : système cible est interrogé toocheck existence hello de hello récupérée utilisateur.

3. Événement de règle de synchronisation : les données utilisateur à partir des systèmes source et cible sont évaluées par rapport à l’attribut hello configuré des règles de mappage et la portée à toodetermine de filtres d’action, le cas échéant, doit être effectuée.

4. Exporter l’événement : si l’événement de règle de synchronisation hello stipulé qu’une action doit être effectuée (par exemple, ajout, mise à jour, suppression), puis les résultats hello d’action de hello sont enregistrés dans un événement d’exportation.

![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>Recherche d’événements d’approvisionnement pour un utilisateur spécifique

Hello principaux cas d’utilisation de hello configuration des journaux d’audit est hello toocheck état d’un compte d’utilisateur de la configuration. toolook des événements de configuration dernière hello pour un utilisateur spécifique :

1. Accédez toohello **journaux d’Audit** section.

2. À partir de hello **catégorie** menu, sélectionnez **l’approvisionnement de comptes**.

3. Bonjour **plage de dates** menu, sélectionnez hello plage de dates toosearch,

4. Bonjour **recherche** barre, entrez les ID d’utilisateur hello d’utilisateur hello toosearch pour. format Hello de valeur d’ID doit correspondre à tout ce que vous avez sélectionné comme hello principal ID correspondant dans la configuration de mappage d’attribut hello (par exemple, userPrincipalName ou employé numéro d’ID). valeur d’ID Hello requis seront visible dans la colonne cible (s) de hello.

5. Appuyez sur entrée toosearch. tout d’abord Hello plus récente d’événements de configuration sera retourné.

6. Si les événements sont retournés, notez les types d’activité hello et ils a réussi ou a échoué. Si aucun résultat n’est renvoyé, cela signifie hello utilisateur n’existe pas ou n’a pas été détecté par hello processus de déploiement si une synchronisation complète n’est pas encore terminée.

7. Cliquez sur les différents événements tooview étendu plus d’informations, y compris toutes les propriétés d’utilisateur qui ont été récupérées, évaluées ou écriture dans le cadre de l’événement de hello.


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>Conseils pour l’affichage de l’approvisionnement hello les journaux d’audit

Pour une meilleure lisibilité meilleures Bonjour portail Azure, sélectionnez hello **colonnes** bouton et sélectionnez ces colonnes :

* **Date** -montre hello date hello événement s’est produit.
* **Cible (s)** -montre hello app Nom et l’ID utilisateur qui sont sujets hello d’événement de hello.
* **Activité** -hello type d’activité, comme décrit précédemment.
* **État** : indique si l’événement de hello a réussi ou non.
* **Raison de l’état** -un résumé des événements survenus dans hello événements de configuration.


## <a name="troubleshooting"></a>Résolution des problèmes

Hello approvisionnement résumé des journaux d’audit et de rapport joue un rôle de clé aidant les administrateurs à résoudre les problèmes de configuration de compte d’utilisateur différents.

Pour obtenir une aide basée sur un scénario sur la façon de tootroubleshoot automatique configuration de l’utilisateur, consultez [des problèmes de configuration et l’approvisionnement des utilisateurs tooan application](active-directory-application-provisioning-content-map.md).


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-enterprise-apps-manage-provisioning.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
