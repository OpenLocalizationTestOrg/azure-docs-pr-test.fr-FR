---
title: aaaManage un espace de travail Machine Learning | Documents Microsoft
description: "Gérer les espaces de travail access tooAzure Machine Learning et de déployer et de gérer les services web d’API de ML"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a>Gestion d'un espace de travail Azure Machine Learning

> [!NOTE]
> Pour plus d’informations sur la gestion des services Web dans le portail de Services Web de Machine Learning hello, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).
> 
> 

Vous pouvez gérer les espaces de travail Machine Learning soit Bonjour portail Azure ou hello portail Azure classic.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a>Utilisez hello portail Azure

toomanage Bonjour portail Azure, un espace de travail :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide d’un compte d’administrateur abonnement Azure.
2. Dans la zone de recherche hello en hello haut hello, entrez « machine learning les espaces de travail », puis sélectionnez **espaces de travail Machine Learning**.
3. Cliquez sur hello espace de travail toomanage.

En outre les informations de gestion de ressources standard toohello et les options disponibles, vous pouvez :

- Vue **propriétés** : cette page affiche des informations d’espace de travail et des ressources hello, et vous pouvez modifier les abonnement hello et groupe de ressources qui n’est connecté à cet espace de travail.
- **Resynchroniser les clés de stockage** -espace de travail hello gère le compte de stockage de clés toohello. Si le compte de stockage hello change les clés, puis vous pouvez cliquer sur **Resync clés** toosynchronize les clés de hello avec espace de travail hello.

associé à cet espace de travail, les services web hello toomanage utiliser le portail de Services Web de Machine Learning hello. Consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md) pour plus d’informations.

> [!NOTE]
> toodeploy ou gérer les nouveaux services web que vous devez avoir un contributeur ou rôle d’administrateur sur le service web hello hello abonnement toowhich est déployé. Si vous invitez à un autre utilisateur tooa d’apprentissage espace de travail, vous devez les affecter tooa un rôle administrateur ou collaborateur sur les abonnement hello avant de pouvoir déployer ou gérer les services web. 
> 
>Pour plus d’informations sur la définition des autorisations d’accès, consultez [afficher les affectations d’accès des utilisateurs et groupes dans le portail Azure - version préliminaire publique de hello](../active-directory/role-based-access-control-manage-assignments.md).

## <a name="use-hello-azure-classic-portal"></a>Utilisez hello portail Azure classic

À l’aide de hello portail Azure classic, vous pouvez gérer vos espaces de travail Machine Learning :

* Surveiller l’utilisation d’espace de travail hello
* Configurer tooallow d’espace de travail hello ou refuser l’accès
* Gérer les services Web créés dans l’espace de travail hello
* Supprimer l’espace de travail hello

En outre, onglet de tableau de bord hello fournit une vue d’ensemble de l’utilisation de l’espace de travail et un aperçu rapide de vos informations d’espace de travail.  

> [!TIP]
> Dans Azure Machine Learning Studio, sur hello **SERVICES WEB** onglet, vous pouvez ajouter, mettre à jour ou supprimer un service Web de la Machine Learning.
> 
> 

toomanage un espace de travail Bonjour portail Azure classic :

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) à l’aide de votre Microsoft Azure compte - utiliser le compte hello hello abonnement Azure associé.
2. Dans le panneau de configuration des services de Microsoft Azure de hello, cliquez sur **MACHINE LEARNING**.
3. Cliquez sur hello espace de travail toomanage.

page d’espace de travail Hello comporte trois onglets :

* **Tableau de bord** -vous permet de l’utilisation de tooview espace de travail et des informations
* **CONFIGURER** -vous permet d’espace de travail toomanage access toohello
* **SERVICES WEB** -vous permet de services Web toomanage qui ont été publiés à partir de cet espace de travail

### <a name="toomonitor-how-hello-workspace-is-being-used"></a>toomonitor utilisation espace de travail hello
Cliquez sur hello **tableau de bord** onglet.

À partir du tableau de bord hello, vous pouvez afficher l’utilisation globale de votre espace de travail et obtenir un aperçu rapide des informations de l’espace de travail.

* Hello **de calcul** graphique montre les ressources de calcul hello utilisés par l’espace de travail hello. Vous pouvez modifier toodisplay de vue hello relatif ou des valeurs absolues, et vous pouvez modifier la période de hello affichée dans le graphique de hello.
* **Présentation de l’utilisation** affiche le stockage Azure utilisé par l’espace de travail hello.
* **Aperçu rapide** fournit un résumé des informations de l’espace de travail ainsi que des liens utiles.

