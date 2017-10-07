---
title: "aaaGetting main d’Azure CDN | Documents Microsoft"
description: "Cette rubrique montre comment tooenable hello Azure réseau CDN (Content Delivery). didacticiel de Hello Guide de création de hello d’un nouveau profil CDN et du point de terminaison."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Prise en main d’Azure CDN
Cette rubrique décrit l’activation d’Azure CDN en créant un nouveau profil CDN et un point de terminaison.

> [!IMPORTANT]
> Pour un fonctionnement du CDN toohow introduction, ainsi que d’une liste des fonctionnalités, consultez hello [vue d’ensemble du CDN](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Créer un profil CDN
Un profil CDN est une collection de points de terminaison CDN.  Chaque profil contient un ou plusieurs points de terminaison CDN.  Vous souhaiterez peut-être toouse plusieurs profils tooorganize vos points de terminaison CDN par domaine internet, application web ou d’autres critères.

> [!NOTE]
> Par défaut, un seul abonnement Azure est profils CDN tooeight limité. Chaque profil CDN est limitée tooten points de terminaison CDN.
> 
> Tarification du CDN est appliquée au niveau de profil CDN hello. Si vous souhaitez toouse un mélange d’Azure CDN niveaux tarifaires, vous devez plusieurs profils CDN.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Créer un point de terminaison CDN
**toocreate un nouveau point de terminaison CDN**

1. Bonjour [Azure Portal](https://portal.azure.com), accédez tooyour le profil CDN.  Vous pouvez avoir épinglée toohello le tableau de bord à l’étape précédente de hello.  Si vous ne vous le trouverez en cliquant sur **Parcourir**, puis **profils CDN**, et en cliquant sur le profil de hello vous prévoyez de tooadd votre point de terminaison.
   
    Panneau de profil CDN Hello s’affiche.
   
    ![Profil CDN][cdn-profile-settings]
2. Cliquez sur hello **ajouter le point de terminaison** bouton.
   
    ![Bouton Ajouter un point de terminaison][cdn-new-endpoint-button]
   
    Hello **ajouter un point de terminaison** panneau s’affiche.
   
    ![Panneau Ajouter un point de terminaison][cdn-add-endpoint]
3. Entrez un **nom** pour ce point de terminaison CDN.  Ce nom sera utilisé tooaccess vos ressources mises en cache au niveau du domaine de hello `<endpointname>.azureedge.net`.
4. Bonjour **type d’origine** liste déroulante, sélectionnez votre type d’origine.  Sélectionnez **Stockage** pour un compte de stockage Azure, **Service cloud** pour un service cloud Azure, **Application web** pour une application web Azure ou **Origine personnalisée** pour toute autre origine de serveur web accessible publiquement (hébergé dans Azure ou ailleurs).
   
    ![Type d'origine CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. Bonjour **nom d’hôte d’origine** liste déroulante, sélectionnez ou tapez votre domaine d’origine.  liste déroulante de Hello répertorie toutes les origines disponibles de type hello spécifié à l’étape 4.  Si vous avez sélectionné *origine du personnalisé* en tant que votre **type d’origine**, vous allez taper dans le domaine hello de votre origine personnalisée.
6. Bonjour **chemin d’origine** texte, entrez hello chemin d’accès toohello ressources toocache, ou laissez vide tooallow cache n’importe quelle ressource au niveau domaine hello spécifié à l’étape 5.
7. Bonjour **en-tête hôte d’origine**, entrez l’en-tête d’hôte hello souhaité hello toosend CDN avec chaque demande, ou laissez hello par défaut.
   
   > [!WARNING]
   > Certains types d’origines, telles que le stockage Azure et les applications Web requièrent hello hôte en-tête toomatch hello domaine d’origine de hello. À moins d’avoir une origine nécessitant un en-tête d’hôte différent de son domaine, vous devez laisser la valeur par défaut de hello.
   > 
   > 
8. Pour **protocole** et **port d’origine**, spécifier hello protocoles et ports utilisés tooaccess vos ressources à l’origine de hello.  Vous devez sélectionner au moins un protocole (HTTP ou HTTPS).
   
   > [!NOTE]
   > Hello **port d’origine** affecte uniquement le point de terminaison hello port utilise les informations de tooretrieve à partir de l’origine de hello.  Hello point de terminaison lui-même sera disponible tooend clients hello par défaut ports HTTP et HTTPS (80 et 443), quel que soit hello **port d’origine**.  
   > 
   > **CDN Azure à partir d’Akamai** points de terminaison n’autorisent pas de plage de ports TCP complète hello pour les origines.  Pour obtenir la liste des ports d’origine non autorisés, consultez l’article [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Ports d’origine autorisés du CDN Azure fourni par Akamai).  
   > 
   > L’accès à CDN contenu à l’aide de HTTPS a hello suivant des contraintes :
   > 
   > * Vous devez utiliser le certificat SSL de hello fournie par hello CDN. Les certificats tiers ne sont pas pris en charge.
   > * Vous devez utiliser le domaine CDN autant de hello (`<endpointname>.azureedge.net`) le contenu tooaccess HTTPS. Prise en charge HTTPS n’est pas disponible pour les noms de domaines personnalisés (enregistrements CNAME) hello CDN ne prenant pas en charge les certificats personnalisés pour l’instant.
   > 
   > 
9. Cliquez sur hello **ajouter** bouton toocreate hello nouveau point de terminaison.
10. Une fois que le point de terminaison hello est créé, il apparaît dans une liste de points de terminaison pour le profil de hello. Hello liste affiche hello URL toouse tooaccess mis en cache le contenu, ainsi que le domaine d’origine hello.
    
    ![Point de terminaison CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > point de terminaison Hello pas immédiatement sera disponible pour une utilisation, comme le temps requis pour toopropagate d’inscription hello via hello CDN.  Pour <b>Azure CDN fourni par Akamai</b> , la propagation s’effectue généralement dans un délai d’une minute.  Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.
    > 
    > Les utilisateurs qui essaient de nom de domaine CDN toouse hello avant la configuration de point de terminaison hello a propagé toohello POP recevront des codes de réponse HTTP 404.  Si plusieurs heures se sont écoulées depuis la création de votre point de terminaison et que vous recevez toujours des réponses 404, consultez [Dépannage des points de terminaison de CDN renvoyant des états 404](cdn-troubleshoot-endpoint.md).
    > 
    > 

## <a name="see-also"></a>Voir aussi
* [Contrôle du comportement de mise en cache des demandes avec des chaînes de requête](cdn-query-string.md)
* [Comment tooa de contenu CDN tooMap un domaine personnalisé](cdn-map-content-to-custom-domain.md)
* [Préchargement d’éléments multimédias sur un point de terminaison CDN Azure](cdn-preload-endpoint.md)
* [Purger un point de terminaison CDN Azure](cdn-purge-endpoint.md)
* [Dépannage des points de terminaison de CDN renvoyant des états 404](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
