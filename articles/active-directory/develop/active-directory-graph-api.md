---
title: aaaAzure Active Directory Graph API | Documents Microsoft
description: "Un guide de présentation et de démarrage rapide pour hello API graphique qui permet la programmation d’accès tooAzure AD via les points de terminaison API REST."
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>API Graph Azure Active Directory
> [!IMPORTANT]
> Nous vous recommandons fortement d’utiliser [Microsoft Graph](https://graph.microsoft.io/) au lieu de l’API Azure AD Graph tooaccess ressources Azure Active Directory. Nos efforts de développement sont maintenant axés sur Microsoft Graph et aucune autre amélioration n’est prévue pour l’API Azure AD Graph. Il existe un nombre très limité de scénarios pour lesquels API Azure AD Graph peut toujours être approprié ; Pour plus d’informations, consultez hello [Microsoft Graph ou hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) billet de blog Bonjour centre de développement Office.
> 
> 

Hello API Graph Azure Active Directory fournit un accès par programmation tooAzure AD via les points de terminaison API REST. Les applications peuvent utiliser hello API Graph tooperform créer, lire, mettre à jour et supprimer (CRUD) des opérations sur les objets et les données d’annuaire. Par exemple, hello API Graph prend en charge hello suit les opérations courantes pour un objet utilisateur :

* Création d’un nouvel utilisateur dans un répertoire
* Obtention des propriétés détaillées d’un utilisateur, par exemple ses groupes
* Mise à jour des propriétés d’un utilisateur, par exemple son emplacement et son numéro de téléphone, ou modification de son mot de passe
* Vérification de l’appartenance de l’utilisateur au groupe pour les accès basés sur les rôles
* Désactivation ou suppression totale d’un compte d’utilisateur

Dans les objets de toouser de plus, vous pouvez effectuer des opérations similaires sur d’autres objets tels que des groupes et des applications. hello toocall API Graph dans un répertoire, une application hello doit être inscrit auprès d’Azure AD et être configuré tooallow accès toohello directory. Cette autorisation fait généralement l’objet d’un consentement de la part de l’utilisateur ou de l’administrateur.

à l’aide de toobegin hello API Azure Active Directory Graph, consultez hello [Guide de démarrage rapide d’API Graph](active-directory-graph-api-quickstart.md), ou vue hello [interactive documentation de référence de l’API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="features"></a>Caractéristiques
Hello API Graph fournit hello suivant de fonctionnalités :

* **Points de terminaison REST API**: hello API Graph est un service RESTful constitué de points de terminaison qui sont accessibles à l’aide de demandes HTTP standard. Hello API Graph prend en charge les types de contenu XML ou Javascript Objet Notation (JSON) pour les demandes et réponses. Pour plus d'informations, consultez [Informations de référence sur l'API REST Graph Azure AD (en anglais)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **L’authentification auprès d’Azure AD**: chaque toohello demande API Graph doit être authentifiée en ajoutant un JSON Web Token (JWT) dans l’en-tête d’autorisation de hello de demande de hello. Ce jeton est obtenu en effectuant un tooAzure demande l’annonce de point de terminaison token fournissant des informations d’identification valides. Vous pouvez utiliser des flux d’informations d’identification client OAuth 2.0 de hello ou un graphique de hello jeton toocall tooacquire de flux d’octroi de code d’autorisation de hello. Pour plus d’informations, consultez [OAuth 2.0 dans Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Autorisation basée sur les rôles (RBAC)**: groupes de sécurité sont utilisé tooperform RBAC Bonjour API Graph. Par exemple, si vous souhaitez toodetermine si l’utilisateur dispose des ressources spécifiques de l’accès tooa, application hello peut appeler hello [vérifier l’appartenance aux groupes (opération transitive)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) opération, qui retourne true ou false.
* **Requête différentielle**: Si vous souhaitez toocheck pour les modifications dans un répertoire entre deux périodes de temps sans avoir toomake fréquentent requêtes toohello API Graph, vous pouvez effectuer une demande de requête différentielle. Ce type de requête retournent uniquement hello les modifications apportées entre la demande de requête différentielle précédente hello et hello actuel. Pour plus d'informations, consultez [Requête différentielle de l'API Graph Azure AD (en anglais)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Extensions d’annuaire**: Si vous développez une application nécessitant des propriétés uniques tooread ou d’écriture pour les objets d’annuaire, vous pouvez inscrire et utiliser des valeurs d’extension à l’aide de l’API Graph de hello. Par exemple, si votre application nécessite une propriété ID de Skype pour chaque utilisateur, vous pouvez enregistrer la nouvelle propriété de hello dans le répertoire de hello et il sera disponible sur tous les objets utilisateur. Pour plus d'informations, consultez [Extensions de schéma d'annuaire de l'API Graph Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **Sécurisés par des étendues d’autorisation**: l’API Graph AAD expose les étendues d’autorisation qui permet aux données de tooAAD consenti/de sécuriser l’accès et prennent en charge divers types d’applications clientes, y compris :
  
  * ceux avec une interface utilisateur qui sont fonction de délégué accéder toodata via l’autorisation à partir de hello utilisateur connecté (délégué)
  * celles qui utilisent un contrôle d'accès basé sur les rôles et défini par l’application, notamment les clients service/daemon (rôles d'application)
    
    Les deux délégués et les étendues d’autorisation de rôle application représentent un privilège exposé par l’API Graph de hello et peuvent être demandées par les applications clientes via les autorisations d’inscription d’application [fonctionnalités Bonjour Azure portal](https://portal.azure.com). Les clients puissent vérifier étendues d’autorisation hello accordé toothem en inspectant la revendication d’étendue (« scp ») de salutation reçue dans le jeton d’accès hello pour les autorisations déléguées et rôles de hello (« rôles ») de revendication pour les autorisations de rôle d’application. En savoir plus sur les [Étendues d'autorisation de l’API Graph Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).

## <a name="scenarios"></a>Scénarios
Hello API Graph permet de nombreux scénarios d’application. Hello les scénarios suivants est hello courants :

* **Application métier (à un seul client)** : dans ce scénario, un développeur d’entreprise travaille pour une organisation qui possède un abonnement Office 365. Hello développeur crée une application web qui interagit avec les tâches de tooperform Azure AD par attribution à un utilisateur tooa de licence. Cette tâche nécessite l’accès toohello API Graph, le développeur de hello inscrit l’application à locataire unique hello dans Azure AD et configure les autorisations Lire et écrire pour hello API Graph. Puis hello application est configurée toouse ses propres informations d’identification ou celles de hello actuellement dans l’authentification utilisateur tooacquire un jeton toocall hello API Graph.
* **Application Software as a Service (architecture mutualisée)** : dans ce scénario, un éditeur de logiciels indépendant (ISV) développe une application web mutualisée hébergée qui fournit des fonctionnalités de gestion utilisateur à d’autres organisations qui utilisent Azure AD. Ces fonctionnalités nécessitent l’accès toodirectory objets et application hello doit donc toocall hello API Graph. développeur de Hello inscrit l’application hello dans Azure AD, configure toorequire lecture et accès en écriture pour hello API Graph, puis active l’accès externe afin que d’autres organisations puissent consentir application hello de toouse dans leur annuaire. Lorsqu’un utilisateur d’une autre organisation s’authentifie application toohello pour hello première fois, une boîte de dialogue de consentement avec des autorisations hello demande l’application hello sont affichées.  Octroi de consentement appliquera application hello celles demandées autorisations toohello API Graph dans le répertoire de l’utilisateur hello. Pour plus d’informations sur l’infrastructure de consentement hello, consultez [vue d’ensemble de l’infrastructure de consentement de hello](active-directory-integrating-applications.md).

## <a name="see-also"></a>Voir aussi
[Guide de démarrage rapide pour l’API Graph Azure AD](active-directory-graph-api-quickstart.md)

[Documentation REST Graph AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Guide du développeur Azure Active Directory](active-directory-developers-guide.md)

