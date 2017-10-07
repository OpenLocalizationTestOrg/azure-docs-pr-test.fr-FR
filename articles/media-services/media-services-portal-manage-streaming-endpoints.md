---
title: aaaManage de diffusion en continu des points de terminaison avec hello portail Azure | Documents Microsoft
description: Cette rubrique montre comment les points de terminaison de diffusion en continu toomanage avec hello portail Azure.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Gérer les points de terminaison de diffusion en continu avec hello portail Azure

Cette rubrique montre comment toouse hello toomanage portail Azure les points de terminaison de diffusion en continu. 

>[!NOTE]
>Assurez-vous que tooreview hello [vue d’ensemble](media-services-streaming-endpoints-overview.md) rubrique. 

Pour plus d’informations sur la façon dont tooscale hello point de terminaison de diffusion en continu, consultez [cela](media-services-portal-scale-streaming-endpoints.md) rubrique.

## <a name="start-managing-streaming-endpoints"></a>Commencer à gérer des points de terminaison de streaming 

toostart la gestion des points de terminaison de diffusion en continu de votre compte, procédez comme hello suivant.

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Bonjour **paramètres** panneau, sélectionnez **points de terminaison de diffusion en continu**.
   
    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> Vous êtes facturé uniquement lorsque votre point de terminaison de streaming est en cours d’exécution.

## <a name="adddelete-a-streaming-endpoint"></a>Ajouter/supprimer un point de terminaison de streaming

>[!NOTE]
>point de terminaison de diffusion en continu de la valeur par défaut Hello ne peut pas être supprimé.

à l’aide du point de terminaison de diffusion en continu tooadd/delete hello portail Azure, procédez comme hello suivant :

1. tooadd un point de terminaison de diffusion en continu, cliquez sur hello **+ point de terminaison** en hello haut hello. 

    Vous pourriez plusieurs points de terminaison de diffusion en continu si vous envisagez de toohave CDN différents ou un CDN et un accès direct.

2. toodelete un point de terminaison de diffusion en continu, appuyez sur **supprimer** bouton.      
3. Cliquez sur hello **Démarrer** hello toostart de bouton point de terminaison de diffusion en continu.
   
    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Configuration de point de terminaison de diffusion en continu de hello
Point de terminaison de diffusion en continu vous permet de hello tooconfigure propriétés suivantes :

* Contrôle d’accès
* Contrôle de cache
* Stratégies d’accès intersite

Pour plus d’informations sur ces propriétés, consultez la rubrique [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).

Vous pouvez configurer le point de terminaison de diffusion en continu de manière hello suivante :

1. Sélectionnez hello point de terminaison de tooconfigure de diffusion en continu.
2. Cliquez sur **Settings**.

Une brève description des champs de hello suit.

![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. Stratégie de cache maximale : tooconfigure utilisés de vie du cache pour les ressources servies par ce point de terminaison de diffusion en continu. Si aucune valeur n’est définie, la valeur par défaut hello est utilisé. valeurs par défaut de Hello peuvent également être définies directement dans le stockage Azure. Si Azure CDN est activé pour le point de terminaison de diffusion en continu de hello, vous ne devez pas définir accessible sans hello cache stratégie valeur de 600 secondes.  
2. Adresses IP autorisées : les adresses IP toospecify qui sont autorisées tooconnect toohello publié le point de terminaison de diffusion en continu utilisées. Si aucune adresse IP n’est spécifié, n’importe quelle adresse IP est tooconnect en mesure de. Les adresses IP peuvent être définies sous forme d’adresse IP unique (par exemple, « 10.0.0.1 »), de plage d’adresses IP constituée d’une adresse IP et d’un masque de sous-réseau CIDR (par exemple, « 10.0.0.1/22 ») ou de plage d’adresses IP constituée d’une adresse IP et d’un masque de sous-réseau au format décimal séparé par des points (par exemple, « 10.0.0.1(255.255.255.0) »).
3. Configuration pour l’authentification d’en-tête de signature Akamai : utilisé toospecify configuration de la demande d’authentification de signature en-tête à partir de serveurs Akamai. L’expiration est au format UTC.

## <a name="scale-your-premium-streaming-endpoint"></a>Mise à l’échelle du point de terminaison de streaming Premium

Pour plus d’informations, consultez [cette rubrique](media-services-portal-scale-streaming-endpoints.md) .

## <a id="enable_cdn"></a>Activer l’intégration au CDN Azure

Lorsque vous créez un compte, l’intégration CDN Azure du point de terminaison de streaming par défaut est activée par défaut.

Si vous souhaitez ultérieurement toodisable/activer hello CDN, votre point de terminaison de diffusion en continu doit être Bonjour **arrêté** état. Peut prendre les heures too2 pour tooget de l’intégration d’Azure CDN hello activé et hello toobe de modifications actif sur tous les hello POP du CDN. Toutefois, vous pouvez démarrer votre point de terminaison et les flux sans interruptions de diffusion en continu à partir du point de terminaison de diffusion en continu de hello et une fois qu’integration de hello est terminée, les flux hello seront remis à partir de hello CDN. Au cours de hello période de mise en service votre point de terminaison de diffusion en continu sera dans **démarrage** état et que vous pouvez observer les performances de degredad.

Intégration de CDN est activée dans tous les execpt de centres de données Azure hello en Chine et régions du gouvernement fédéral.

Une fois qu’elle est activée, hello **le contrôle d’accès**, **nom d’hôte personnalisé** et **l’authentification de Akamai Signature** configuration obtient désactivée.
 
> [!IMPORTANT]
> L’intégration d’Azure Media Services au CDN Azure est implémentée sur le **CDN Azure fourni par Verizon** pour les points de terminaison de streaming Standard. Les points de terminaison de streaming Premium peuvent être configurés à l’aide de l’ensemble des **fournisseurs et niveaux de tarification Azure CDN**. Pour plus d’informations sur les fonctionnalités d’Azure CDN, consultez hello [vue d’ensemble CDN](../cdn/cdn-overview.md).
 
### <a name="additional-considerations"></a>Considérations supplémentaires

* Si le CDN est activé pour un point de terminaison de diffusion en continu, les clients ne peuvent pas demandent du contenu directement à partir de l’origine de hello. Si vous devez hello capacité tootest votre contenu avec ou sans CDN, vous pouvez créer un autre point de terminaison diffusion en continu qui n’est pas de CDN activé.
* Votre diffusion en continu reste de nom d’hôte de point de terminaison hello même après l’activation du CDN. Vous n’avez pas besoin toomake n’importe quel flux de travail de modifications tooyour media services une fois que le CDN est activé. Par exemple, si votre nom d’hôte du point de terminaison diffusion en continu est strasbourg.streaming.mediaservices.windows.net, après avoir activé le CDN, hello exacte même nom d’hôte est utilisé.
* Pour les nouveaux points de terminaison de diffusion en continu, vous pouvez activer CDN simplement par la création d’un point de terminaison ; pour les points de terminaison de diffusion en continu existants, vous avez besoin de point de terminaison hello toofirst arrêter, puis sur Activer/désactiver hello CDN.
* Le point de terminaison de streaming Standard ne peut être configuré qu’à l’aide du **fournisseur CDN Standard Verizon** par le biais du portail de gestion Azure. Toutefois, vous pouvez activer d’autres fournisseurs Azure CDN à l’aide d’API REST.

## <a name="configure-cdn-profile"></a>Configurer le profil CDN

Vous pouvez configurer le profil CDN hello en sélectionnant hello **gérer le CDN** bouton à partir du haut de hello.

![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>Étapes suivantes
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

