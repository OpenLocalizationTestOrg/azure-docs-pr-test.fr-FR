---
title: "aaaAzure Service Fabric avec le démarrage rapide de gestion des API | Documents Microsoft"
description: "Ce guide vous explique comment démarrer avec l’API de gestion et Azure Service Fabric tooquickly."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Azure Service Fabric avec Gestion des API - Démarrage rapide

Ce guide vous explique comment tooset jusqu'à la gestion des API Azure avec l’infrastructure de Service et configurer des votre première API opération toosend trafic tooback services en Service fabric. toolearn en savoir plus sur les scénarios de gestion des API Azure avec l’infrastructure de Service, consultez hello [vue d’ensemble](service-fabric-api-management-overview.md) l’article. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>Déployer tooAzure gestion des API et le Service Fabric

première étape de Hello est toodeploy gestion des API et un tooAzure de cluster Service Fabric dans un réseau virtuel partagé. Cela permet de toocommunicate de gestion des API directement avec l’infrastructure de Service afin d’exécuter découverte de service, la résolution de partition de service et transférer le trafic directement tooany principal de service Service Fabric.

### <a name="topology"></a>Topologie

Ce guide déploie suivant de hello tooAzure de topologie dans lequel l’infrastructure de Service et de gestion des API se trouvent dans des sous-réseaux de hello même réseau virtuel :

 ![Légende de l’image][sf-apim-topology-overview]

tooget démarrer rapidement, les modèles du Gestionnaire de ressources sont fournis pour chaque étape du déploiement :

 - Topologie du réseau :
    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]
 - Cluster Service Fabric :
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]
 - Gestion des API :
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>Connectez-vous à tooAzure et sélectionnez votre abonnement

Ce guide utilise [Azure PowerShell][azure-powershell]. Lorsque vous démarrez une nouvelle session PowerShell, connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement avant d’exécuter des commandes Azure.
 
La connexion tooyour compte Azure :

```powershell
PS > Login-AzureRmAccount
```

Sélectionnez votre abonnement :

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créez un groupe de ressources pour votre déploiement. Attribuez-lui un nom et un emplacement.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Déployer la topologie du réseau hello

Hello première étape consiste tooset des toowhich de topologie réseau hello gestion des API et cluster Service Fabric de hello sera déployé. Hello [network.json] [ network-arm] modèle du Gestionnaire de ressources est toocreate configuré un réseau virtuel (VNET) avec deux sous-réseaux et les deux groupes de sécurité réseau (NSG). 

Hello [network.parameters.json] [ network-parameters-arm] fichier de paramètres contient des noms de hello des sous-réseaux de hello et des groupes de sécurité réseau gestion des API et l’infrastructure de Service seront déployé. Dans ce guide, les valeurs de paramètre hello n’avez pas besoin toobe modifié. modèles de gestion des API et le Gestionnaire de ressources de l’infrastructure de Service Hello utilisent ces valeurs, afin de s’ils sont modifiés ici, vous devez modifier dans hello en conséquence les autres modèles de gestionnaire de ressources. 

 1. Vous pouvez télécharger hello suivant du fichier de modèle et les paramètres du Gestionnaire de ressources :

    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]

 2. Utilisez hello suivant PowerShell commande toodeploy hello Gestionnaire de ressources du modèle de fichiers et de paramètres pour le programme d’installation de hello réseau :

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Déployer le cluster Service Fabric de hello

Une fois que les ressources du réseau hello ont terminé le déploiement, étape suivante de hello est toodeploy un toohello de cluster Service Fabric réseau virtuel dans un sous-réseau de hello et désigné par groupe de sécurité réseau pour le cluster Service Fabric de hello. Pour ce didacticiel, modèle de gestionnaire de ressources de l’infrastructure de Service hello est préconfigurée de manière toouse les noms de hello hello réseau virtuel, sous-réseau et groupe de sécurité réseau que vous avez configurée à l’étape précédente de hello. 

