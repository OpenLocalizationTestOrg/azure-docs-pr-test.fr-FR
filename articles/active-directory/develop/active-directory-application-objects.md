---
title: aaaAzure Active Directory Application et les objets de Principal du Service | Documents Microsoft
description: "Une description de relation hello entre l’application et les objets principal du service dans Azure Active Directory"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Objets application et principal du service dans Azure Active Directory (Azure AD)
Parfois hello signification du terme hello « application » peut être mal comprise lorsqu’il est utilisé dans le contexte de hello d’Azure AD. Hello cet article vise toomake il plus claire, en clarifiant les aspects conceptuelles et concrètes d’intégration d’application Azure AD, avec une illustration de l’inscription et de consentement pour un [application mutualisée](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Vue d'ensemble
Une application qui a été intégrée à Azure AD a des implications qui vont au-delà des aspects du logiciel hello. « Application » est fréquemment utilisée comme un terme conceptuel, qui fait référence toonot uniquement hello hello logiciel d’application, mais également son inscription à Azure AD et un rôle dans l’authentification/autorisation « conversations » lors de l’exécution. Par définition, une application peut fonctionner dans un [client](active-directory-dev-glossary.md#client-application) rôle (utilise une ressource), un [serveur de ressources](active-directory-dev-glossary.md#resource-server) rôle (exposition API tooclients), ou même les deux. protocole de conversation Hello est définie par une [flux d’octroi d’autorisation OAuth 2.0](active-directory-dev-glossary.md#authorization-grant), autorisant hello/ressource client tooaccess/protéger les données d’une ressource respectivement. Passons maintenant un niveau plus profond et voir comment le modèle d’application hello Azure AD représente une application au moment de la conception et d’exécution. 

## <a name="application-registration"></a>Inscription de l’application
Lorsque vous inscrivez une application Azure AD Bonjour [portail Azure][AZURE-Portal], deux objets sont créés dans votre locataire Azure AD : un objet application et un objet principal de service.

#### <a name="application-object"></a>Objet application
Une application Azure AD est définie par son seul et application unique objet, qui réside dans le locataire Azure AD de hello où l’application hello a été enregistrée, connu en tant que locataire « home » de l’application hello. Bonjour Azure AD Graph [entité d’Application] [ AAD-Graph-App-Entity] définit le schéma de hello pour les propriétés d’un objet application. 

#### <a name="service-principal-object"></a>Objet principal du service
objet principal de service Hello définit la stratégie de hello et les autorisations d’accès d’une application dans un client spécifique, en fournissant de la base de hello pour une application de hello de toorepresent principal de sécurité au moment de l’exécution. Bonjour Azure AD Graph [entité ServicePrincipal] [ AAD-Graph-Sp-Entity] définit le schéma de hello pour les propriétés d’un objet principal service. 

#### <a name="application-and-service-principal-relationship"></a>Relation entre l’application et le principal de service
Envisagez d’objet d’application hello comme hello *global* la représentation sous forme de votre application pour une utilisation sur tous les locataires et de principal du service hello comme hello *local* représentation pour une utilisation dans un spécifique client. Hello objet application sert hello modèle à partir de quels commun et les propriétés par défaut sont *dérivée* à utiliser pour créer des objets de principal de service correspondants. Par conséquent, un objet d’application a une relation 1:1 avec application hello et une relation 1:many avec ses objets de principal de service correspondant.

Un principal de service doit être créé dans chaque locataire où l’application hello est utilisée, ce qui lui tooestablish une identité pour la connexion et/ou tooresources accès sécurisé par le client hello. Une application à locataire unique n’a qu’un seul principal de service (dans son locataire de base), généralement créé et pouvant être utilisé pendant l’inscription de l’application. Une application Web de plusieurs locataire/API aura également un principal de service créé à chaque client sur lequel un utilisateur à partir de ce client a consenti tooits utilisation.  

> [!NOTE]
> Les modifications que vous apportez tooyour objet d’application, sont également répercutées dans son objet principal de service dans accueil client l’application hello uniquement (locataire hello dans laquelle il a été enregistré). Pour les applications mutualisées, objet d’application de modifications toohello ne sont pas répercutées dans les objets principaux de service aux clients tout consommateur, jusqu'à ce que l’accès hello est supprimé via hello [volet d’accès Application](https://myapps.microsoft.com) et accordées à nouveau.
><br>  
> Notez également que les applications natives sont enregistrées en tant que mutualisées par défaut.
> 
> 

## <a name="example"></a>Exemple
Hello diagramme suivant illustre la relation hello entre l’objet d’application et le service correspondant objets principal, dans le contexte de hello d’un exemple d’application mutualisée appelées d’une application **application RH**. Il existe trois clients Azure AD dans ce scénario : 

* **Adatum** - hello client utilisé par des sociétés hello développement hello **application RH**
* **Contoso** - hello client utilisé par hello organisation Contoso, qui est un consommateur de hello **application RH**
* **Fabrikam** - hello client utilisé par hello organisation Fabrikam, ce qui consomme également hello **application RH**

![Relation entre un objet application et un objet principal du service](./media/active-directory-application-objects/application-objects-relationship.png)

Dans le diagramme précédent de hello, étape 1 consiste hello créer des application hello et objets de principal de service client de base de l’application hello.

À l’étape 2, issue de l’accord, les administrateurs de Contoso et Fabrikam un objet principal de service est créé dans le locataire Azure AD de leur société et les autorisations affectées hello qu’administrateur hello accordé. Notez également que cette application hello RH peut être configuré/conçu de tooallow consentement des utilisateurs individuels.

À l’étape 3, hello consommateur de hello application RH (Contoso et Fabrikam) chaque doté de son propre objet principal de service. Chacun représente leur utilisation d’une instance de l’application hello lors de l’exécution, régie par hello autorisations consenties par un administrateur respectifs de hello.

## <a name="next-steps"></a>Étapes suivantes
Objet d’application d’une application est accessible via hello API Azure AD Graph, hello [du portail Azure] [ AZURE-Portal] éditeur de manifeste d’application, ou [applets de commande PowerShell Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), comme représenté par son OData [entité d’Application][AAD-Graph-App-Entity].

Objet principal de service d’une application est accessible via hello API Azure AD Graph ou [applets de commande PowerShell Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), comme représenté par son OData [entité ServicePrincipal] [ AAD-Graph-Sp-Entity].

Hello [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) est utile pour l’interrogation application hello et objets principal du service.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
