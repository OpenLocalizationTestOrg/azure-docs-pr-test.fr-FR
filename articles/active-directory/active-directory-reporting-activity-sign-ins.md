---
title: "rapports aaaSign sur l’activité dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "Présentation des rapports toosign sur l’activité dans le portail d’Azure Active Directory hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Rapports d’activité de connexion dans le portail d’Azure Active Directory hello

Avec Azure Active Directory (Azure AD) reporting Bonjour [portail Azure](https://portal.azure.com), vous pouvez obtenir des informations de hello nécessaires toodetermine faire de votre environnement.

Hello architecture des rapports dans Azure Active Directory se compose de hello suivant des composants :

- **Activité** 
    - **Activités de connexion** – informations sur l’utilisation de hello des applications gérées et les activités d’authentification des utilisateurs
    - **Activités du système** – Informations sur les activités du système liées aux utilisateurs et à la gestion des groupes, à vos applications gérées et aux activités de répertoire.
- **Sécurité** 
    - **Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur. Pour en savoir plus, consultez Connexions risquées.
    - **Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis. Pour en savoir plus, consultez Utilisateurs avec indicateur de risque.

Cette rubrique donne une vue d’ensemble d’activités de connexion hello.

## <a name="pre-requisite"></a>Conditions préalables

### <a name="who-can-access-hello-data"></a>Qui peut accéder à des données de salutation ?
* Utilisateurs dans le rôle d’administrateur de la sécurité ou de sécurité Reader hello
* Administrateurs généraux
* Tous les utilisateurs (non administrateurs) peuvent accéder à leurs propres connexions 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>Licence Azure AD tooaccess activités avez-vous besoin ?
* Votre client doit avoir une licence Azure AD Premium associée toosee hello tout signe-rapport activité


## <a name="signs-in-activities"></a>Activités de connexion

Informations hello fournies par le rapport d’authentification de l’utilisateur du hello, trouver tooquestions réponses telles que :

* Quel est le modèle hello d’authentification d’un utilisateur ?
* Combien d’utilisateurs se sont connectés au cours d’une semaine ?
* Quel est état hello de ces connexions ?

Votre première entrée tooall de point de connexion activités données **connexions** dans la section d’activité de hello **Azure Active**.


![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/61.png "Activité de connexion")


Un journal d’audit inclut un mode Liste par défaut, qui indique :

- utilisateur Hello
- Hello application hello l’utilisateur a connecté-de
- état de la connexion Hello
- temps de connexion Hello

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/41.png "Activité de connexion")

Vous pouvez personnaliser l’affichage de liste hello en cliquant sur **colonnes** dans la barre d’outils hello.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/19.png "Activité de connexion")

Cela vous permet de toodisplay des champs supplémentaires ou supprimer des champs qui sont déjà affichés.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/42.png "Activité de connexion")

En cliquant sur un élément dans la vue de liste hello, vous obtenez toutes les informations disponibles à ce sujet.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/43.png "Activité de connexion")


## <a name="filtering-sign-in-activities"></a>Filtrage des activités de connexion

toonarrow bas hello signalés au niveau de tooa de données que fonctionne pour vous, vous pouvez filtrer les données de connexions hello hello suivant des champs à l’aide de :

- Intervalle de temps
- Utilisateur
- Application
- Client
- État de la connexion

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/44.png "Activité de connexion")


Hello **intervalle de temps** filtre active tooyou toodefine un laps de temps pour hello a retourné des données.  
Les valeurs possibles sont les suivantes :

- 1 mois
- 7 jours
- 24 heures
- Personnalisée

Lorsque vous sélectionnez une plage personnalisée, vous pouvez configurer une heure de début et une heure de fin.

Hello **utilisateur** filtre vous permet de nom de hello toospecify ou hello nom d’utilisateur principal (UPN) de l’utilisateur hello vous intéressent.

Hello **application** filtre vous permet de nom de hello toospecify de l’application hello vous intéressent.

Hello **client** filtre vous permet de toospecify d’informations sur les appareils hello vous intéressent.

Hello **état de la connexion** filtre vous permet de tooselect un Hello suivant filtre :

- Tout
- Succès
- Échec


## <a name="sign-in-activities-shortcuts"></a>Raccourcis relatifs aux activités de connexion

En outre tooAzure Active Directory, hello portail Azure vous offre deux entrée supplémentaire points activités toosign de données :

- Utilisateurs et groupes
- Applications d’entreprise


### <a name="users-and-groups-sign-ins-activities"></a>Activités de connexion des utilisateurs et des groupes

Informations hello fournies par le rapport d’authentification de l’utilisateur du hello, trouver tooquestions réponses telles que :

- Quel est le modèle hello d’authentification d’un utilisateur ?
- Combien d’utilisateurs se sont connectés au cours d’une semaine ?
- Quel est état hello de ces connexions ?



Vos données de toothis de point d’entrée sont hello utilisateur connectez-vous graphique Bonjour **vue d’ensemble** sous **utilisateurs et groupes**.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/45.png "Activité de connexion")

graphique d’ouverture de session utilisateur Hello montre agrégations hebdomadaire de la connexion ins pour tous les utilisateurs dans une période donnée. valeur par défaut de Hello pour hello laps de temps est de 30 jours.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/46.png "Activité de connexion")

Lorsque vous cliquez sur un jour dans hello connectez-vous graphique, vous obtenez une liste détaillée des activités de connexion hello pour ce jour.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/41.png "Activité de connexion")

Chaque ligne de hello connectez-vous activités liste donne que vous hello des informations détaillées sur hello sélectionné connectez-vous comme :

* Qui s’est connecté ?
* Quel était hello liées UPN ?
* Quelle application a été hello cible hello connectez-vous ?
* Nouveautés d’adresse IP de hello de la connexion au hello ?
* Quel était le statut hello de la connexion au hello ?

Hello **connexions** vous donne une vue d’ensemble complète de toutes les connexions utilisateur.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/51.png "Activité de connexion")



## <a name="usage-of-managed-applications"></a>Utilisation des applications gérées

En disposant d’une vue centrée sur les applications de vos données de connexion, vous pouvez répondre aux questions telles que :

* Qui utilise mes applications ?
* Quelles sont les principales 3 applications hello dans votre organisation ?
* J’ai récemment déployé une application. Comment se comporte-t-elle ?

Vos données de toothis de point d’entrée sont hello supérieur 3 applications dans votre organisation dans le dernier rapport de 30 jours hello Bonjour **vue d’ensemble** sous **des applications d’entreprise**.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/64.png "Activité de connexion")

Hello application utilisation graphique agrégations hebdomadaires de connexions pour vos applications haut 3 dans un laps de temps donné. valeur par défaut de Hello pour hello laps de temps est de 30 jours.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/47.png "Activité de connexion")

Si vous le souhaitez, vous pouvez définir le focus de hello sur une application spécifique.


![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")

Lorsque vous cliquez sur le graphique d’utilisation application hello par jour, vous obtenez une liste détaillée des activités de connexion hello.


![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/48.png "Activité de connexion")


Hello **connexions** vous donne une vue d’ensemble complète de toutes les applications de tooyour d’événements de connexion.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/49.png "Activité de connexion")



## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooknow plus d’informations sur les codes d’erreur activité de connexion, consultez hello [connexion activité rapport codes d’erreur portail d’Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).

