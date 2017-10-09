---
title: aaaCreate une application de conteneur Azure Service Fabric | Documents Microsoft
description: "Créez votre première application de conteneur Windows sur Microsoft Azure Service Fabric.  Créer une image Docker avec une application de Python, push de Registre de conteneur hello image tooa, générer et déployer une application de conteneur de Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Créer votre première application de conteneur Service Fabric sur Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Exécution d’une application existante dans un conteneur Windows sur un cluster Service Fabric ne requiert pas n’importe quelle application tooyour de modifications. Cet article vous guide dans la création d’une image Docker qui contient une Python [ballon](http://flask.pocoo.org/) web application et déploiement de cluster du Service Fabric tooa.  Vous allez également partager votre application en conteneur via [Azure Container Registry](/azure/container-registry/).  Cet article suppose une connaissance élémentaire de Docker. Vous pouvez en savoir plus sur Docker par la lecture de hello [vue d’ensemble de Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Composants requis
Un ordinateur de développement exécutant :
* Visual Studio 2015 ou Visual Studio 2017.
* [Outils et SDK Service Fabric](service-fabric-get-started.md).
*  Docker pour Windows.  [Obtenez Docker CE pour Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). Une fois l’installation et démarrage de Docker, avec le bouton droit sur l’icône de barre d’état hello et sélectionnez **basculer les conteneurs tooWindows**. Il s’agit de toorun requis Docker images basées sur Windows.

