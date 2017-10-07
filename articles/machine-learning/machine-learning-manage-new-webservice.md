---
title: portail de Services Web de Azure Machine Learning hello aaaUse | Documents Microsoft
description: "Gérer les espaces de travail access tooAzure Machine Learning et de déployer et de gérer les services web d’API de ML"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>Gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello
Vous pouvez gérer votre Machine Learning nouvelle et classique des services Web à l’aide du portail de Services Web de Microsoft Azure Machine Learning hello. Étant donné que les services web classiques et nouveaux sont basés sur des technologies différentes , les fonctionnalités de gestion diffèrent légèrement pour chacun d’eux.

Dans le portail de Services Web de Machine Learning hello, vous pouvez :

* Surveiller l’utilisation du service web de hello.
* Configurer la description de hello, mettre à jour les clés de hello pour le web de hello service (nouveau uniquement), mettre à jour votre stockage compte clé (nouveau uniquement), activer l’enregistrement et activer ou désactiver des exemples de données.
* Supprimer le service web de hello.
* créer, supprimer ou mettre à jour des plans de facturation (nouveau uniquement) ;
* ajouter et supprimer des points de terminaison (classique uniquement).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>Autorisations toomanage nouveau gestionnaire de ressources en fonction des services web

De nouveaux services web sont déployés en tant que ressources Azure. Par conséquent, vous devez disposer des toodeploy des autorisations correctes hello et gérer de nouveaux services web.  toodeploy ou gérer les nouveaux services web que vous devez avoir un contributeur ou rôle d’administrateur sur le service web hello hello abonnement toowhich est déployé. Si vous invitez à un autre utilisateur tooa d’apprentissage espace de travail, vous devez les affecter tooa un rôle administrateur ou collaborateur sur les abonnement hello avant de pouvoir déployer ou gérer les services web. 

Si l’utilisateur de hello n’a pas de corriger des ressources de tooaccess d’autorisations dans le portail de Services Web de Azure Machine Learning hello hello, ils recevront hello l’erreur suivante lors de la tentative de toodeploy un service web :

*Échec du déploiement d’un service web. Ce compte n’a pas suffisamment accès toohello abonnement Azure qui contient l’espace de travail de hello. Dans l’ordre toodeploy un tooAzure de Service Web, hello même compte doit être invité toohello espace de travail et être donné accès toohello abonnement Azure qui contient hello espace de travail.*

Pour plus d'informations sur la création d'un espace de travail, consultez [Créer et partager un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).

Pour plus d’informations sur la définition des autorisations d’accès, consultez [afficher les affectations d’accès des utilisateurs et groupes dans le portail Azure - version préliminaire publique de hello](../active-directory/role-based-access-control-manage-assignments.md).


## <a name="manage-new-web-services"></a>Gérer de nouveaux services web
toomanage vos services d’un site Web :

1. Connectez-vous à toohello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portail à l’aide de votre compte Microsoft Azure - utiliser le compte hello associé hello abonnement Azure.
2. Cliquez sur hello, **Services Web**.

La liste des services web déployés pour votre abonnement s’affiche. 

toomanage un service Web, cliquez sur les Services Web. Vous pouvez effectuer les opérations suivantes à partir de la page des Services Web hello :

* Cliquez sur hello web service toomanage il.
* Cliquez sur hello Plan de facturation pour hello web service tooupdate il.
* supprimer un service web.
* Copie d’un service web et le déployer tooanother région.

Lorsque vous cliquez sur un service web, page de démarrage rapide du service web hello s’ouvre. page de démarrage rapide du service web Hello comporte deux options de menu qui vous permettent de toomanage votre service web :

* **Tableau de bord** -vous permet de tooview utilisation du service Web.
* **CONFIGURER** - vous permet de tooadd un texte descriptif, mise à jour hello clé compte de stockage hello associé au service Web, hello et activer ou désactiver des exemples de données.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Analyse l’utilisation du service web de hello
Cliquez sur hello **tableau de bord** onglet.

À partir du tableau de bord hello, vous pouvez afficher l’utilisation globale de votre service Web sur une période de temps. Vous pouvez sélectionner les tooview période hello dans hello période liste déroulante dans le coin supérieur droit de hello de graphiques d’utilisation de hello. tableau de bord Hello montre hello informations suivantes :

* **Les demandes au fil du temps** affiche un graphique de l’étape du nombre de hello de demandes au hello période sélectionnée. Ce graphique vous permet d’identifier les pics d’utilisation.
* **Demandes de requête-réponse** affiche hello le nombre total d’appels de requête-réponse service de hello a reçu sur hello période sélectionnée et l’échec de nombre d'entre eux.
* **Temps moyen de demande-réponse de calcul** affiche une moyenne de temps de hello nécessaire tooexecute hello reçu demandes.
* **Requêtes de lots** hello affiche le nombre total de service hello de requêtes de lots a reçu sur hello période sélectionnée et Échec de nombre d'entre eux.
* **Latence de travail moyenne** affiche une moyenne de temps de hello nécessaire tooexecute hello reçu demandes.
* **Erreurs** numéro hello d’agrégation d’erreurs qui se sont produites sur le service web de toohello appels.
* **Les coûts des services** affiche hello des frais pour le plan de facturation hello associé hello service.