modèle de gestionnaire de ressources de cluster de Service Fabric Hello est toocreate configuré un cluster sécurisé avec la sécurité du certificat. certificat de Hello est communication de nœud à nœud toosecure utilisé pour votre cluster et le cluster Service Fabric de toomanage utilisateur accès tooyour. Gestion des API utilise cette hello tooaccess de certificat l’infrastructure de Service d’affectation de noms de Service pour la découverte de service.

Cette étape nécessite de disposer d’un certificat de sécurité du cluster dans le coffre de clés. Pour plus d’informations sur la configuration d’un cluster sécurisé avec le coffre de clés, consultez [ce guide sur la création d’un cluster dans Azure à l’aide de Resource Manager](service-fabric-cluster-creation-via-arm.md).

> [!NOTE]
> Vous pouvez ajouter l’authentification Azure Active Directory dans Ajout toohello certificat est utilisé pour l’accès au cluster. Azure Active Directory est hello recommandé cluster Service Fabric de façon toomanage utilisateur accès tooyour, mais n’est pas nécessaire toocomplete ce didacticiel. Un certificat est requis dans les deux cas pour la sécurité nœud à nœud du cluster et pour l’authentification de Gestion des API Azure, qui ne prend pas actuellement en charge l’authentification avec Azure Active Directory pour un principal de Service Fabric.

 1. Vous pouvez télécharger hello suivant du fichier de modèle et les paramètres du Gestionnaire de ressources :
 
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]

 2. Renseignez les paramètres vide hello hello `cluster.parameters.json` fichier pour votre déploiement, y compris hello [les informations de coffre de clés](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) pour votre certificat de cluster.

 3. Utilisez hello suivant PowerShell commande toodeploy hello Gestionnaire de ressources du modèle et le paramètre fichiers toocreate hello cluster Service Fabric :

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>Déploiement de Gestion des API

Enfin, déployez toohello de gestion des API réseau virtuel dans un sous-réseau de hello et NSG désigné pour la gestion des API. Il est inutile toowait pour toofinish de déploiement de cluster de Service Fabric hello avant de déployer la gestion des API. 

Pour ce didacticiel, modèle de gestionnaire de ressources de gestion des API hello est préconfigurée de manière toouse les noms de hello hello réseau virtuel, sous-réseau et groupe de sécurité réseau que vous avez configurée à l’étape précédente de hello. 

 1. Vous pouvez télécharger hello suivant du fichier de modèle et les paramètres du Gestionnaire de ressources :
 
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

 2. Renseignez les paramètres vide hello hello `apim.parameters.json` pour votre déploiement.

 3. Utilisez hello suivant PowerShell commande toodeploy hello Gestionnaire de ressources du modèle de fichiers et de paramètres pour la gestion des API :

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>Configuration de Gestion des API

Une fois Gestion des API et le cluster Fabric Service déployés, vous pouvez configurer un principal de Service Fabric dans Gestion des API. Cela vous permet de toocreate une stratégie de service principaux qui envoie le cluster Service Fabric de tooyour le trafic.

### <a name="api-management-security"></a>Sécurité de Gestion des API

tooconfigure hello Service Fabric principal, vous devez tout d’abord les paramètres de sécurité de gestion des API tooconfigure. les paramètres de sécurité tooconfigure, accédez tooyour API de service de gestion Bonjour portail Azure.

#### <a name="enable-hello-api-management-rest-api"></a>Activer l’API REST de gestion des API de hello

Hello API REST de gestion des API est actuellement hello seule façon tooconfigure un service principal. première étape de Hello est tooenable hello API REST de gestion des API et sécuriser.

 1. Dans le service de gestion des API de hello, sélectionnez **gestion des API - version préliminaire** sous **sécurité**.
 2. Vérifiez hello **API REST de gestion des API activer** case à cocher.
 3. Notez hello URL d’API de gestion - il s’agit des URL de hello, nous allons utiliser tooset ultérieure des principaux de Service Fabric hello
 4. Générer un **jeton d’accès** en sélectionnant une date d’expiration et une clé, puis cliquez sur hello **générer** bouton bas hello de page de hello.
 5. Hello de copie **jeton d’accès** et enregistrez-le - nous les utiliserons Bonjour comme suit. Notez que cela est différent de hello des clés primaires et secondaires.

