---
title: "les notifications aaaConfigure et envoyer par courrier électronique des modèles de gestion des API Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure notifications et modèles dans Azure API Management de courrier électronique."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>Comment les notifications tooconfigure et envoyer par courrier électronique des modèles de gestion des API Azure
Gestion des API permet hello tooconfigure des notifications d’événements spécifiques ou des modèles de messages électroniques hello tooconfigure sont toocommunicate utilisé avec les administrateurs de hello et aux développeurs d’une instance de la gestion des API. Cette rubrique montre comment les notifications tooconfigure pour hello événements disponibles et fournit une vue d’ensemble de la configuration de modèles de messages électroniques hello utilisés pour ces événements.

## <a name="publisher-notifications"></a>Configuration des notifications de l’éditeur
notifications de tooconfigure, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API. Cela vous prend un portail de publication de gestion des API toohello.

![Portail des éditeurs][api-management-management-console]

> [!NOTE] 
> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.

Cliquez sur **Notifications** de hello **gestion des API** hello menu gauche tooview notification hello est disponible.

![Notifications de l’éditeur][api-management-publisher-notifications]

Hello la liste suivante d’événements peut être configurée pour les notifications.

* **Demandes d’abonnement (nécessitant l’approbation)** : hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique à propos des demandes d’abonnement pour les produits d’API nécessitant une approbation.
* **Les nouveaux abonnements** : hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique relatives à des abonnements de produit d’API.
* **Les demandes d’application de la galerie** : hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique lorsque les nouvelles applications sont soumis toohello Galerie d’applications.
* **Cci** : hello destinataires spécifiés et les utilisateurs reçoivent par courrier électronique invisible copie de tous les messages électroniques envoyés toodevelopers.
* **Nouveau problème ou un commentaire** - hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique lorsqu’un nouveau problème ou commentaire est envoyé sur le portail des développeurs hello.
* **Message de fermer le compte** : hello destinataires spécifiés et les utilisateurs reçoivent des notifications par courrier électronique quand un compte est fermé.
* **Limite de quota approchant abonnement** : hello suivant des destinataires de courrier électronique et les utilisateurs reçoivent des notifications par courrier électronique lors de l’utilisation d’abonnement obtient toousage fermer quota.

Pour chaque événement, vous pouvez spécifier des destinataires de courrier électronique à l’aide de la zone de texte adresse e-mail hello ou vous pouvez sélectionner des utilisateurs à partir d’une liste.

toospecify hello messagerie adresses toobe averti, entrez-les dans la zone de texte adresse e-mail hello. Si vous devez entrer plusieurs adresses, séparez-les par des virgules.

![Notification recipients][api-management-email-addresses]

toospecify hello utilisateurs toobe la notification, cliquez sur **Ajouter destinataire**, hello la case en regard de hello utilisateurs toobe est notifiée, puis cliquez sur **OK**.

> [!NOTE] 
> Seuls les administrateurs sont affichés dans la liste de hello.


Après avoir configuré les destinataires des notifications hello, cliquez sur **enregistrer** tooapply hello mis à jour les destinataires des notifications.

> [!NOTE] 
> Si vous quittez hello **Notifications du serveur de publication** portail de publication onglet hello vous avertit qu’il y a des modifications non enregistrées.


## <a name="email-templates"></a>Configuration des modèles de courrier électronique
Gestion des API fournit des modèles de messagerie pourquoi les messages électroniques qui sont envoyés en cours hello d’administration et à l’aide du service de hello. Hello suivant des modèles de messages électroniques est fournie.

* Demande d'ajout à la galerie d'applications approuvée
* Lettre d'adieu au développeur
* Notification de la limite du quota d'abonnement bientôt atteinte
* Invitation de l'utilisateur
* Nouveau commentaire ajouté tooan problème
* Nouveau problème reçu
* Nouvel abonnement activé
* Confirmation du renouvellement de l'abonnement
* Refus de la demande d'abonnement
* Réception de la demande d'abonnement

Ces modèles peuvent être modifiés comme vous le souhaitez.

tooview et configurer les modèles de messagerie hello pour votre instance de la gestion des API, cliquez sur **Notifications** de hello **gestion des API** menu hello gauche et sélectionnez hello **modèles de messages électroniques**  onglet.

![Email templates][api-management-email-templates]

tooview ou modifier un modèle spécifique, sélectionnez-le dans hello **modèles** liste déroulante.

![Email templates list][api-management-email-templates-list]

Pour chaque modèle de message, l'objet est au format texte et le corps au format HTML. Chaque élément peut être personnalisé.

![Email template editor][api-management-email-template]

Hello **paramètres** liste contient une liste de paramètres, où insérées dans hello objet ou le corps, sera remplacé hello désigné lorsque hello e-mail est envoyé. tooinsert un paramètre, placez le curseur à hello où vous le souhaitez toogo de paramètre hello et cliquez sur hello flèche toohello à gauche du nom de paramètre hello.

Cliquez sur **aperçu** ou **envoyer un test** toosee comment par courrier électronique hello sera rechercher ou envoyer un courrier électronique de test.

> [!NOTE] 
> paramètres de Hello ne sont pas remplacées par des valeurs réelles lors de l’aperçu ou l’envoi d’un test.

modèle d’e-mail toohello toosave hello modifications, cliquez sur **enregistrer**, ou cliquez sur les modifications de hello toocancel **Annuler**.
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
