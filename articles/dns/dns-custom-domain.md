---
title: aaaIntegrate DNS Azure avec vos ressources Azure | Documents Microsoft
description: "Découvrez comment toouse Azure DNS le long de tooprovide DNS pour vos ressources Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Utiliser les paramètres de domaine personnalisé tooprovide Azure DNS pour un service Azure

DNS Azure fournit un DNS pour un domaine personnalisé, pour toutes vos ressources Azure prenant en charge les domaines personnalisés ou ayant un nom de domaine complet (FQDN). Vous disposez d’une application web Azure et que vous souhaitez que vos utilisateurs tooaccess en l’utilisant contoso.com ou www.contoso.com comme nom de domaine complet. Cet article vous guide tout au long de la configuration de votre service Azure avec DNS Azure pour l’utilisation de domaines personnalisés.

## <a name="prerequisites"></a>Composants requis

Dans l’ordre toouse Azure DNS pour votre domaine personnalisé, vous devez tout d’abord déléguer votre tooAzure de domaine DNS. Visitez [déléguer un tooAzure de domaine DNS](./dns-delegate-domain-azure-dns.md) pour obtenir des instructions sur la façon de tooconfigure vos serveurs de noms pour la délégation. Une fois votre domaine délégué tooyour Azure Directory, vous êtes tooconfigure en mesure des enregistrements DNS hello si nécessaires.