#### <a name="upload-a-service-fabric-client-certificate"></a>Chargement d’un certificat client Service Fabric

Gestion des API doivent s’authentifier avec votre cluster Service Fabric pour la découverte de service à l’aide d’un certificat client qui a cluster tooyour d’accès. Par souci de simplicité, ce didacticiel utilise hello même certificat spécifié lors de la création du cluster Service Fabric hello, qui par défaut peut être utilisé tooaccess votre cluster.

 1. Dans le service de gestion des API de hello, sélectionnez **certificats clients - version préliminaire** sous **sécurité**.
 2. Cliquez sur hello **+ ajouter** bouton
 2. Sélectionnez hello fichier de clé privée (.pfx) du certificat de cluster hello que vous avez spécifié lors de la création de votre cluster Service Fabric, lui donner un nom et mot de passe clé privée hello.

> [!NOTE]
> Ce didacticiel utilise hello même certificat pour la sécurité de client d’authentification et du cluster de nœud à l’autre. Vous pouvez utiliser un certificat client distinct si vous avez un tooaccess configuré votre cluster Service Fabric.

### <a name="configure-hello-backend"></a>Configurer hello principal

Maintenant que la sécurité de la gestion des API est configurée, vous pouvez configurer les principaux de Service Fabric hello. Pour les serveurs principaux de Service Fabric, cluster Service Fabric de hello est hello principal, plutôt que d’un service de l’infrastructure de Service spécifique. Cela permet à un toomore tooroute de stratégie unique à un service de cluster de hello.

Cette étape nécessite le jeton d’accès hello que précédemment générés et hello empreinte numérique de votre certificat de cluster que vous avez téléchargé tooAPI Management à l’étape précédente de hello.

> [!NOTE]
> Si vous avez utilisé un certificat client distinct à l’étape précédente de hello pour la gestion des API, vous devez l’empreinte numérique hello du certificat client hello empreinte de certificat du cluster addition toohello dans cette étape.

Envoyer hello suivant toohello de demande HTTP PUT URL d’API de gestion des API notées précédemment lors de l’activation du service principal de hello API REST de gestion des API tooconfigure hello Service Fabric. Vous devez voir une `HTTP 201 Created` réponse lors de la commande hello réussit. Pour plus d’informations sur chaque champ, consultez Gestion des API de hello [documentation de référence des API de service principal](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).

Commande HTTP et URL :
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

En-têtes de requête :
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

Corps de la requête :
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

Hello **url** paramètre ici est un nom qualifié complet de service d’un service dans votre cluster de toutes les demandes sont routés par défaut de tooby si aucun nom de service n’est spécifié dans une stratégie de serveur principal. Vous pouvez utiliser un nom de service factice, tel que « fabric : / faux/service » si vous ne comptez pas toohave un service de secours.

Consultez toohello gestion des API [documentation de référence des API de service principal](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) pour plus d’informations sur chaque champ.

#### <a name="example"></a>Exemple

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Déploiement d’un service principal de Service Fabric

Maintenant que vous avez hello que service Fabric est configuré comme un tooAPI principal Management, vous pouvez créer des stratégies du serveur principal pour votre API qui envoient le trafic services de Service Fabric tooyour. Mais tout d’abord vous avez besoin d’un service en cours d’exécution dans les demandes de tooaccept Service Fabric.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>Création d’un service Service Fabric avec un point de terminaison HTTP

Pour ce didacticiel, nous allons créer une base Service sans état ASP.NET Core fiable à l’aide du modèle de projet Web API hello par défaut. Vous créerez ainsi un point de terminaison HTTP pour votre service, que vous exposerez via Gestion des API Azure :

