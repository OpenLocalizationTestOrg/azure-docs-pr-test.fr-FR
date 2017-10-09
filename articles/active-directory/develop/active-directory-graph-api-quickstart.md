---
title: aaaQuickstart pour hello API Azure AD Graph | Documents Microsoft
description: "Hello API Graph Azure Active Directory fournit un accès par programmation tooAzure AD via les points de terminaison API REST OData. Les applications peuvent utiliser hello API Graph tooperform créer, lire, mettre à jour et supprimer (CRUD) des opérations sur les objets et les données d’annuaire."
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Démarrage rapide pour hello API Azure AD Graph
Hello l’API Graph Azure Active Directory (AD) fournit un accès par programmation tooAzure AD via les points de terminaison API REST OData. Les applications peuvent utiliser hello API Graph tooperform créer, lire, mettre à jour et supprimer (CRUD) des opérations sur les objets et les données d’annuaire. Par exemple, vous pouvez utiliser hello API Graph toocreate un nouvel utilisateur, afficher ou mettre à jour les propriétés de l’utilisateur, modification du mot de passe, vérifier l’appartenance au groupe pour l’accès en fonction du rôle, désactiver ou supprimer l’utilisateur hello. Pour plus d’informations sur les fonctionnalités de l’API Graph hello et les scénarios d’application, consultez [API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) et [conditions préalables de Azure AD Graph API](https://msdn.microsoft.com/library/hh974476.aspx). 

> [!IMPORTANT]
> Nous vous recommandons fortement d’utiliser [Microsoft Graph](https://developer.microsoft.com/graph) au lieu de l’API Azure AD Graph tooaccess ressources Azure Active Directory. Nos efforts de développement sont maintenant axés sur Microsoft Graph et aucune autre amélioration n’est prévue pour l’API Azure AD Graph. Il existe un nombre très limité de scénarios pour lesquels API Azure AD Graph peut toujours être approprié ; Pour plus d’informations, consultez hello [Microsoft Graph ou hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) billet de blog Bonjour centre de développement Office.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>Comment tooconstruct une URL d’API Graph
Dans l’API Graph, les données d’annuaire tooaccess et les objets (en d’autres termes, les ressources ou les entités) dans laquelle vous souhaitez que tooperform les opérations CRUD, vous pouvez utiliser des URL basées sur hello protocole Open Data (OData). Hello URL utilisées dans l’API Graph se composent de quatre parties principales : racine, identificateur de locataire, chemin d’accès de ressource et options de chaîne de requête de service : `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`. Prenons l’exemple hello Hello suivant URL : `https://graph.windows.net/contoso.com/groups?api-version=1.6`.

* **Racine du service**: dans l’API Graph Azure AD, hello racine de service est toujours https://graph.windows.net.
* **Identificateur de client**: cette section peut être un nom de domaine (inscrit) vérifié, Bonjour précédent exemple, contoso.com. Il peut également être un client objet ID ou hello « myorganization » ou « me » alias. Pour plus d’informations, consultez [traitement des entités et opérations Bonjour API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **Chemin d’accès de la ressource**: cette section d’une URL identifie les ressources hello toobe possible d’interagir (utilisateurs, groupes, un utilisateur particulier, ou un groupe particulier, etc..) Dans l’exemple hello ci-dessus, il est tooaddress « groupes de niveau supérieur » hello ce jeu de ressources. Vous pouvez également adresser une entité spécifique, par exemple « users/{objectId} » ou « users/userPrincipalName ».
* **Paramètres de requête**: un point d’interrogation ( ?) sépare la section de chemin d’accès de ressource hello à partir de la section de paramètres de requête hello. paramètre de requête « api-version » Hello est requis sur toutes les demandes dans hello API Graph. Hello API Graph prend également en charge hello options de requête OData suivantes : **$filter**, **$orderby**, **$expand**, **$top**et **$format**. Hello, les options de requête suivantes n’est pas actuellement pris en charge : **$count**, **$inlinecount**, et **$skip**. Pour plus d'informations, consultez [Options de requêtes, de filtres et de pagination prises en charge dans l'API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options).

## <a name="graph-api-versions"></a>Versions d'API Graph
Vous spécifiez la version hello pour une demande d’API Graph dans le paramètre de requête « api-version » hello. Pour les versions 1.5 et ultérieures, utilisez une valeur numérique de version ; api-version=1.6. Pour les versions antérieures, vous utilisez une chaîne de date qui respecte le format toohello AAAA-MM-JJ ; par exemple, api-version = 2013-11-08. Pour les fonctionnalités en version préliminaire, utiliser le chaîne hello « beta » ; par exemple, api-version = beta. Pour plus d'informations sur les différences entre les versions de l'API Graph, consultez [Contrôle de version de l'API graphique Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

## <a name="graph-api-metadata"></a>Métadonnées d'API Graph
tooreturn hello fichier de métadonnées de l’API Graph, ajouter segment de hello « $metadata » après l’identificateur hello du locataire dans hello URL. par exemple, hello suivant retourne les métadonnées d’URL pour une société de démonstration : `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`. Vous pouvez entrer cette URL dans barre d’adresses hello de métadonnées hello de toosee du navigateur web. Hello document de métadonnées CSDL renvoyé décrit les entités hello types complexes, propriétés et hello et leurs actions exposées par la version de hello de API Graph demandée. L’omission du paramètre api-version de hello retourne les métadonnées pour la version la plus récente hello.

## <a name="common-queries"></a>Requêtes courantes
[Requêtes Azure AD Graph API courantes](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) répertorie des requêtes courantes qui peuvent être utilisés avec hello Azure AD Graph, y compris les requêtes qui peuvent être des ressources de niveau supérieur tooaccess utilisés dans vos opérations tooperform active et des requêtes dans votre annuaire.

Par exemple, `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` renvoie des informations sur la société pour l'annuaire contoso.com.

Ou `https://graph.windows.net/contoso.com/users?api-version=1.6` répertorie tous les objets utilisateur hello directory contoso.com.

## <a name="using-hello-graph-explorer"></a>À l’aide de hello Explorateur graphique
Vous pouvez utiliser hello Explorateur graphique pour les données d’annuaire Azure AD Graph API tooquery hello de hello lorsque vous générez votre application.

Hello Voici hello sortie serait voir si vous étiez toonavigate toohello Graph Explorer, connectez-vous, puis entrez `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` toodisplay tous hello utilisateurs hello active de l’utilisateur connecté :

![explorateur api graph Azure AD](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**Hello de charge Explorateur graphique**: hello de tooload outil, accédez trop[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/). Cliquez sur **connexion** et connectez-vous avec votre toorun d’informations d’identification de compte Azure AD hello Explorateur graphique sur votre client. Si vous exécutez l’Explorateur graphique sur votre propre client, vous ou votre administrateur doit tooconsent pendant la connexion. Si vous avez un abonnement à Office 365, vous disposez automatiquement d’un client Azure AD. Hello informations d’identification vous toosign dans tooOffice 365 sont, en fait, les comptes Azure AD et que vous pouvez utiliser ces informations d’identification avec l’Explorateur graphique.

**Exécuter une requête**: toorun une requête, tapez votre requête dans la zone de texte de requête hello et cliquez sur **obtenir** ou cliquez sur hello **entrez** clé. résultats de Hello sont affichés dans la zone de réponse hello. Par exemple, `https://graph.windows.net/myorganization/groups?api-version=1.6` répertorie tous les objets de groupe dans le répertoire de hello signé de l’utilisateur.

Hello de note suivant les fonctionnalités et les limitations de hello Explorateur graphique :

* Fonctionnalité de saisie semi-automatique sur des jeux de ressources. toosee cette fonctionnalité, cliquez sur hello demander la zone de texte (où apparaît le hello URL de l’entreprise). Vous pouvez sélectionner une ressource définie à partir de la liste déroulante de hello.
* Prend en charge hello « me » et « myorganization » alias d’adressage. Par exemple, vous pouvez utiliser `https://graph.windows.net/me?api-version=1.6` objet user tooreturn hello utilisateur connecté hello ou `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn tous les utilisateurs dans le répertoire en cours de hello.
* Section d’en-tête de réponse. Cette section peut servir toohelp résoudre les problèmes qui se produisent lors de l’exécution des requêtes.
* Une visionneuse JSON pour la réponse hello avec les fonctionnalités de développement et de réduction.
* Aucune prise en charge de l'affichage d'une photo miniature.

## <a name="using-fiddler-toowrite-toohello-directory"></a>À l’aide du répertoire de Fiddler toowrite toohello
Pour des raisons de hello de ce guide de démarrage rapide, vous pouvez utiliser toopractice de débogueur Web Fiddler hello effectuant '' les opérations d’écriture par rapport à votre annuaire Azure AD. Pour plus d’informations et tooinstall Fiddler, consultez [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler).

Dans l’exemple hello ci-dessous, vous utilisez le débogueur Web Fiddler toocreate un nouveau groupe de sécurité « MyTestGroup » dans votre annuaire Azure AD.

**Obtenir un jeton d’accès**: tooaccess Azure AD Graph, les clients sont requis toosuccessfully authentifier tooAzure AD tout d’abord. Pour plus d’informations, consultez la page [Scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md).

**Composer et exécuter une requête**: hello complète comme suit :

1. Ouvrez le débogueur Web Fiddler et basculez toohello **Composer** onglet.
2. Étant donné que vous souhaitez toocreate un nouveau groupe de sécurité, sélectionnez **Post** comme hello méthode HTTP à partir du menu déroulant de hello. Pour plus d’informations sur les opérations et les autorisations sur un objet de groupe, consultez [groupe](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) dans hello [référence d’API REST Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
3. Bonjour champ ensuite trop**Post**, type suivant de hello hello URL de demande : `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`.
   
   > [!NOTE]
   > Vous devez remplacer mytenantdomain par le nom de domaine hello de votre propre annuaire Azure AD.
   > 
   > 
4. Dans le champ hello directement sous déroulant publier, tapez hello qui suit :
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > Remplacez votre &lt;votre jeton d’accès&gt; avec un jeton d’accès hello pour votre annuaire Azure AD.
   > 
   > 
5. Bonjour **corps de la demande** champ, tapez hello qui suit :
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    Pour plus d'informations sur la création de groupes, consultez [Création d’un groupe](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup).

Pour plus d’informations sur les entités Azure AD et les types qui sont exposés par Graph et des informations sur les opérations hello qui peuvent être effectuées sur ceux-ci avec Graph, consultez [référence d’API REST Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur hello [API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* En savoir plus sur les [Étendues d’autorisation de l’API Graph Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

