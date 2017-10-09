---
title: aaaConfigure SSL pour un service cloud (classiques) | Documents Microsoft
description: "Découvrez comment toospecify un point de terminaison HTTPS pour un rôle web et comment tooupload une connexion SSL certificat toosecure de votre application."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a>Configuration de SSL pour une application dans Azure
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-configure-ssl-certificate-portal.md)
> * [portail Azure Classic](cloud-services-configure-ssl-certificate.md)
> 
> 

Le chiffrement Secure Socket Layer (SSL) est la méthode hello couramment utilisé de la sécurisation des données envoyées sur hello internet. Cette tâche courante explique comment toospecify un point de terminaison HTTPS pour un rôle web et comment tooupload une connexion SSL certificat toosecure de votre application.

> [!NOTE]
> les procédures de Hello dans cette tâche s’appliquent les Services de cloud computing tooAzure ; pour les Services d’application, consultez [cela](../app-service-web/web-sites-configure-ssl-certificate.md) l’article.
> 
> 

Cette tâche utilise un déploiement de production. Vous trouverez des informations sur l’utilisation d’un déploiement intermédiaire à fin hello de cette rubrique.

Lisez tout d’abord [cet](cloud-services-how-to-create-deploy.md) article si vous n’avez pas encore créé de service cloud.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Étape 1 : obtention d’un certificat SSL
tooconfigure SSL pour une application, vous devez tout d’abord tooget un certificat SSL qui a été signé par un certificat autorité (CA), un tiers de confiance qui émet des certificats à cet effet. Si vous n’en avez pas déjà, vous devez tooobtain une à partir d’une société qui vend des certificats SSL.

certificat de Hello doit respecter hello suivant les exigences pour les certificats SSL dans Azure :

* certificat de Hello doit contenir une clé privée.
* certificat de Hello doit être créé pour l’échange de clés, exportable tooa fichier d’échange d’informations personnelles (.pfx).
* Hello nom du sujet du certificat doit correspondre au service de cloud hello domaine utilisé tooaccess hello. Impossible d’obtenir un certificat SSL à partir d’une autorité de certification (CA) pour le domaine cloudapp.net de hello. Vous devez vous procurer un toouse de nom de domaine personnalisé lorsque accéder à votre service. Lorsque vous demandez un certificat à partir d’une autorité de certification, nom du sujet du certificat hello doit correspondre à hello domaine personnalisé nom utilisé tooaccess votre application. Par exemple, si votre nom de domaine personnalisé est **contoso.com**, vous demandez un certificat auprès de votre autorité de certification pour **.contoso.com** ou **www.contoso.com**.
* certificat de Hello doit utiliser un minimum de chiffrement de 2048 bits.

Dans le cadre d’un test, vous pouvez [créer](cloud-services-certs-create.md) et utiliser un certificat auto-signé. Un certificat auto-signé n’est pas authentifié par une autorité de certification et pouvez utiliser le domaine cloudapp.net de hello en tant qu’URL du site Web hello. Par exemple, hello tâche suivante utilise un certificat auto-signé qui Bonjour nom commun (CN) utilisé dans le certificat de hello est **sslexample.cloudapp.net**.

Ensuite, vous devez inclure plus d’informations sur les certificats hello dans votre définition de service et les fichiers de configuration de service.

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>Étape 2 : Modifier les fichiers de définition et de configuration de service hello
Votre application doit être configuré toouse hello et un point de terminaison HTTPS doit être ajouté. Par conséquent, hello définition de service et les fichiers de configuration de service doivent toobe mis à jour.

1. Dans votre environnement de développement, ouvrez le fichier de définition de service (CSDEF) hello, ajoutez un **certificats** section hello **WebRole** section et inclure hello informations suivantes le certificat (et les certificats intermédiaires) :
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   Hello **certificats** section définit le nom hello de notre certificat, son emplacement et le nom de hello du magasin hello où il se trouve.
   
   Autorisations (`permisionLevel` attribut) peut être tooone de jeu de hello valeurs suivantes :
   
   | Valeur de l’autorisation | Description |
   | --- | --- |
   | limitedOrElevated |**(Par défaut)**  Tous les processus de rôle peuvent accéder à clé privée de hello. |
   | elevated |Seuls les processus élevés peuvent accéder à clé privée de hello. |