```
/api/values
```

Commencez par [configurer votre environnement de développement pour le développement d’ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).

Une fois votre environnement de développement configuré, démarrez Visual Studio en tant qu’administrateur et créez un service ASP.NET Core :

 1. Dans Visual Studio, sélectionnez Fichier -> Nouveau projet.
 2. Sélectionnez le modèle d’Application Service Fabric hello dans le Cloud et nommez-le **« ApiApplication »**.
 3. Sélectionnez hello modèle de service ASP.NET Core et projet de hello nom **« WebApiService »**.
 4. Sélectionnez le modèle de projet hello Web API ASP.NET Core 1.1.
 5. Une fois que le projet de hello est créé, ouvrez `PackageRoot\ServiceManifest.xml` et supprimer hello `Port` attribut à partir de la configuration de ressource de point de terminaison hello :
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    Cela permet à Service Fabric toospecify un port de manière dynamique à partir de la plage de ports d’application hello, qui nous ouverts via hello groupe de sécurité réseau dans le modèle de gestionnaire de ressources de cluster hello, en autorisant le trafic tooflow tooit à partir de la gestion des API.
 
 6. Appuyez sur F5 dans Visual Studio tooverify hello web API est disponible localement. 

    Ouvrez l’Explorateur de l’infrastructure de Service et Descendre instance spécifique de tooa Hello ASP.NET toosee hello adresse de base hello service principal est à l’écoute sur. Ajouter `/api/values` toohello adresse de base et ouvrez-le dans un navigateur. Cela appelle hello méthode Get sur hello ValuesController dans le modèle d’API Web hello. Il renvoie la réponse par défaut hello qui est fourni par le modèle de hello, un tableau JSON qui contient deux chaînes :

    ```json
    ["value1", "value2"]`
    ```

    Il s’agit de point de terminaison hello vous expose via l’API de gestion dans Azure.

 7. Enfin, déployez un cluster tooyour hello application dans Azure. [À l’aide de Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), cliquez sur le projet d’Application hello et sélectionnez **publier**. Fournissez votre point de terminaison de cluster (par exemple, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour l’infrastructure de Service de cluster dans Azure.

Un service ASP.NET Core sans état nommé `fabric:/ApiApplication/WebApiService` doit maintenant s’exécuter dans votre cluster Service Fabric dans Azure.

## <a name="create-an-api-operation"></a>Création d’une opération d’API

Maintenant, nous sommes prêt toocreate une opération de gestion des API qui toocommunicate d’utilisation des clients externes avec hello service sans état de ASP.NET Core en cours d’exécution dans le cluster Service Fabric de hello.

 1. Connectez-vous à toohello portail Azure et accédez de déploiement du service Gestion des API tooyour.
 2. Dans le panneau de service de gestion des API hello, sélectionnez **API - version préliminaire**
 3. Ajouter une nouvelle API en cliquant sur hello **API vide** boîte et remplissez la boîte de dialogue hello :

     - **URL du service Web** : pour les principaux de Service Fabric, cette valeur d’URL n’est pas utilisée. Vous pouvez placer n’importe quelle valeur ici. Pour ce didacticiel, utilisez : `http://servicefabric`.
     - **Nom** : entrez un nom pour votre API. Pour ce didacticiel, utilisez `Service Fabric App`.
     - **Modèle d’URL** : sélectionnez HTTP, HTTPS ou les deux. Pour ce didacticiel, utilisez `both`.
     - **API URL Suffix** (Suffixe d’URL d’API) : spécifiez un suffixe pour notre API. Pour ce didacticiel, utilisez `myapp`.
 
 4. Une fois hello API est créé, cliquez sur **+ de l’opération d’ajout de** tooadd une API frontale opération. Renseignez les valeurs hello :
    
     - **URL**: sélectionnez `GET` et fournir un chemin d’accès URL hello API. Pour ce didacticiel, utilisez `/api/values`.
     
       Par défaut, le chemin d’accès de hello URL spécifié ici est le chemin d’accès des URL hello envoyé service de l’infrastructure de Service principal toohello. Si vous utilisez hello même chemin d’URL ici que votre service utilise, dans ce cas `/api/values`, puis hello fonctionne sans modification supplémentaire. Vous pouvez également spécifier un chemin d’URL ici est différent du chemin d’accès de l’URL hello utilisé par votre service principal de service de l’infrastructure de Service, dans ce cas, vous devez également toospecify besoin de réécrire d’un chemin d’accès de votre stratégie de l’opération ultérieurement.
     - **Nom d’affichage**: fournir un nom pour l’API de hello. Pour ce didacticiel, utilisez `Values`.

