---
title: "aaaBuy un nom de domaine personnalisé pour les applications Web Azure"
description: "Découvrez comment nommer des toobuy un domaine personnalisé avec une application web dans Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Acheter un nom de domaine personnalisé pour Azure Web Apps

Les domaines App Service (version préliminaire) sont des domaines de niveau supérieur gérés directement dans Azure. Il est donc facile toomanage des domaines personnalisés [Azure Web Apps](app-service-web-overview.md). Ce didacticiel vous montre comment toobuy un domaine de Service d’application et attribuez DNS noms tooAzure Web Apps.

Cet article concerne Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps). Pour la machine virtuelle Azure ou le stockage Azure, consultez [tooAzure de domaine du Service d’applications affecter machine virtuelle ou le stockage Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/). Pour Services cloud, consultez [Configuration d’un nom de domaine personnalisé pour un service cloud Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

* [Créez une application App Service](/azure/app-service/), ou utilisez une application créée pour un autre didacticiel.

## <a name="prepare-hello-app"></a>Préparer l’application hello

toouse des domaines personnalisés dans les d’applications Web Azure, votre application web [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) doit être un niveau payant (**Shared**, **base**, **Standard**, ou **Premium**). Dans cette étape, vous vérifiez que l’application web hello est Bonjour pris en charge niveau tarifaire.

### <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez hello [portail Azure](https://portal.azure.com) et connectez-vous avec votre compte Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Accédez application toohello Bonjour portail Azure

Dans le menu de gauche hello, sélectionnez **des Services d’application**, puis sélectionnez le nom hello de l’application hello.

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/select-app.png)

Page de gestion hello Hello application de Service de l’application s’affiche.  

### <a name="check-hello-pricing-tier"></a>Vérifier le niveau tarifaire de hello

Bonjour barre de navigation de page de l’application hello gauche, faites défiler toohello **paramètres** section et sélectionnez **montée en puissance (plan App Service)**.

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