### <a name="configuring-hello-web-service"></a>Configuration du service web de hello
Cliquez sur hello **configurer** option de menu.

Vous pouvez mettre à jour hello propriétés suivantes :

* **Description** vous permet de tooenter une description de service Web de hello.
* **Titre** vous permet de tooenter un titre pour le service Web de hello
* **Clés** vous permet de toorotate vos clés API primaires et secondaires.
* **Clé de compte de stockage** vous permet de tooupdate hello clé hello compte de stockage associé aux modifications de service Web hello. 
* **Activer les exemples de données** vous permet de tooprovide exemples de données que vous pouvez utiliser le service de requête-réponse de hello tootest. Si vous avez créé le service web de hello dans Machine Learning Studio, les données d’exemple hello sont effectuées à partir des données de hello votre tootrain utilisé votre modèle. Si vous avez créé le service de hello par programme, les données de salutation provient de données d’exemple hello fournies en tant que partie du package JSON hello.

### <a name="managing-billing-plans"></a>Gestion des plans de facturation
Cliquez sur hello **Plans** option de menu à partir de la page de démarrage rapide de services web hello. Vous pouvez également cliquer sur le plan hello associé spécifique toomanage de service Web qui planifier.

* **Nouvelle** vous permet de toocreate un nouveau plan.
* **Instance de l’ajout/suppression de Plan** vous permet de trop « montée en charge » une capacité de tooadd de plan existant.
* **Mise à niveau/rétrogradation** vous permet de trop « montée en puissance » une capacité de tooadd de plan existant.
* **Supprimer** vous permet de toodelete un plan.

Cliquez sur un plan tooview son tableau de bord. tableau de bord Hello vous donne un plan ou instantané de l’utilisation sur une période de temps. tooselect hello tooview période de temps, cliquez sur hello **période** déroulante hello en haut à droite du tableau de bord. 

le tableau de bord Hello plan fournit hello informations suivantes :

* **Description plan** affiche des informations sur les coûts de hello et capacité associé au plan de hello.
* **Planifier l’utilisation** affiche le nombre de hello de transactions et des heures de calcul qui ont été facturés par rapport au plan de hello.
* **Services Web** affiche le nombre hello de services Web qui sont à l’aide de ce plan.
* **Premiers Web par les appels de Service** affiche les services Web hello quatre principaux qui effectuent des appels sont facturées par rapport au plan de hello.
* **Principaux de Services Web par heures de calcul** affiche les services Web hello quatre principaux qui utilisent les ressources de calcul sont facturées par rapport au plan de hello.

## <a name="manage-classic-web-services"></a>Gérer des services web classiques
> [!NOTE]
> les procédures de Hello dans cette section sont les services web toomanaging pertinentes classique via le portail de Services Web de Azure Machine Learning hello. Pour plus d’informations sur la gestion de site Web Classic services via hello Machine Learning Studio et hello Azure classic portail, consultez [gérer un espace de travail Azure Machine Learning](machine-learning-manage-workspace.md).
> 
> 

toomanage vos services Web classique :

1. Connectez-vous à toohello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portail à l’aide de votre compte Microsoft Azure - utiliser le compte hello associé hello abonnement Azure.
2. Cliquez sur hello, **classique des Services Web**.

toomanage un Service Web classique, cliquez sur **classique des Services Web**. À partir de la page des Services Web classique de hello, vous pouvez :

* Cliquez sur des points de terminaison hello web service tooview hello associé.
* supprimer un service web.

Lorsque vous gérez un service Web classique, vous gérer chacun des points de terminaison hello séparément. Lorsque vous cliquez sur un service web dans la page des Services Web hello, liste hello de points de terminaison associés au service de hello s’ouvre. 

Sur la page de point de terminaison hello classique Service Web, vous pouvez ajouter et supprimer des points de terminaison de service de hello. Pour plus d’informations sur l’ajout de points de terminaison, consultez [Création de points de terminaison](machine-learning-create-endpoint.md).

Cliquez sur une page démarrage rapide de hello points de terminaison tooopen hello web service. Sur la page de démarrage rapide de hello, existe-t-il deux options de menu qui vous permettent de toomanage votre service web :

* **Tableau de bord** -vous permet de tooview utilisation du service Web.
* **CONFIGURER** -vous permet de tooadd un texte descriptif, activer la journalisation des erreurs et désactiver la clé de mise à jour hello compte de stockage hello associé au service Web, hello et activer et désactiver des exemples de données.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Analyse l’utilisation du service web de hello
Cliquez sur hello **tableau de bord** onglet.

À partir du tableau de bord hello, vous pouvez afficher l’utilisation globale de votre service Web sur une période de temps. Vous pouvez sélectionner les tooview période hello dans hello période liste déroulante dans le coin supérieur droit de hello de graphiques d’utilisation de hello. tableau de bord Hello montre hello informations suivantes :