Vous pouvez configurer un domaine personnalisé pour [Applications Azure Function](#azure-function-app), [Azure IoT](#azure-iot), [Adresses IP publiques](#public-ip-address), [App Service (Web Apps)](#app-service-web-apps), [Stockage Blob](#blob-storage) et [Azure CDN](#azure-cdn).

## <a name="azure-function-app"></a>Application Azure Function

tooconfigure un domaine personnalisé pour les applications de la fonction Azure, un enregistrement CNAME est créé, ainsi que la configuration de l’application de fonction hello proprement dit.
 
Accédez trop**autres** > **fonction application** et sélectionnez votre application de la fonction. Cliquez sur **Fonctionnalités de la plateforme**, puis, sous **MISE EN RÉSEAU**, cliquez sur **Domaines personnalisés**.

![Panneau d’application de fonction](./media/dns-custom-domain/functionapp.png)

Notez les url actuelle du hello sur hello **les domaines personnalisés** panneau, cette adresse est utilisé comme alias de hello pour hello un enregistrement DNS créé.

![Panneau de domaine personnalisé](./media/dns-custom-domain/functionshostname.png)

Déplacer la Zone DNS de tooyour, cliquez sur **+ enregistrer ensemble**. Remplir hello suivant les informations de hello **ajouter le jeu d’enregistrements** panneau, cliquez sur **OK** toocreate il.

|Propriété  |Valeur  |Description  |
|---------|---------|---------|
|Nom     | myFunctionApp        | Cette valeur, ainsi que l’étiquette de nom de domaine hello est hello nom de domaine complet pour le nom de domaine personnalisé hello.        |
|Type     | CNAME        | Utiliser un enregistrement CNAME équivaut à utiliser un alias.        |
|TTL     | 1        | 1 est utilisé pour 1 heure        |
|Unité de durée de vie     | Heures        | Heures sont utilisées en tant que mesure de temps hello         |
|Alias     | adatumfunction.azurewebsites.net        | nom DNS de Hello vous créez des alias de hello, dans cet exemple, il s’agit hello adatumfunction.azurewebsites.net DNS nom fourni par l’application de fonction toohello par défaut.        |

Accédez d’application de fonction tooyour précédent, cliquez sur **fonctionnalités de plateforme**et sous **mise en réseau** cliquez sur **les domaines personnalisés**, puis sous **lesnomsd’hôte**cliquez sur **+ ajouter un nom d’hôte**.

Sur hello **ajouter le nom d’hôte** panneau, entrez l’enregistrement CNAME de hello Bonjour **nom d’hôte** champ de texte et cliquez sur **Validate**. Si l’enregistrement de hello a été en mesure de toobe trouvé, hello **ajouter le nom d’hôte** bouton s’affiche. Cliquez sur **ajouter le nom d’hôte** alias de hello tooadd.

![Panneau Ajouter un nom d’hôte pour application de fonction](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>Azure IoT

Azure IoT ne dispose pas de toutes les personnalisations qui sont requis par le service hello proprement dit. toouse un domaine personnalisé avec un IoT Hub uniquement un enregistrement CNAME pointe toohello ressources est nécessaire.

Accédez trop**Internet of Things** > **IoT Hub** et sélectionnez votre hub IoT. Sur hello **vue d’ensemble** panneau, hello de Remarque FQDN du hub IoT de hello.

![Panneau IoT Hub](./media/dns-custom-domain/iot.png)

Ensuite, accédez de Zone DNS de tooyour et cliquez sur **+ enregistrer ensemble**. Remplir hello suivant les informations de hello **ajouter le jeu d’enregistrements** panneau, cliquez sur **OK** toocreate il.


|Propriété  |Valeur  |Description  |
|---------|---------|---------|
|Nom     | myiothub        | Cette valeur, ainsi que l’étiquette de nom de domaine hello est hello nom de domaine complet pour le hub IoT de hello.        |
|Type     | CNAME        | Utiliser un enregistrement CNAME équivaut à utiliser un alias.
|TTL     | 1        | 1 est utilisé pour 1 heure        |
|Unité de durée de vie     | Heures        | Heures sont utilisées en tant que mesure de temps hello         |
|Alias     | adatumIOT.azure-devices.net        | nom DNS de Hello vous créez des alias de hello, dans cet exemple, il est le nom d’hôte adatumIOT.azure-devices.net hello fournie par hello IoT hub.

Une fois l’enregistrement de hello est créé, tester la résolution de nom avec l’utilisation de l’enregistrement CNAME de hello`nslookup`

## <a name="public-ip-address"></a>Adresse IP publique

tooconfigure un domaine personnalisé pour les services qui utilisent une adresse IP publique résoudre des ressources tels que Service Cloud passerelle d’Application, l’équilibrage de charge, les machines virtuelles Resource Manager, et, les machines virtuelles classique, un enregistrement CNAME est utilisé.

Accédez trop**réseau** > **adresse IP publique**, sélectionnez la ressource d’adresse IP publique hello et cliquez sur **Configuration**. Notez l’adresse IP de hello indiqué.

![Panneau Adresse IP publique](./media/dns-custom-domain/publicip.png)

Déplacer la Zone DNS de tooyour, cliquez sur **+ enregistrer ensemble**. Remplir hello suivant les informations de hello **ajouter le jeu d’enregistrements** panneau, cliquez sur **OK** toocreate il.


|Propriété  |Valeur  |Description  |
|---------|---------|---------|
|Nom     | mywebserver        | Cette valeur, ainsi que l’étiquette de nom de domaine hello est hello nom de domaine complet pour le nom de domaine personnalisé hello.        |
|Type     | A        | Utiliser un enregistrement A comme ressource de hello est une adresse IP.        |
|TTL     | 1        | 1 est utilisé pour 1 heure        |
|Unité de durée de vie     | Heures        | Heures sont utilisées en tant que mesure de temps hello         |
|Adresse IP     | <your ip address>       | adresse IP publique de Hello.|

![Créer un enregistrement A](./media/dns-custom-domain/arecord.png)

Une fois que hello un enregistrement est créé, exécutez `nslookup` toovalidate hello enregistrement résolu.

![Recherche DNS d’adresse IP publique](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>App Service (Web Apps)

Hello étapes suivantes vous guident pour configurer un domaine personnalisé pour une application de service d’applications web.

Accédez trop**Web et Mobile** > **du Service d’applications** et sélectionnez hello ressource que vous configurez un nom de domaine personnalisé, puis cliquez sur **les domaines personnalisés**.

Notez les url actuelle du hello sur hello **les domaines personnalisés** panneau, cette adresse est utilisé comme alias de hello pour hello un enregistrement DNS créé.

![Panneau Domaines personnalisés](./media/dns-custom-domain/url.png)

Déplacer la Zone DNS de tooyour, cliquez sur **+ enregistrer ensemble**. Remplir hello suivant les informations de hello **ajouter le jeu d’enregistrements** panneau, cliquez sur **OK** toocreate il.


|Propriété  |Valeur  |Description  |
|---------|---------|---------|
|Nom     | mywebserver        | Cette valeur, ainsi que l’étiquette de nom de domaine hello est hello nom de domaine complet pour le nom de domaine personnalisé hello.        |
|Type     | CNAME        | Utiliser un enregistrement CNAME équivaut à utiliser un alias. Si les ressources hello utilisé une adresse IP, un enregistrement A est utilisé.        |
|TTL     | 1        | 1 est utilisé pour 1 heure        |
|Unité de durée de vie     | Heures        | Heures sont utilisées en tant que mesure de temps hello         |
|Alias     | webserver.azurewebsites.net        | nom DNS de Hello vous créez des alias de hello, dans cet exemple, il est le nom DNS de hello webserver.azurewebsites.net fournie par l’application web par défaut toohello.        |


![Créer un enregistrement CNAME](./media/dns-custom-domain/createcnamerecord.png)

Accédez toohello différé du service d’applications qui est configuré pour le nom de domaine personnalisé hello. Cliquez sur **Domaines personnalisés**, puis sur **Noms d’hôte**. enregistrement CNAME de hello tooadd que vous avez créé, cliquez sur **+ ajouter un nom d’hôte**.

![figure 1](./media/dns-custom-domain/figure1.png)

Une fois que hello est terminée, exécutez **nslookup** toovalidate la résolution de noms fonctionne.

![figure 1](./media/dns-custom-domain/finalnslookup.png)

toolearn en savoir plus sur le mappage d’un domaine personnalisé de tooApp Service, visitez [mapper un tooAzure de nom DNS personnalisé existant Web Apps](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).

Si vous avez besoin de toopurchase un domaine personnalisé, visitez [acheter un nom de domaine personnalisé pour les applications Web Azure](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn plus d’informations sur les domaines de Service d’applications.

## <a name="blob-storage"></a>Stockage d'objets blob

Hello étapes suivantes vous guident tout configurer un enregistrement CNAME pour un compte de stockage d’objets blob à l’aide de la méthode d’asverify hello. Cette méthode garantit l’absence de temps d’arrêt.

Accédez trop**stockage** > **comptes de stockage**, sélectionnez votre compte de stockage, puis cliquez sur **un domaine personnalisé**. Inscrire le nom de domaine complet de hello sous l’étape 2, cette valeur est utilisée toocreate hello premier CNAME enregistrement

![Domaine personnalisé de stockage BLOB](./media/dns-custom-domain/blobcustomdomain.png)

Déplacer la Zone DNS de tooyour, cliquez sur **+ enregistrer ensemble**. Remplir hello suivant les informations de hello **ajouter le jeu d’enregistrements** panneau, cliquez sur **OK** toocreate il.


|Propriété  |Valeur  |Description  |
|---------|---------|---------|
|Nom     | asverify.mystorageaccount        | Cette valeur, ainsi que l’étiquette de nom de domaine hello est hello nom de domaine complet pour le nom de domaine personnalisé hello.        |
|Type     | CNAME        | Utiliser un enregistrement CNAME équivaut à utiliser un alias.        |
|TTL     | 1        | 1 est utilisé pour 1 heure        |
|Unité de durée de vie     | Heures        | Heures sont utilisées en tant que mesure de temps hello         |
|Alias     | asverify.adatumfunctiona9ed.blob.core.windows.net        | nom DNS de Hello vous créez des alias de hello, dans cet exemple, il s’agit hello asverify.adatumfunctiona9ed.blob.core.windows.net DNS nom fourni par le compte de stockage toohello par défaut.        |

Accédez de compte de stockage tooyour arrière en cliquant sur **stockage** > **comptes de stockage**, sélectionnez votre compte de stockage, cliquez sur **un domaine personnalisé**. Type Bonjour alias que vous avez créé sans préfixe d’asverify hello dans la zone de texte hello, cocher ** la validation CNAME indirecte, puis cliquez sur **enregistrer**. Une fois cette étape terminée, renvoyer la zone DNS de tooyour et créer un enregistrement CNAME sans préfixe d’asverify hello.  Une fois à ce stade, vous êtes enregistrement CNAME hello toodelete sécurisée avec le préfixe de cdnverify hello.

![Domaine personnalisé de stockage BLOB](./media/dns-custom-domain/indirectvalidate.png)

Validez la résolution DNS en exécutant `nslookup`.

toolearn plus sur le mappage d’un point de terminaison du stockage d’objets blob tooa domaine personnalisé, visitez [configurer un nom de domaine personnalisé pour votre point de terminaison de stockage d’objets Blob](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>Azure CDN

Hello étapes suivantes vous guident tout configurer un enregistrement CNAME pour un point de terminaison CDN à l’aide de la méthode de cdnverify hello. Cette méthode garantit l’absence de temps d’arrêt.

Accédez trop**réseau** > **CDN profils**, sélectionnez votre profil CDN, cliquez sur **points de terminaison** sous **général**.

Sélectionner le point de terminaison hello vous travaillez, cliquez sur **+ un domaine personnalisé**. Hello de note **nom d’hôte du point de terminaison** que cette valeur est hello cet enregistrement CNAME de hello pointe vers.

![Domaine personnalisé du CDN](./media/dns-custom-domain/endpointcustomdomain.png)

Déplacer la Zone DNS de tooyour, cliquez sur **+ enregistrer ensemble**. Remplir hello suivant les informations de hello **ajouter le jeu d’enregistrements** panneau, cliquez sur **OK** toocreate il.

|Propriété  |Valeur  |Description  |
|---------|---------|---------|
|Nom     | cdnverify.mycdnendpoint        | Cette valeur, ainsi que l’étiquette de nom de domaine hello est hello nom de domaine complet pour le nom de domaine personnalisé hello.        |
|Type     | CNAME        | Utiliser un enregistrement CNAME équivaut à utiliser un alias.        |
|TTL     | 1        | 1 est utilisé pour 1 heure        |
|Unité de durée de vie     | Heures        | Heures sont utilisées en tant que mesure de temps hello         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.net        | nom DNS de Hello vous créez des alias de hello, dans cet exemple, il s’agit hello cdnverify.adatumcdnendpoint.azureedge.net DNS nom fourni par le compte de stockage toohello par défaut.        |

Accédez de point de terminaison CDN tooyour arrière en cliquant sur **réseau** > **CDN profils**, puis sélectionnez votre profil CDN. Cliquez sur **+ un domaine personnalisé** et entrez votre alias d’enregistrement CNAME sans préfixe de cdnverify hello, puis cliquez sur **ajouter**.

Une fois cette étape terminée, renvoyer la zone DNS de tooyour et créer un enregistrement CNAME sans préfixe de cdnverify hello.  Une fois à ce stade, vous êtes enregistrement CNAME hello toodelete sécurisée avec le préfixe de cdnverify hello. Pour plus d’informations sur le CDN et comment tooconfigure un domaine personnalisé sans étape d’inscription intermédiaire de hello visitez [domaine personnalisé de carte Azure CDN contenu tooa](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[configurer DNS inverse pour les services hébergés dans Azure](dns-reverse-dns-for-azure-services.md).