2. Dans votre fichier de définition de service, ajoutez un **InputEndpoint** élément hello **points de terminaison** section tooenable HTTPS :
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443" 
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. Dans votre fichier de définition de service, ajoutez un **liaison** élément hello **Sites** section. Cette section permet d’ajouter un toomap de liaison du site tooyour de point de terminaison HTTPS :
   
    ```xml   
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```
   
   Tous les fichier de définition de service de toohello de modifications requises de hello ont été effectuées, mais vous devez toujours des informations de certificat hello tooadd au fichier de configuration de service hello.
4. Dans votre fichier de configuration service (CSCFG), ServiceConfiguration.Cloud.cscfg, ajoutez un **certificats** section hello **rôle** section, en remplaçant la valeur d’empreinte numérique exemple hello ci-dessous avec celui de votre certificat :
   
    ```xml   
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff" 
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc" 
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

(hello précédant l’exemple suivant utilise **sha1** pour l’algorithme d’empreinte numérique hello. Spécifiez la valeur appropriée de hello pour l’algorithme d’empreinte numérique de votre certificat.)

Maintenant que les fichiers de configuration des service et de définition de hello service ont été mis à jour, votre déploiement pour le téléchargement tooAzure du package. Si vous utilisez **cspack**, n’utilisez pas l’indicateur **/generateConfigurationFile**, car les informations de certificat que vous venez d’entrer seraient écrasées.

## <a name="step-3-upload-a-certificate"></a>Étape 3 : chargement d’un certificat
Votre package de déploiement a été le certificat de hello toouse mis à jour, et un point de terminaison HTTPS a été ajoutée. Vous pouvez maintenant télécharger tooAzure de package et de certificat hello avec hello portail Azure classic.

1. Connectez-vous à toohello [portail Azure classic][Azure classic portal]. 
2. Cliquez sur **Services de cloud computing** sur le volet de navigation de gauche hello.
3. Cliquez sur le service de cloud computing hello souhaité.
4. Cliquez sur hello **certificats** onglet.
   
    ![Cliquez sur onglet de certificats hello](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. Cliquez sur hello **télécharger** bouton.
   
    ![Télécharger](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. Fournir hello **fichier**, **mot de passe**, puis cliquez sur **Complete** (hello coche).

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Étape 4 : Connecter l’instance de rôle toohello à l’aide de HTTPS
Maintenant que votre déploiement est en cours d’exécution dans Azure, vous pouvez vous connecter tooit à l’aide de HTTPS.

1. Dans hello portail Azure classic, sélectionnez votre déploiement, puis cliquez sur lien hello sous **URL du Site**.
   
   ![Déterminer l'URL du site][2]
2. Dans votre navigateur web, modifiez hello lien toouse **https** au lieu de **http**, puis consultez la page de hello.
   
   > [!NOTE]
   > Si vous utilisez un certificat auto-signé, lorsque vous parcourez tooan point de terminaison HTTPS a associé à un certificat auto-signé de hello, vous voyez une erreur de certificat dans le navigateur de hello. À l’aide d’un certificat signé par une autorité de certification approuvée élimine le problème ; Bonjour attendant, vous pouvez ignorer les erreurs hello. (Une autre option consiste à magasin Autorités de certification approuvée de certificat d’utilisateur toohello tooadd hello certificat auto-signé.)
   > 
   > 
   
   ![Exemple de site Web SSL][3]

Si vous souhaitez toouse SSL pour un déploiement intermédiaire au lieu d’un déploiement de production, vous devez d’abord les URL de hello toodetermine utilisée pour le déploiement intermédiaire de hello. Déployez votre environnement intermédiaire de cloud service toohello sans inclure un certificat ou toutes les informations de certificat. Une fois déployé, vous pouvez déterminer les URL de type GUID hello, qui est répertoriée dans hello portail Azure classic **URL du Site** champ. Créez un certificat avec hello courantes URL basée sur le GUID de nom (CN) égal toohello (par exemple, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**). Utilisez hello tooadd de portail classique Azure hello certificat tooyour mises en lots de service cloud. Ensuite, ajoutez hello informations tooyour CSDEF et CSCFG fichiers de certificat, réorganiser votre application et mettre à jour votre déploiement intermédiaire toouse hello nouveau package.

## <a name="next-steps"></a>Étapes suivantes
* [Configuration générale de votre service cloud](cloud-services-how-to-configure.md).
* Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy.md).
* Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name.md).
* [Gérez votre service cloud](cloud-services-how-to-manage.md).

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