Un cluster Windows avec au moins trois nœuds s’exécutant sur Windows Server 2016 avec conteneurs. [Créez un cluster](service-fabric-cluster-creation-via-portal.md) ou [essayez gratuitement Service Fabric](https://aka.ms/tryservicefabric).

Un registre dans Azure Container Registry. [Créez un registre de conteneurs](../container-registry/container-registry-get-started-portal.md) dans votre abonnement Azure.

## <a name="define-hello-docker-container"></a>Définir le conteneur Docker de hello
Générer une image basée sur hello [image de Python](https://hub.docker.com/_/python/) situé sur le Hub d’ancrage.

Définissez votre conteneur Docker dans un fichier Dockerfile. Hello Dockerfile contient des instructions pour configurer l’environnement hello à l’intérieur de votre conteneur, chargement de l’application hello souhaité toorun et mapper les ports. Hello Dockerfile est toohello d’entrée de hello `docker build` commande qui crée l’image de hello.

Créer un répertoire vide et créer le fichier de hello *Dockerfile* (avec aucune extension de fichier). Ajouter hello suivant trop*Dockerfile* et enregistrer vos modifications :

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Hello de lecture [informations de référence](https://docs.docker.com/engine/reference/builder/) pour plus d’informations.

## <a name="create-a-simple-web-application"></a>Créer une application web simple
Créez une application web Flask écoutant le port 80 qui renvoie « Hello World! ».  Dans l’hello même répertoire, créez le fichier de hello *requirements.txt*.  Ajoutez hello suivant et enregistrez vos modifications :
```
Flask
```

Créer également des hello *app.py* de fichiers et ajoutez hello qui suit :

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Générer l’image de hello
Exécutez hello `docker build` commande toocreate hello image qui exécute votre application web. Ouvrez une fenêtre PowerShell et accédez répertoire toohello contenant hello Dockerfile. Exécutez hello de commande suivante :

```
docker build -t helloworldapp .
```

Cette commande builds hello nouvelle image à l’aide des instructions de hello dans votre fichier Dockerfile, d’affectation de noms (-t marquage) l’image hello « helloworldapp ». Génération d’une image extrait l’image de base hello vers le bas à partir du Hub d’ancrage et crée une image qui ajoute votre application sur l’image de base hello.  

Une fois la commande de génération hello terminée, exécutez hello `docker images` toosee plus d’informations sur la nouvelle image de hello de commandes :

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Exécutez hello application localement
Vérifiez votre image localement avant d’en exécutant un push du Registre de conteneur hello.  

Exécutez l’application hello :

```
docker run -d --name my-web-site helloworldapp
```

*nom* donne un toohello nom du conteneur (au lieu de l’ID de conteneur hello) en cours d’exécution.

Une fois le conteneur de hello démarre, trouver son adresse IP afin de pouvoir vous connecter tooyour conteneur en cours d’exécution à partir d’un navigateur :
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Se connecter toohello conteneur en cours d’exécution.  Ouvrez un navigateur web pointant toohello adresse IP retournée, par exemple « http://172.31.194.61 ». Vous devez voir hello titre « Hello World ! » afficher dans le navigateur de hello.

toostop votre conteneur, exécutez :

```
docker stop my-web-site
```

Supprimer le conteneur de hello à partir de votre ordinateur de développement :

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>Registre de conteneur push hello image toohello
Après avoir vérifié que le conteneur de hello s’exécute sur votre ordinateur de développement, push de Registre de tooyour hello image dans le Registre de conteneur Azure.

Exécutez ``docker login`` toolog dans le Registre de conteneur tooyour avec votre [informations d’identification du Registre](../container-registry/container-registry-authentication.md).

Hello exemple suivant passe hello ID et mot de passe d’Azure Active Directory [principal du service](../active-directory/active-directory-application-objects.md). Par exemple, vous avez peut-être affectés un Registre tooyour principal de service pour un scénario d’automatisation. Ou bien, vous pouvez vous connecter à l’aide de votre nom d’utilisateur de registre et mot de passe.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hello commande suivante crée une balise ou un alias de l’image de hello, avec un Registre tooyour de chemin d’accès qualifié complet. Cet exemple place hello image Bonjour ```samples``` encombrement de l’espace de noms tooavoid dans la racine du Registre de hello hello.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Registre de conteneur tooyour push hello image :

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Créer un service de hello placées dans des conteneurs dans Visual Studio
Hello Service Fabric SDK et outils fournissent une toohelp de modèle de service vous créez une application en conteneur.

1. Démarrez Visual Studio.  Sélectionnez **Fichier** > **Nouveau** > **Projet**.
2. Sélectionnez **Service Fabric application** (Application Service Fabric), nommez-la « MyFirstContainer », puis cliquez sur **OK**.
3. Sélectionnez **invité conteneur** à partir de la liste des hello **les modèles de service**.
4. Dans **nom de l’Image** Entrez « myregistry.azurecr.io/samples/helloworldapp », image hello envoyées de référentiel de conteneurs tooyour.
5. Donnez un nom à votre service et cliquez sur **OK**.

## <a name="configure-communication"></a>Configurer la communication
service de Hello en conteneur a besoin d’un point de terminaison pour la communication. Ajouter un `Endpoint` élément avec le fichier ServiceManifest.xml toohello du type, le port et protocole de hello. Pour cet article, hello placées dans des conteneurs service écoute le port 8081.  Dans cet exemple, un port fixe 8081 est utilisé.  Si aucun port n’est spécifié, un port aléatoire à partir de la plage de ports d’application hello est choisi.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

En définissant un point de terminaison, l’infrastructure de Service publie toohello de point de terminaison hello Naming service.  Autres services qui s’exécutent dans un cluster de hello peuvent résoudre ce conteneur.  Vous pouvez également effectuer la communication de conteneur à l’autre à l’aide de hello [proxy inverse](service-fabric-reverseproxy.md).  Communication est effectuée en fournissant le port d’écoute hello proxy inverse HTTP et le nom hello de services hello que vous souhaitez toocommunicate avec comme variables d’environnement.

## <a name="configure-and-set-environment-variables"></a>Configurer et définir des variables d’environnement
Variables d’environnement peuvent être spécifiées pour chaque package de code dans le manifeste de service hello. Cette fonctionnalité est disponible pour tous les services, qu’ils soient déployés sous forme de conteneurs, de processus ou d’exécutables invités. Vous pouvez remplacer la variable d’environnement valeurs dans une application hello manifeste ou spécifient durant le déploiement en tant que paramètres de l’application.

Hello service manifeste XML extrait de code suivant illustre un exemple de variables d’environnement toospecify pour un package de code :
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Ces variables d’environnement peuvent être remplacées dans le manifeste de l’application hello :

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Configuration du mappage des ports de conteneur aux ports hôtes et de la détection de conteneur à conteneur
Configurer un toocommunicate de port utilisé hôte avec le conteneur de hello. liaison de port Hello mappe le port de hello sur quel hello service écoute à l’intérieur de hello conteneur tooa port sur l’ordinateur hôte de hello. Ajouter un `PortBinding` élément `ContainerHostPolicies` élément du fichier de ApplicationManifest.xml hello.  Pour cet article, `ContainerPort` est 80 (conteneur de hello expose le port 80, comme spécifié dans hello Dockerfile) et `EndpointRef` est « Guest1TypeEndpoint » (hello de point de terminaison défini précédemment dans le manifeste de service hello).  Les demandes entrantes sur le port 8081 du service toohello sont mappées tooport 80 sur le conteneur de hello.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Configurer l’authentification au registre de conteneurs Azure
Configurer l’authentification de Registre de conteneur en ajoutant `RepositoryCredentials` trop`ContainerHostPolicies` du fichier de ApplicationManifest.xml hello. Ajoutez hello et mot de passe pour le Registre de conteneur hello myregistry.azurecr.io, ce qui permet l’image de conteneur hello service toodownload hello à partir du référentiel de hello.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

Nous vous conseillons de chiffrer un mot de passe hello référentiel en utilisant un certificat de chiffrement qui a déployé tooall des nœuds de cluster de hello. Lorsque le Service Fabric déploie hello service package toohello de cluster, certificat de chiffrement hello est texte de chiffrement utilisé toodecrypt hello.  applet de commande Invoke-ServiceFabricEncryptText Hello est le texte de chiffrement hello toocreate utilisé pour le mot de passe hello, qui est ajouté toohello ApplicationManifest.xml fichier.

Bonjour script suivant crée un certificat auto-signé et il exporte le fichier PFX tooa.  certificat de Hello est importé dans un coffre de clés existant et puis déployé cluster Service Fabric de toohello.

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Chiffrer le mot de passe hello à l’aide de hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) applet de commande.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Remplacez le mot de passe de hello avec le texte de chiffrement hello retourné par hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) applet de commande et la valeur `PasswordEncrypted` trop à la valeur « true ».

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>Configurer le mode d’isolation
Windows prend en charge deux modes d’isolation pour les conteneurs : Processus et Hyper-V. Avec le mode d’isolation du processus de hello, en cours d’exécution tous les conteneurs de hello hello même hôte ordinateur partage hello du noyau avec l’hôte de hello. Avec le mode d’isolation hello Hyper-V, les noyaux hello sont isolées entre chaque conteneur Hyper-V et l’hôte de conteneur hello. le mode d’isolation Hello est spécifié dans hello `ContainerHostPolicies` élément dans le fichier manifeste d’application hello. modes d’isolation Hello qui peuvent être spécifiées sont `process`, `hyperv`, et `default`. mode d’isolement Hello par défaut est trop`process` sur Windows Server héberge et la valeur par défaut est trop`hyperv` sur des hôtes Windows 10. Hello extrait de code suivant montre comment le mode d’isolation hello est défini dans le fichier manifeste d’application hello.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Configurer la gouvernance des ressources
[Gouvernance des ressources](service-fabric-resource-governance.md) restreint hello ressources hello conteneur peuvent utiliser sur l’ordinateur hôte de hello. Hello `ResourceGovernancePolicy` élément, qui est spécifié dans le manifeste de l’application hello, est utilisé toodeclare des limites de ressources pour un package de code de service. Les limites de ressources peuvent être définies pour hello suivant des ressources : mémoire, MemorySwap, CpuShares (poids relatif de l’UC), MemoryReservationInMB, BlkioWeight (BlockIO le poids relatif).  Dans cet exemple, le package de service Guest1Pkg Obtient un cœur sur les nœuds de cluster hello où il est placé.  Limites de la mémoire étant absolus, le package de code hello est limitée too1024 Mo de mémoire (et une réservation soft-garantie de hello même). Packages de code (conteneurs ou processus) ne sont pas en mesure de tooallocate plus de mémoire que cette limite et de tenter de toodo engendre une exception de mémoire insuffisante. Pour toowork de mise en œuvre de limite de ressource, tous les packages de code au sein d’un package de service doivent avoir des limites de mémoire spécifiées.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Déployer l’application de conteneur hello
Enregistrer toutes vos modifications et générer l’application hello. toopublish votre application, avec le bouton droit sur **MyFirstContainer** dans l’Explorateur de solutions, puis sélectionnez **publier**.

Dans **connexion de point de terminaison**, entrez le point de terminaison de gestion hello pour le cluster de hello.  Par exemple : « containercluster.westus2.cloudapp.azure.com:19000 ». Vous pouvez trouver la connexion de client hello point de terminaison dans le panneau de vue d’ensemble de hello pour votre cluster Bonjour [portail Azure](https://portal.azure.com).

Cliquez sur **Publier**.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) est un outil web dédié à l’inspection et à la gestion d’applications et de nœuds dans un cluster Service Fabric. Ouvrez un navigateur et accédez toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorateur et suivez le déploiement de l’application hello.  application Hello déploie mais se trouve dans un état d’erreur jusqu'à ce que l’image de hello est téléchargé sur les nœuds de cluster hello (qui peuvent prendre un certain temps, en fonction de la taille de l’image hello) : ![erreur][1]

application Hello est prête, lorsqu’il est dans ```Ready``` état : ![prêt][2]

Ouvrez un navigateur et accédez toohttp://containercluster.westus2.cloudapp.azure.com:8081. Vous devez voir hello titre « Hello World ! » afficher dans le navigateur de hello.

## <a name="clean-up"></a>Nettoyer
Vous continuer tooincur frais pendant l’exécution du cluster de hello, envisagez de [la suppression de votre cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  Les [clusters d’essai](http://tryazureservicefabric.westus.cloudapp.azure.com/) sont automatiquement supprimés après quelques heures.

Une fois que vous effectuez un push Registre de conteneur toohello hello image, vous pouvez supprimer les images locales hello à partir de votre ordinateur de développement :

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Exemples complets de manifestes d’application et de service Service Fabric
Voici complète du service hello et des manifestes d’application utilisés dans cet article.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a>Configurer l’intervalle de temps d’attente avant l’arrêt forcé du conteneur

Vous pouvez configurer un intervalle de temps pour hello runtime toowait avant la suppression du conteneur de hello après que hello suppression du service (ou un nœud de tooanother move) a démarré. Intervalle de temps hello configuration envoie hello `docker stop <time in seconds>` conteneur toohello de commande.   Pour plus d’informations, consultez [Arrêt du docker](https://docs.docker.com/engine/reference/commandline/stop/). toowait d’intervalle de temps Hello est spécifié sous hello `Hosting` section. Hello suivant extrait de manifeste de cluster montre comment tooset hello délai d’attente :

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Hello intervalle de temps par défaut a la valeur too10 secondes. Étant donné que cette configuration est dynamique, une configuration uniquement mettre à niveau sur le délai d’attente de hello cluster mises à jour hello. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Configurer hello runtime tooremove les images de conteneur inutilisé

Vous pouvez configurer tooremove de cluster Service Fabric hello des images de conteneur inutilisé à partir du nœud de hello. Cette configuration permet de toobe d’espace disque rétabli si trop d’images de conteneur sont présents sur le nœud de hello.  tooenable cette fonctionnalité, la mise à jour hello `Hosting` section dans le manifeste du cluster hello, comme indiqué dans hello suivant extrait de code : 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Pour les images qui ne doivent pas être supprimés, vous pouvez les spécifier sous hello `ContainerImagesToSkip` paramètre. 



## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur l’exécution des [conteneurs sur Service Fabric](service-fabric-containers-overview.md).
* Hello de lecture [déployer une application .NET dans un conteneur](service-fabric-host-app-in-a-container.md) didacticiel.
* En savoir plus sur hello Service Fabric [cycle de vie des applications](service-fabric-application-lifecycle.md).
* Hello d’extraction [exemples de code de Service Fabric conteneur](https://github.com/Azure-Samples/service-fabric-dotnet-containers) sur GitHub.

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
