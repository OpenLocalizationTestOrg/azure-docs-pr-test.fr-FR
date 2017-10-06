---
title: aaaTroubleshoot Analytique dans Azure Application Insights | Documents Microsoft
description: "Des problèmes avec Application Insights Analytics ? Démarrer ici. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Dépannage d’Analytics dans Application Insights
Des problèmes avec [Application Insights Analytics](app-insights-analytics.md)? Démarrer ici. Analytique est un outil puissant hello d’aperçus d’Application Azure.

## <a name="limits"></a>limites
* À l’heure actuelle, ses résultats sont limité toojust plus d’une semaine de données passées.
* Navigateurs que nous testons : dernières versions d’Internet Explorer, Chrome et Edge.

## <a name="known-incompatible-browser-extensions"></a>Extensions du navigateur incompatibles connues
* Ghostery

Désactivation de l’extension de hello ou utilisez un navigateur différent.

## <a name="e-a"></a> « Erreur inattendue »
![Ecran Erreur inattendue](./media/app-insights-analytics-troubleshooting/010.png)

Une erreur interne s’est produite lors de l’exécution du portail : exception non gérée.

* Nettoyer la mémoire cache du navigateur hello. 

## <a name="e-b"></a>403... Veuillez essayer tooreload
![403... Veuillez essayer tooreload](./media/app-insights-analytics-troubleshooting/020.png)

Une erreur d’authentification s’est produite (lors de l’authentification ou pendant la génération du jeton d’accès). portail de Hello ne peut avoir aucun moyen de récupérer trop sans modifier les paramètres du navigateur.

* Vérifiez [les cookies tiers sont activés](#cookies) dans le navigateur de hello. 

## <a name="authentication"></a>403... vérifiez la zone de sécurité
![403... vérifiez la zone de sécurité](./media/app-insights-analytics-troubleshooting/030.png)

Une erreur d’authentification s’est produite (lors de l’authentification ou pendant la génération du jeton d’accès). portail de Hello ne peut avoir aucun moyen de récupérer trop sans modifier les paramètres du navigateur.

1. Vérifiez [les cookies tiers sont activés](#cookies) dans le navigateur de hello. 
2. Vous avez peut-être utilisé un favori, un signet ou un lien enregistré tooopen hello Analytique portail ? Si vous êtes connecté avec différentes informations d’identification que vous avez utilisé lorsque vous avez enregistré le lien de hello ?
3. Essayez d’utiliser une fenêtre de navigateur privée/anonyme (après avoir fermé toutes les fenêtres de ce type). Vous avez tooprovide vos informations d’identification. 
4. Ouvrir une autre fenêtre de navigateur (ordinaire) et accédez trop[Azure](https://portal.azure.com). Déconnectez-vous. Ouvrez votre lien, puis connectez-vous avec les informations d’identification correctes hello.
5. Les utilisateurs Edge et Internet Explorer peuvent également obtenir cette erreur lorsque les paramètres de la zone de confiance ne sont pas pris en charge.
   
    Vérifiez que les deux [portal d’Analytique](https://analytics.applicationinsights.io) et [portail Azure Active Directory](https://portal.azure.com) sont Bonjour même zone de sécurité :
   
   * Dans Internet Explorer, ouvrez **Options Internet**, **Sécurité**, **Sites de confiance**, **Sites** :
     
     ![Boîte de dialogue Options Internet, ajout d’un site tooTrusted Sites](./media/app-insights-analytics-troubleshooting/033.png)
     
     Dans la liste de sites Web hello, si un des hello URL suivantes sont inclus, assurez-vous que hello d’autres sont également inclus :
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Ressource introuvable
![404... ressource introuvable](./media/app-insights-analytics-troubleshooting/040.png)

Une ressource d’application a été supprimée d’Application Insights et n’est plus disponible. Cela peut se produire si vous avez enregistré la page de hello URL toohello Analytique.

## <a name="e-e"></a>403 ... Aucune autorisation
![403... non autorisé](./media/app-insights-analytics-troubleshooting/050.png)

Vous n’avez tooopen d’autorisation de cette application dans Analytique.

* Vous avez reçu hello lien à partir d’une autre personne ? Demandez-lui toomake que vous êtes dans hello [lecteurs ou les collaborateurs pour ce groupe de ressources](app-insights-resources-roles-access-control.md).
* Avez-vous enregistré lien hello à l’aide des informations d’identification différentes ? Ouvrez hello [portail Azure](https://portal.azure.com), déconnectez-vous, puis essayez à nouveau, ce lien fournissant les informations d’identification correctes hello.

## <a name="html-storage"></a>403 ... Stockage HTML5
Notre portail utilise HTML5 localStorage et sessionStorage.

* Chrome : Paramètres, Confidentialité, Paramètres de content.
* Internet Explorer : Options Internet, onglet Avancé, Sécurité, Activer le stockage DOM

![403... Essayez tooenable HTML5 stockage](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Abonnement introuvable
![404 ... Abonnement introuvable](./media/app-insights-analytics-troubleshooting/070.png)

URL de Hello n’est pas valide. 

* Ouvrez la ressource d’application hello dans [portail Application Insights](https://portal.azure.com). Utilisez ensuite le bouton d’Analytique hello.

## <a name="e-h"></a>404... page inexistante
![404 ... Page inexistante](./media/app-insights-analytics-troubleshooting/080.png)

URL de Hello n’est pas valide.

* Ouvrez la ressource d’application hello dans [portail Application Insights](https://portal.azure.com). Utilisez ensuite le bouton d’Analytique hello.

## <a name="cookies"></a>Activer les cookies tiers
  Consultez [toodisable tiers comment les cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), mais nous devons trop**activer** les.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

