---
title: aaaAdd un tooan CDN Azure App Service | Documents Microsoft
description: "Ajouter un toocache de Azure App Service de réseau de distribution de contenu (CDN) tooan et remettre vos fichiers statiques à partir de serveurs clients de fermer tooyour hello du monde."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>Ajouter un tooan de réseau de distribution de contenu (CDN) Azure App Service

[Réseau de distribution de contenu (CDN) Azure](../cdn/cdn-overview.md) met en cache le contenu web statique au débit maximal de tooprovide emplacements stratégiques pour la diffusion de contenu toousers. Hello CDN réduit également la charge du serveur sur votre application web. Ce didacticiel montre comment tooadd Azure CDN tooa [application web dans Azure App Service](app-service-web-overview.md). 

Voici la page d’accueil hello de hello exemple site HTML statique que vous allez travailler avec :

![Page d’accueil de l’exemple d’application](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

Ce que vous allez apprendre :

> [!div class="checklist"]
> * Créer un point de terminaison CDN.
> * Actualiser les ressources mises en cache.
> * Utiliser la requête des chaînes de versions de toocontrol mis en cache.
> * Utilisez un domaine personnalisé pour le point de terminaison CDN hello.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

- [Installez Git](https://git-scm.com/)
- [Installation d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Créer une application web de hello

toocreate hello web application que vous allez travailler avec suivi hello [démarrage rapide HTML statique](app-service-web-get-started-html.md) via hello **Parcourir toohello application** étape.

### <a name="have-a-custom-domain-ready"></a>Nécessité d’avoir un nom de domaine

étape de domaine personnalisé hello toocomplete de ce didacticiel, vous devez tooown un domaine personnalisé et disposer du Registre de l’accès tooyour DNS pour votre fournisseur de domaine (par exemple, GoDaddy). Par exemple, les entrées DNS tooadd pour `contoso.com` et `www.contoso.com`, tooconfigure accès hello vos paramètres DNS pour hello doivent être `contoso.com` domaine racine.

Si vous n’avez pas encore un nom de domaine, envisagez d’hello [didacticiel du domaine du Service d’applications](custom-dns-web-site-buydomains-web-app.md) toopurchase un domaine à l’aide de hello portail Azure. 

## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure

Ouvrez un navigateur et accédez toohello [portail Azure](https://portal.azure.com).

## <a name="create-a-cdn-profile-and-endpoint"></a>Création d’un profil CDN et d’un point de terminaison

Bonjour barre de navigation gauche, sélectionnez **des Services d’application**, puis sélectionnez application hello que vous avez créé dans hello [démarrage rapide HTML statique](app-service-web-get-started-html.md).

![Sélectionnez l’application de Service d’applications dans le portail de hello](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

Bonjour **du Service d’applications** page hello **paramètres** section, sélectionnez **mise en réseau > configurer le CDN Azure pour votre application**.

![Sélectionnez le CDN dans le portail de hello](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

Bonjour **Azure Content Delivery Network** , fournissez hello **nouveau point de terminaison** paramètres comme spécifié dans la table de hello.

![Créer le point de terminaison et un profil dans le portail de hello](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| Paramètre | Valeur suggérée | Description |
| ------- | --------------- | ----------- |
| **Profil CDN** | myCDNProfile | Sélectionnez **nouvel** toocreate profil CDN. Profil CDN est une collection de points de terminaison CDN avec hello même niveau de tarification. |
| **Niveau tarifaire** | Standard Akamai | Hello [tarification](../cdn/cdn-overview.md#azure-cdn-features) Spécifie le fournisseur de hello et les fonctionnalités disponibles. Dans ce didacticiel, nous utilisons Standard Akamai. |
| **Nom du point de terminaison CDN** | N’importe quel nom qui est unique dans le domaine de azureedge.net hello | Accéder à vos ressources mises en cache au niveau du domaine de hello  *\<endpointname >. azureedge.net*.

Sélectionnez **Créer**.

Azure crée le point de terminaison et le profil de hello. nouveau point de terminaison Hello s’affiche dans hello **points de terminaison** liste hello même page, et lorsqu’elle est approvisionnée hello statut **en cours d’exécution**.

![Nouveau point de terminaison dans la liste](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>Hello de test point de terminaison CDN

Si vous avez sélectionné le niveau tarifaire Verizon, il faut généralement compter environ 90 minutes pour la propagation du point de terminaison. Pour Akamai, la propagation prend quelques minutes.

exemple d’application Hello a un `index.html` fichier et *css*, *img*, et *js* dossiers qui contiennent d’autres ressources statiques. Hello contenu sont des chemins d’accès pour tous ces fichiers hello identique au point de terminaison CDN hello. Par exemple, les deux URL suivantes de hello accéder hello *bootstrap.css* fichier Bonjour *css* dossier :

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

Accédez à un toohello navigateur suivant l’URL :

```
http://<endpointname>.azureedge.net/index.html
```

![Page d’accueil de l’exemple d’application traitée à partir du CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 Vous consultez hello même page que vous avez exécuté précédemment dans une application web Azure. Azure CDN a récupéré les ressources de l’application web hello origine et sert de point de terminaison CDN hello

tooensure que cette page est mise en cache dans hello CDN, page hello d’actualisation. Deux demandes pour hello même actif sont parfois requis pour hello CDN toocache hello contenu demandé.

Pour plus d’informations sur la création de profils et de points de terminaison Azure CDN, consultez [Prise en main d’Azure CDN](../cdn/cdn-create-new-endpoint.md).

## <a name="purge-hello-cdn"></a>Purge hello CDN

Hello CDN actualise régulièrement ses ressources de l’application web de hello origine selon hello time-to-live (TTL) configuration. la valeur par défaut de Hello durée de vie est de sept jours.

Dans certains cas vous devrez peut-être toorefresh hello CDN avant hello date d’expiration de la durée de vie : par exemple, lorsque vous déployez l’application web toohello contenu mis à jour. tootrigger une actualisation, vous pouvez purger manuellement les ressources CDN hello. 

Dans cette section du didacticiel de hello, vous déployez une application web de toohello modification et purgez hello CDN tootrigger hello CDN toorefresh son cache.

### <a name="deploy-a-change-toohello-web-app"></a>Déployer une application web de toohello modification

Ouvrez hello `index.html` et ajoutez «-V2 « toohello H1 en-tête, comme indiqué dans hello l’exemple suivant : 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

Valider votre modification et déployer l’application web toohello.

```bash
git commit -am "version 2"
git push azure master
```

Une fois le déploiement terminé, parcourir toohello URL de l’application web et que vous consultez hello modifier.

```
http://<appname>.azurewebsites.net/index.html
```

![V2 dans le titre de l’application web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

URL de point de terminaison CDN Parcourir toohello pour la page d’accueil hello et que vous ne voyez pas hello modifier, car la version de mise en cache hello Bonjour CDN n’a pas encore expiré. 

```
http://<endpointname>.azureedge.net/index.html
```

![Pas de V2 dans le titre du CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Purge hello CDN dans le portail de hello

tootrigger hello CDN tooupdate sa version mise en cache, la purge hello CDN.

Dans hello portail de navigation gauche, sélectionnez **groupes de ressources**, puis sélectionnez le groupe de ressources hello que vous avez créé pour votre application web (myResourceGroup).

![Sélection du groupe de ressources](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

Dans la liste hello des ressources, sélectionnez votre point de terminaison CDN.

![Sélection du point de terminaison](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

En haut de hello Hello **point de terminaison** , cliquez sur **purger**.

![Sélection de l’option Vider](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

Entrez les chemins de contenu hello toopurge vous le souhaitez. Vous pouvez passer un toopurge de chemin d’accès complet du fichier, un fichier individuel ou un toopurge de segment de chemin d’accès et actualiser tout le contenu dans un dossier. Étant donné que vous avez modifié `index.html`, assurez-vous qu’est un des chemins d’accès hello.

Au bas de hello de page de hello, sélectionnez **purger**.

![Vidage de la page](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>Vérifiez que hello que CDN est mis à jour.

Attendez que la demande de vidage hello termine le traitement, en général de quelques minutes. état actuel toosee hello icône de cloche sélectionnez hello en hello haut hello. 

![Notification de vidage](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Parcourir les URL de point de terminaison CDN toohello pour `index.html`, et vous voyez à présent hello V2 que vous avez ajouté toohello titre sur la page d’accueil hello. Cela indique que le cache CDN hello a été actualisé.

```
http://<endpointname>.azureedge.net/index.html
```

![V2 dans le titre du CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

Pour plus d’informations, consultez [Purger un point de terminaison CDN Azure](../cdn/cdn-purge-endpoint.md). 

## <a name="use-query-strings-tooversion-content"></a>Utiliser le contenu de tooversion de chaînes de requête

Bonjour Azure CDN offre hello mise en cache des options de comportement suivantes :

* Ignorer les chaînes de requête
* Contourner la mise en cache pour les chaînes de requête
* Mettre en cache chaque URL unique 

Hello tout d’abord ces est par défaut hello, ce qui ne signifie qu’une version mise en cache d’un élément multimédia, quelle que soit la chaîne de requête hello hello URL. 

Dans cette section du didacticiel de hello, vous modifiez hello mise en cache de comportement toocache chaque URL unique.

### <a name="change-hello-cache-behavior"></a>Modifier le comportement de cache hello

Bonjour Azure portal **point de terminaison CDN** page, sélectionnez **Cache**.

Sélectionnez **mettre en Cache chaque URL unique** de hello **comportement de mise en cache de chaîne de requête** liste déroulante.

Sélectionnez **Enregistrer**.

![Sélection du comportement de mise en cache de chaîne de requête](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>Vérification de la mise en cache séparée des URL uniques

Dans un navigateur, accédez de page d’accueil toohello au point de terminaison CDN hello, mais inclure une chaîne de requête : 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

Hello CDN retourne hello web application contenu actuel, qui inclut « V2 » dans l’en-tête de hello. 

tooensure que cette page est mise en cache dans hello CDN, page hello d’actualisation. 

Ouvrez `index.html` et également de modifier « V2 » « V3 » et déployer les modifications de hello. 

```bash
git commit -am "version 3"
git push azure master
```

Dans un navigateur, accédez toohello URL de point de terminaison CDN avec une chaîne de requête, tel que `q=2`. Hello CDN obtient hello actuel `index.html` de fichiers et affiche « V3 ».  Toutefois, si vous accédez toohello point de terminaison CDN avec hello `q=1` chaîne de requête, vous voyez « V2 ».

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 dans le titre dans le CDN, chaîne de requête 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 dans le titre dans le CDN, chaîne de requête 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

Cette sortie montre que chaque chaîne de requête est traitée différemment :

* Comme la chaîne de requête q=1 a été utilisée précédemment, le contenu mis en cache est retourné (V2).
* q = 2 est nouvelle, afin de contenu application web plus récente de hello est récupérés et retournée (V3).

Pour plus d’informations, consultez [Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête](../cdn/cdn-query-string.md).

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>Mapper un point de terminaison CDN tooa domaine personnalisé

Vous allez mapper votre domaine personnalisé de tooyour point de terminaison CDN en créant un enregistrement CNAME. Un enregistrement CNAME est une fonctionnalité DNS qui mappe un domaine de destination de tooa de domaine source. Par exemple, vous pouvez mapper `cdn.contoso.com` ou `static.contoso.com` trop`contoso.azureedge.net`.

Si vous n’avez pas un domaine personnalisé, envisagez d’hello [didacticiel du domaine du Service d’applications](custom-dns-web-site-buydomains-web-app.md) toopurchase un domaine à l’aide de hello portail Azure. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>Rechercher toouse de nom d’hôte hello avec hello CNAME

Bonjour Azure portal **point de terminaison** , vérifiez que **vue d’ensemble** est sélectionné dans hello gauche de navigation, puis sélectionnez hello **+ un domaine personnalisé** bouton en hello haut hello.

![Sélection de l’ajout d’un domaine personnalisé](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

Bonjour **ajouter un domaine personnalisé** page, vous voyez hello point de terminaison hôte nom toouse pour la création d’un enregistrement CNAME. nom d’hôte Hello est dérivée de l’URL de point de terminaison CDN :  **&lt;EndpointName >. azureedge.net**. 

![Ajout d’une page de domaine](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>Configurer hello CNAME avec votre bureau d’enregistrement de domaine

Parcourir le site web de tooyour de domaines et recherchez la section hello pour la création d’enregistrements DNS. Vous pourrez trouver ces informations dans une section telle que **Domain Name**, **DNS** ou **Name Server Management**.

Rechercher la section de hello pour la gestion des enregistrements CNAME. Vous pouvez posséder de page de paramètres avancés de tooan toogo et recherchez les mots hello CNAME, Alias ou sous-domaines.

Créer un enregistrement CNAME qui mappe votre sous-domaine choisi (par exemple, **statique** ou **cdn**) toohello **nom d’hôte de point de terminaison** indiqué plus haut dans le portail de hello. 

### <a name="enter-hello-custom-domain-in-azure"></a>Entrez un domaine personnalisé de hello dans Azure

Retourner toohello **ajouter un domaine personnalisé** page et entrez votre domaine personnalisé, y compris les sous-domaine hello, dans la boîte de dialogue hello. Par exemple, entrez : `cdn.contoso.com`.   
   
Azure vérifie que l’enregistrement CNAME de hello existe pour le nom de domaine hello que vous avez entré. Si hello CNAME est correct, votre domaine personnalisé est validé.

Peut prendre du temps pour les serveurs de tooname toopropagate enregistrement hello CNAME sur hello Internet. Si votre domaine n’est pas validé immédiatement, patientez quelques minutes, puis réessayez.

### <a name="test-hello-custom-domain"></a>Domaine personnalisé hello de test

Dans un navigateur, accédez à toohello `index.html` de fichiers à l’aide de votre domaine personnalisé (par exemple, `cdn.contoso.com/index.html`) tooverify qui en résulte hello hello même que lorsque vous accédez directement trop`<endpointname>azureedge.net/index.html`.

![Page d’accueil d’exemple d’application utilisant l’URL du domaine personnalisé](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

Pour plus d’informations, consultez [domaine personnalisé de carte Azure CDN contenu tooa](../cdn/cdn-map-content-to-custom-domain.md).

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un point de terminaison CDN.
> * Actualiser les ressources mises en cache.
> * Utiliser la requête des chaînes de versions de toocontrol mis en cache.
> * Utilisez un domaine personnalisé pour le point de terminaison CDN hello.

Découvrez comment les articles de performances du CDN toooptimize Bonjour suivant :

> [!div class="nextstepaction"]
> [Compression des fichiers dans Azure CDN pour améliorer les performances](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Préchargement d’éléments multimédias sur un point de terminaison CDN Azure](../cdn/cdn-preload-endpoint.md)