* **Les demandes au fil du temps** affiche un graphique de l’étape du nombre de hello de demandes au hello période sélectionnée. Ce graphique vous permet d’identifier les pics d’utilisation.
* **Demandes de requête-réponse** affiche hello le nombre total d’appels de requête-réponse service de hello a reçu sur hello période sélectionnée et l’échec de nombre d'entre eux.
* **Temps moyen de demande-réponse de calcul** affiche une moyenne de temps de hello nécessaire tooexecute hello reçu demandes.
* **Requêtes de lots** hello affiche le nombre total de service hello de requêtes de lots a reçu sur hello période sélectionnée et Échec de nombre d'entre eux.
* **Latence de travail moyenne** affiche une moyenne de temps de hello nécessaire tooexecute hello reçu demandes.
* **Erreurs** numéro hello d’agrégation d’erreurs qui se sont produites sur le service web de toohello appels.
* **Les coûts des services** affiche hello des frais pour le plan de facturation hello associé hello service.

### <a name="configuring-hello-web-service"></a>Configuration du service web de hello
Cliquez sur hello **configurer** option de menu.

Vous pouvez mettre à jour hello propriétés suivantes :

* **Description** vous permet de tooenter une description de service Web de hello. Le champ Description est obligatoire.
* **Journalisation** vous permet d’erreur tooenable ou désactiver la connexion de point de terminaison hello. Pour plus d’informations sur la journalisation, voir [Activation de la journalisation pour les services web Machine Learning](machine-learning-web-services-logging.md).
* **Activer les exemples de données** vous permet de tooprovide exemples de données que vous pouvez utiliser le service de requête-réponse de hello tootest. Si vous avez créé le service web de hello dans Machine Learning Studio, les données d’exemple hello sont effectuées à partir des données de hello votre tootrain utilisé votre modèle. Si vous avez créé le service de hello par programme, les données de salutation provient de données d’exemple hello fournies en tant que partie du package JSON hello.

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>Accorder ou suspendre l’accès des services de tooWeb pour les utilisateurs dans le portail de hello
À l’aide de hello portail Azure classic, vous pouvez autoriser ou refuser l’accès aux utilisateurs de toospecific.

### <a name="access-for-users-of-new-web-services"></a>Accès des utilisateurs de nouveaux services web
tooenable autres toowork utilisateurs avec vos services Web dans le portail de Services Web de Azure Machine Learning hello, vous devez les ajouter en tant qu’administrateurs de co sur votre abonnement Azure.

Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) à l’aide de votre Microsoft Azure compte - utiliser le compte hello hello abonnement Azure associé.

1. Dans le volet de navigation hello, cliquez sur **paramètres**, puis cliquez sur **administrateurs**.
2. Au bas de hello de fenêtre hello, cliquez sur **ajouter**. 
3. Dans la boîte de dialogue ADD A CO-ADMINISTRATOR de hello, hello de type adresse de messagerie de personne hello tooadd en tant que coadministrateur, puis sélectionnez abonnement hello que vous souhaitez hello coadministrateur tooaccess.
4. Cliquez sur **Enregistrer**.

### <a name="access-for-users-of-classic-web-services"></a>Accès des utilisateurs de services web classiques
toomanage un espace de travail :

Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) à l’aide de votre Microsoft Azure compte - utiliser le compte hello hello abonnement Azure associé.

1. Dans le panneau de configuration des services de Microsoft Azure de hello, cliquez sur **MACHINE LEARNING**.
2. Cliquez sur hello espace de travail toomanage.
3. Cliquez sur hello **configurer** onglet.

À partir de l’onglet de configuration hello, vous pouvez suspendre l’espace de travail access toohello Machine Learning en cliquant sur **DENY**. Les utilisateurs ne seront plus en mesure de tooopen hello espace de travail Machine Learning Studio. toorestore accès, cliquez sur **autoriser**.

utilisateurs de toospecific :

toomanage autres comptes qui ont accès toohello espace de travail dans Machine Learning Studio, cliquez sur **connexion tooML Studio** Bonjour **tableau de bord** onglet. Espace de travail hello dans Machine Learning Studio s’ouvre. À ce stade, cliquez sur hello **paramètres** onglet, puis **utilisateurs**. Vous pouvez cliquer sur **inviter des utilisateurs plus** toogive utilisateurs accéder toohello, espace de travail, ou sélectionnez un utilisateur, puis cliquez sur **supprimer**.

> [!NOTE]
> Hello **connexion tooML Studio** lien ouvre Machine Learning Studio à l’aide de hello Account Microsoft vous êtes actuellement connecté. Hello Microsoft Account vous avez utilisé toosign dans toohello toocreate portail classique Azure un espace de travail automatiquement n’autorisation tooopen cet espace de travail. tooopen un espace de travail, vous devez être connecté toohello Account Microsoft qui a été défini en tant que propriétaire hello d’espace de travail hello, ou vous devez tooreceive une invitation à partir de l’espace de travail hello propriétaire toojoin hello.
> 
> 

