---
title: "contrôles de page de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les contrôles de page hello disponibles pour une utilisation dans les modèles de portail de développement de gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Contrôles de page Gestion des API Azure
Gestion des API Azure fournit hello suivant des contrôles utilisables dans les modèles de portail de développement hello.  
  
 toouse un contrôle, placez-le dans emplacement de hello souhaité dans le modèle de portail de développement hello. Certains contrôles, tels que hello [actions de l’application](#app-actions) , possèdent des paramètres, comme indiqué dans hello l’exemple suivant.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 valeurs Hello pour les paramètres de hello sont transmis comme partie du modèle de données hello pour le modèle de hello. Dans la plupart des cas, vous pouvez simplement Coller dans hello fournis exemple pour chaque contrôle toowork correctement. Pour plus d’informations sur les valeurs de paramètre hello, vous pouvez voir la section de modèle de données hello pour chaque modèle dans lequel un contrôle peut être utilisé.  
  
 Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Contrôles de page du modèle dans le portail des développeurs  
  
-   [app-actions](#app-actions)  
  
-   [basic-signin](#basic-signin)  
  
-   [paging-control](#paging-control)  
  
-   [fournisseurs](#providers)  
  
-   [search-control](#search-control)  
  
-   [sign-up](#sign-up)  
  
-   [subscribe-button](#subscribe-button)  
  
-   [subscription-cancel](#subscription-cancel)  
  
##  <a name="app-actions"></a> app-actions  
 Hello `app-actions` contrôle fournit une interface utilisateur permettant d’interagir avec des applications sur la page de profil utilisateur hello dans le portail des développeurs hello.  
  
 ![contrôle app-actions](./media/api-management-page-controls/APIM-app-actions-control.png "contrôle app-actions APIM")  
  
### <a name="usage"></a>Usage  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>parameters  
  
|Paramètre|Description|  
|---------------|-----------------|  
|appId|id de Hello de l’application hello.|  
  
### <a name="developer-portal-templates"></a>Modèles du portail des développeurs  
 Hello `app-actions` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.  
  
-   [Applications](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a> basic-signin  
 Hello `basic-signin` contrôle fournit un contrôle de page dans le portail des développeurs hello de connexion informations Bonjour de collecte connexion utilisateur.  
  
 ![contrôle basic-signin](./media/api-management-page-controls/APIM-basic-signin-control.png "contrôle basic-signin APIM")  
  
### <a name="usage"></a>Usage  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>parameters  
 Aucune.  
  
### <a name="developer-portal-templates"></a>Modèles du portail des développeurs  
 Hello `basic-signin` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.  
  
-   [Connexion](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> paging-control  
 Hello `paging-control` fournit la fonctionnalité de pagination sur développeur pages du portail qui affichent une liste d’éléments.  
  
 ![paging-control](./media/api-management-page-controls/APIM-paging-control.png "paging-control APIM")  
  
### <a name="usage"></a>Usage  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>parameters  
 Aucune.  
  
### <a name="developer-portal-templates"></a>Modèles du portail des développeurs  
 Hello `paging-control` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.  
  
-   [Liste d’API](api-management-api-templates.md#APIList)  
  
-   [Liste des problèmes](api-management-issue-templates.md#IssueList)  
  
-   [Liste de produits](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> providers  
 Hello `providers` contrôle fournit un contrôle pour la sélection des fournisseurs d’authentification dans la page dans le portail des développeurs hello de connexion hello.  
  
 ![contrôle providers](./media/api-management-page-controls/APIM-providers-control.png "contrôle providers APIM")  
  
### <a name="usage"></a>Usage  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>parameters  
 Aucune.  
  
### <a name="developer-portal-templates"></a>Modèles du portail des développeurs  
 Hello `providers` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.  
  
-   [Connexion](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> search-control  
 Hello `search-control` fournit des fonctionnalités de recherche sur développeur pages du portail qui affichent une liste d’éléments.  
  
 ![search-control](./media/api-management-page-controls/APIM-search-control.png "search-control APIM")  
  
### <a name="usage"></a>Usage  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>parameters  
 Aucune.  
  
### <a name="developer-portal-templates"></a>Modèles du portail des développeurs  
 Hello `search-control` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.  
  
-   [Liste d’API](api-management-api-templates.md#APIList)  
  
-   [Liste de produits](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> sign-up  
 Hello `sign-up` contrôle fournit un contrôle pour la collecte des informations de profil utilisateur dans la page dans le portail des développeurs hello d’inscription hello.  
  
 ![sign-up](./media/api-management-page-controls/APIM-sign-up-control.png "sign-up APIM")  
  
### <a name="usage"></a>Usage  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>parameters  
 Aucune.  
  
### <a name="developer-portal-templates"></a>Modèles du portail des développeurs  
 Hello `sign-up` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.  
  
-   [Inscription](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> subscribe-button  
 Hello `subscribe-button` fournit un contrôle pour s’abonner à un produit de tooa utilisateur.  
  
 ![contrôle subscribe-button](./media/api-management-page-controls/APIM-subscribe-button-control.png "contrôle subscribe-button APIM")  
  
### <a name="usage"></a>Usage  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>parameters  
 Aucune.  
  
### <a name="developer-portal-templates"></a>Modèles du portail des développeurs  
 Hello `subscribe-button` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.  
  
-   [Produit](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> subscription-cancel  
 Hello `subscription-cancel` contrôle fournit un contrôle pour l’annulation d’un produit de tooa d’abonnement dans la page de profil utilisateur hello dans le portail des développeurs hello.  
  
 ![contrôle subscription-cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "contrôle subscription-cancel APIM")  
  
### <a name="usage"></a>Usage  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>parameters  
  
|Paramètre|Description|  
|---------------|-----------------|  
|subscriptionId|id de Hello de hello abonnement toocancel.|  
|cancelUrl|Annuler l’abonnement de Hello URL.|  
  
### <a name="developer-portal-templates"></a>Modèles du portail des développeurs  
 Hello `subscription-cancel` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.  
  
-   [Produit](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).