niveau actuel de l’application Hello est mis en surbrillance d’une bordure bleue. Vérifiez que cette application hello n’est pas hello de toomake **libre** couche. DNS personnalisé n’est pas pris en charge dans hello **libre** couche. 

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Si hello plan App Service n’est pas **libre**, fermez hello **choisir votre niveau tarifaire** page et ignorer trop[domaine de hello acheter](#buy-the-domain).

### <a name="scale-up-hello-app-service-plan"></a>Montée en puissance hello plan App Service

Sélectionnez un des niveaux de hello occupé (**Shared**, **base**, **Standard**, ou **Premium**). 

Cliquez sur **Sélectionner**.

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Lorsque vous voyez hello suivant la notification, l’opération de mise à l’échelle de hello est terminée.

![Confirmation d’opération de mise à l’échelle](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Acheter hello domaine

### <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure
Ouvrez hello [portail Azure](https://portal.azure.com/) et connectez-vous avec votre compte Azure.

### <a name="launch-buy-domains"></a>Lancer Acheter des domaines
Bonjour **Web Apps** , cliquez sur le nom hello de votre application web, sélectionnez **paramètres**, puis sélectionnez **les domaines personnalisés**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Bonjour **les domaines personnalisés** , cliquez sur **acheter des domaines**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Configurer le fournisseur de domaine hello

Bonjour **domaine d’application Service** page hello **recherche pour le domaine** boîte, de type hello nom du domaine toobuy et type `Enter`. Hello suggérées domaines disponibles sont affichés juste en dessous de zone de texte hello. Sélectionnez un ou plusieurs domaines que vous souhaitez toobuy. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Cliquez sur hello **coordonnées de contact** et remplissez le formulaire des informations de contact du domaine hello. Lorsque vous avez terminé, cliquez sur **OK** page de domaine d’application Service tooreturn toohello.
   
Il est très important de remplir tous les champs obligatoires aussi précisément que possible. Domaines de toopurchase échec peuvent entraîner des données incorrectes pour les informations de contact. 

Ensuite, sélectionnez les options de hello souhaité pour votre domaine. Consultez hello tableau pour obtenir des explications suivant :

| Paramètre | Valeur suggérée | Description |
|-|-|-|
|Renouvellement automatique | **Activer** | Renouvelle automatiquement votre domaine App Service chaque année. Votre carte de crédit hello même prix d’achat au moment de hello de renouvellement. |
|Protection des données personnelles | Activer | S’abonner trop « Confidentialité », qui est incluse dans le prix d’achat hello _gratuitement_ (à l’exception des domaines de premier niveau dont le Registre ne prennent pas en charge la protection des données, telles que _. co.in_, _. Co.uk_, et ainsi de suite). |
| Attribuer des noms d’hôte par défaut | **www** et **@** | Sélectionnez hello souhaitée des liaisons de nom d’hôte, si vous le souhaitez. Lorsqu’une opération d’achat domaine hello est terminée, votre application web est accessible à des noms d’hôtes hello sélectionné. Si l’application hello web se trouve derrière [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), vous ne voyez pas le domaine racine hello hello option tooassign (@), parce que Traffic Manager ne pas les enregistrements de prise en charge. Vous pouvez modifier les attributions de nom d’hôte toohello issue de l’achat de domaine hello. |

### <a name="accept-terms-and-purchase"></a>Accepter les mentions et acheter

Cliquez sur **juridiques** tooreview hello générales de frais de hello, puis cliquez sur **acheter**.

> [!NOTE]
> Domaines de Service d’application d’utilisent des domaines de hello toohost Azure DNS. En outre frais d’inscription de domaine toohello, frais d’utilisation pour Azure DNS s’appliquent. Pour en savoir plus, consultez la page relative à la [tarification Azure DNS](https://azure.microsoft.com/pricing/details/dns/).
>
>

Dans hello **domaine d’application Service** , cliquez sur **OK**. Lors de l’opération de hello est en cours d’exécution, vous voyez hello suivant des notifications :

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>Noms d’hôte de test hello

Si vous avez attribué par défaut les noms d’hôte tooyour web app, vous voyez également une notification de réussite pour chaque nom d’hôte sélectionné. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

Vous voyez également les noms d’hôte hello sélectionné Bonjour **les domaines personnalisés** page hello **noms d’hôtes** section. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

noms d’hôtes de tootest hello, accédez toohello répertorié les noms d’hôtes dans le navigateur de hello. Dans l’exemple hello Bonjour précédant la capture d’écran, essayez too_kontoso.net_ et _www.kontoso.net_.

## <a name="assign-hostnames-tooweb-app"></a>Affecter des noms d’hôtes tooweb application

Si vous ne choisissez pas les tooassign une ou plus par défaut les noms d’hôte tooyour web app pendant hello processus d’achat, ou si vous avez besoin tooassign un nom d’hôte non répertorié, vous pouvez affecter un nom d’hôte à tout moment.

Vous pouvez également affecter des noms d’hôte dans tooany de domaine de Service d’application hello autre application web. Hello étapes dépendent si hello domaine du Service d’application et l’application web hello appartiennent toohello même abonnement.

- Autre abonnement : mapper les enregistrements DNS personnalisés à partir de domaine de Service d’application hello toohello l’application web à un domaine extérieur achetée. Pour plus d’informations sur l’ajout de DNS personnalisé des noms tooan domaine du Service d’application, consultez [gérer les enregistrements DNS personnalisés](#custom). toomap une application web de tooa domaine achetées externe, consultez [mapper un tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md). 
- Même abonnement : hello utilisation comme suit.

### <a name="launch-add-hostname"></a>Lancer Ajouter un nom d’hôte
Bonjour **des Services d’application** page, le nom hello select de votre application web que vous souhaitez que les noms d’hôte tooassign pour sélectionner **paramètres**, puis sélectionnez **les domaines personnalisés**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Assurez-vous que votre domaine achetée est répertorié dans hello **domaines de Service d’application** section, mais ne l’activez pas. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Tous les domaines de Service d’application Bonjour même abonnement sont affichés dans l’application hello web **les domaines personnalisés** page. Si votre domaine est inclus dans l’abonnement de l’application hello web, mais il ne figure pas dans l’application hello web **les domaines personnalisés** page, essayez de rouvrir hello **les domaines personnalisés** page ou d’actualiser la page Web de hello. Vérifiez également représentant une cloche de notification hello haut hello hello portail Azure pour les échecs de la création ou de progression.
>
>

Sélectionnez **Ajouter un nom d’hôte**.

### <a name="configure-hostname"></a>Configurer le nom d’hôte
Bonjour **ajouter le nom d’hôte** boîte de dialogue, le nom de domaine complet de type hello de votre domaine de Service d’application ou un sous-domaine. Par exemple :

- kontoso.net
- www.kontoso.net
- abc.kontoso.net

Lorsque vous avez terminé, sélectionnez **Valider**. type d’enregistrement de nom d’hôte Hello est automatiquement sélectionné pour vous.

Sélectionnez **Ajouter un nom d’hôte**.

Lors de l’opération de hello est terminée, vous voyez une notification de réussite pour hello affecté le nom d’hôte.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Fermer Ajouter un nom d’hôte
Bonjour **ajouter le nom d’hôte** page, attribuer un autre nom d’hôte tooyour web application, comme vous le souhaitez. Une fois terminé, fermez hello **ajouter le nom d’hôte** page.

Vous devez maintenant voir hello viennent d’être attribué hostname(s) dans votre application **les domaines personnalisés** page.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>Noms d’hôte de test hello

Accédez de noms d’hôtes toohello répertorié dans le navigateur de hello. Dans l’exemple hello Bonjour précédant la capture d’écran, essayez too_abc.kontoso.net_.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Gérer des enregistrements DNS personnalisés

Dans Azure, les enregistrements DNS d’un domaine App Service sont gérés à l’aide d’[Azure DNS](https://azure.microsoft.com/services/dns/). Vous pouvez ajouter, supprimer et mettre à jour les enregistrements DNS, comme pour un domaine acheté en externe.

### <a name="open-app-service-domain"></a>Ouvrir le domaine App Service

Bonjour portail Azure, à partir du menu de gauche hello, sélectionnez **plus Services** > **domaines de Service d’application**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Sélectionnez hello domaine toomanage. 

### <a name="access-dns-zone"></a>Accéder à la zone DNS

Dans le menu de gauche du domaine hello, sélectionnez **zone DNS**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Cette action ouvre hello [zone DNS](../dns/dns-zones-records.md) page de votre domaine de Service d’application dans Azure DNS. Pour plus d’informations sur la façon de tooedit les enregistrements DNS, consultez [comment toomanage les Zones DNS dans hello Azure portal](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>Annuler l’achat (supprimer le domaine)

Après avoir acheté hello domaine du Service d’application, vous avez cinq jours toocancel votre achat d’un remboursement intégral. Après cinq jours, vous pouvez supprimer hello domaine du Service d’application, mais ne peut pas remboursé.

### <a name="open-app-service-domain"></a>Ouvrir le domaine App Service

Bonjour portail Azure, à partir du menu de gauche hello, sélectionnez **plus Services** > **domaines de Service d’application**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Sélectionnez hello domaine tooyou que vous souhaitez toocancel ou supprimer. 

### <a name="delete-hostname-bindings"></a>Supprimer des liaisons de noms d’hôte

Dans le menu de gauche du domaine hello, sélectionnez **liaisons de nom d’hôte**. liaisons de nom d’hôte Hello de tous les services Azure sont répertoriées ici.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

Impossible de supprimer hello App Service de domaine jusqu'à ce que toutes les liaisons de nom d’hôte sont supprimés.

Supprimez chaque liaison de nom d’hôte en sélectionnant **...** > **Supprimer**. Une fois que toutes les liaisons de hello sont supprimés, sélectionnez **enregistrer**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>Annuler ou supprimer

Dans le menu de gauche du domaine hello, sélectionnez **vue d’ensemble**. 

Si la période d’annulation hello sur le domaine de hello acheté n’est pas écoulé, sélectionnez **Annuler achat**. Dans le cas contraire, vous verrez le bouton **Supprimer**. domaine de hello toodelete sans restitution, sélectionnez **supprimer**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Sélectionnez **OK** opération hello de tooconfirm. Si vous ne souhaitez pas tooproceed, cliquez n’importe où en dehors de la boîte de dialogue de confirmation hello.

Une fois hello terminée, domaine de hello est lancé à partir de votre abonnement et disponibles pour toute personne toopurchase à nouveau. 