## <a name="configure-a-backend-policy"></a>Configuration d’une stratégie de principal

stratégie de serveur principal Hello lie l’ensemble. Il s’agit dans laquelle vous configurez hello principal Service Fabric toowhich du service sont routées. Vous pouvez appliquer cette opération de l’API tooany stratégie. Hello [configuration principale d’un Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) fournit suivant de hello demande des contrôles de routage : 
 - Sélection de l’instance de service en spécifiant un nom d’instance d’un service Service Fabric, soit codé en dur (par exemple, `"fabric:/myapp/myservice"`) ou généré à partir de la demande de hello HTTP (par exemple, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Résolution de partition en générant une clé de partition à l’aide d’un modèle de partitionnement de Service Fabric.
 - Sélection de réplica pour les services avec état.
 - Résolution recommencez les conditions qui permettent de conditions de hello toospecify pour résoudre à nouveau un emplacement de service et le renvoi d’une demande.

Pour ce didacticiel, créez une stratégie de serveur principal qui route les requêtes directement toohello service sans état de ASP.NET Core déployé précédemment :

 1. Sélectionner et modifier hello **entrants stratégies** pour hello `Values` opération en cliquant sur icône de modification hello, puis en sélectionnant **mode Code**.
 2. Dans l’éditeur de code hello stratégie, ajoutez un `set-backend-service` stratégie sous entrant stratégies, comme indiqué ici et cliquez sur hello **enregistrer** bouton :
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

Pour un ensemble d’attributs de stratégie principal de l’infrastructure de Service, consultez toohello [documentation principale de gestion des API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Ajouter hello API tooa produit. 

Avant de pouvoir appeler les API hello, il doit être ajouté produit tooa où vous pouvez accorder l’accès toousers. 

 1. Dans le service de gestion des API de hello, sélectionnez **produits - version préliminaire**.
 2. Par défaut, Gestion des API fournit deux produits : Starter et Unlimited. Sélectionnez illimitées hello.
 3. Sélectionnez les API.
 4. Cliquez sur hello **+ ajouter** bouton.
 5. Sélectionnez hello `Service Fabric App` API vous créés dans les étapes précédentes hello et cliquez sur hello **sélectionnez** bouton.

### <a name="test-it"></a>Testez-le

Vous pouvez maintenant essayer d’envoi d’un service principal de tooyour demande dans l’infrastructure de Service via la gestion de l’API directement à partir de hello portail Azure.

 1. Dans le service de gestion des API de hello, sélectionnez **API - version préliminaire**.
 2. Bonjour `Service Fabric App` API que vous avez créé dans les étapes précédentes hello, sélectionnez hello **Test** onglet.
 3. Cliquez sur hello **envoyer** bouton toosend un service de test demande toohello principal.

## <a name="next-steps"></a>Étapes suivantes

À ce stade, vous devez disposer d’une configuration de base avec Service Fabric et Gestion des API.

Ce didacticiel utilise l’authentification de base utilisateur basée sur certificat pour votre tooget de cluster Service Fabric que vous permettent de rapidement. Une authentification utilisateur plus avancée de votre cluster Service Fabric est préférable avec [l’authentification Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication). 

Ensuite, [créer et configurer des paramètres de produits avancés dans Gestion des API Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare votre application pour le trafic du monde réel.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