> [!NOTE]
> Hello **connexion tooML Studio** lien ouvre Machine Learning Studio à l’aide de hello Account Microsoft vous êtes actuellement connecté. Hello Microsoft Account vous avez utilisé toosign dans toohello toocreate portail classique Azure un espace de travail automatiquement n’autorisation tooopen cet espace de travail. tooopen un espace de travail, vous devez être connecté toohello Account Microsoft qui a été défini en tant que propriétaire hello d’espace de travail hello, ou vous devez tooreceive une invitation à partir de l’espace de travail hello propriétaire toojoin hello.
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a>toogrant ou suspendre l’accès pour les utilisateurs
Cliquez sur hello **configurer** onglet.

Vous pouvez effectuer les opérations suivantes à partir de l’onglet de configuration hello :

* Suspendre l’espace de travail access toohello Machine Learning en cliquant sur Refuser. Les utilisateurs ne seront plus en mesure de tooopen hello espace de travail Machine Learning Studio. toorestore access, cliquez sur Autoriser.

toomanage autres comptes qui ont accès toohello espace de travail dans Machine Learning Studio, cliquez sur **connexion tooML Studio** Bonjour **tableau de bord** onglet (voir la remarque précédente de hello concernant  **Sign-in tooML Studio**). Espace de travail hello dans Machine Learning Studio s’ouvre. À ce stade, cliquez sur hello **paramètres** onglet, puis **utilisateurs**. Vous pouvez cliquer sur **inviter des utilisateurs plus** toogive utilisateurs accéder toohello, espace de travail, ou sélectionnez un utilisateur, puis cliquez sur **supprimer**.

### <a name="toomanage-web-services-in-this-workspace"></a>services web toomanage dans cet espace de travail
Cliquez sur hello **SERVICES WEB** onglet.

Cela affiche une liste des services Web publiés à partir de cet espace de travail.
toomanage un service web, cliquez sur nom hello dans la page du service Web hello liste tooopen hello.

Un service web peut avoir un ou plusieurs points de terminaison.

* Vous pouvez définir plusieurs points de terminaison dans le point de terminaison addition toohello « Default ». tooadd hello du point de terminaison, cliquez sur **gérer les points de terminaison** bas hello du portail de Services Web de Azure Machine Learning hello du tableau de bord tooopen hello.
* toodelete un point de terminaison (vous ne pouvez pas supprimer de point de terminaison « Par défaut » hello), cliquez sur la case à cocher au début de hello de ligne de point de terminaison hello hello, puis cliquez sur **supprimer**. Cela supprime les point de terminaison hello hello service Web.
  
  > [!NOTE]
  > Si une application utilise le point de terminaison de service hello web lors de la suppression du point de terminaison hello, application hello recevra un hello erreur prochaine que tente de service de hello tooaccess.
  > 
  > 

Cliquez sur nom hello d’un tooopen de point de terminaison de service Web il. 

À partir du tableau de bord hello, vous pouvez afficher l’utilisation globale de votre service Web sur une période de temps. Vous pouvez sélectionner les tooview période hello dans hello période liste déroulante dans le coin supérieur droit de hello de graphiques d’utilisation de hello. tableau de bord Hello montre hello informations suivantes :

* **Les demandes au fil du temps** affiche un graphique de l’étape du nombre de hello de demandes au hello période sélectionnée. Ce graphique vous permet d’identifier les pics d’utilisation.
* **Demandes de requête-réponse** affiche hello le nombre total d’appels de requête-réponse service de hello a reçu sur hello période sélectionnée et l’échec de nombre d'entre eux.
* **Temps moyen de demande-réponse de calcul** affiche une moyenne de temps de hello nécessaire tooexecute hello reçu demandes.
* **Requêtes de lots** hello affiche le nombre total de service hello de requêtes de lots a reçu sur hello période sélectionnée et Échec de nombre d'entre eux.
* **Latence de travail moyenne** affiche une moyenne de temps de hello nécessaire tooexecute hello reçu demandes.
* **Erreurs** numéro hello d’agrégation d’erreurs qui se sont produites sur le service web de toohello appels.
* **Les coûts des services** affiche hello des frais pour le plan de facturation hello associé hello service.

À partir de la page Configurer de hello, vous pouvez mettre à jour hello propriétés suivantes :

* **Description** vous permet de tooenter une description de service Web de hello. Le champ Description est obligatoire.
* **Journalisation** vous permet d’erreur tooenable ou désactiver la connexion de point de terminaison hello. Pour plus d’informations sur la journalisation, voir [Activation de la journalisation pour les services web Machine Learning](machine-learning-web-services-logging.md).
* **Activer les exemples de données** vous permet de tooprovide exemples de données que vous pouvez utiliser le service de requête-réponse de hello tootest. Si vous avez créé le service web de hello dans Machine Learning Studio, les données d’exemple hello sont effectuées à partir des données de hello votre tootrain utilisé votre modèle. Si vous avez créé le service de hello par programme, les données de salutation provient de données d’exemple hello fournies en tant que partie du package JSON hello.

