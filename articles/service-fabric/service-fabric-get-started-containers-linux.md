---
title: aaaCreate une application de conteneur Azure Service Fabric sur Linux | Documents Microsoft
description: "Créez votre première application de conteneur Linux sur Microsoft Azure Service Fabric.  Créer une image Docker avec votre application, push de Registre de conteneur hello image tooa, générer et déployer une application de conteneur de Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Créer votre première application de conteneur Service Fabric sur Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Exécution d’une application existante dans un conteneur de Linux sur un cluster Service Fabric ne requiert pas n’importe quelle application tooyour de modifications. Cet article vous guide dans la création d’une image Docker qui contient une Python [ballon](http://flask.pocoo.org/) web application et déploiement de cluster du Service Fabric tooa.  Vous allez également partager votre application en conteneur via [Azure Container Registry](/azure/container-registry/).  Cet article suppose une connaissance élémentaire de Docker. Vous pouvez en savoir plus sur Docker par la lecture de hello [vue d’ensemble de Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Composants requis
* Un ordinateur de développement exécutant :
  * [Outils et SDK Service Fabric](service-fabric-get-started-linux.md).
  * [Docker CE pour Linux](https://docs.docker.com/engine/installation/#prior-releases). 
  * [Interface de ligne de commande de Service Fabric](service-fabric-cli.md)

* Un registre dans Azure Container Registry. [Créez un registre de conteneurs](../container-registry/container-registry-get-started-portal.md) dans votre abonnement Azure. 

## <a name="define-hello-docker-container"></a>Définir le conteneur Docker de hello
Générer une image basée sur hello [image de Python](https://hub.docker.com/_/python/) situé sur le Hub d’ancrage. 

Définissez votre conteneur Docker dans un fichier Dockerfile. Hello Dockerfile contient des instructions pour configurer l’environnement hello à l’intérieur de votre conteneur, chargement de l’application hello souhaité toorun et mapper les ports. Hello Dockerfile est toohello d’entrée de hello `docker build` commande qui crée l’image de hello. 

Créer un répertoire vide et créer le fichier de hello *Dockerfile* (avec aucune extension de fichier). Ajouter hello suivant trop*Dockerfile* et enregistrer vos modifications :

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
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

## <a name="build-hello-image"></a>Générer l’image de hello
Exécutez hello `docker build` commande toocreate hello image qui exécute votre application web. Ouvrez une fenêtre PowerShell et accédez trop*c:\temp\helloworldapp*. Exécutez hello de commande suivante :

```bash
docker build -t helloworldapp .
```

Cette commande builds hello nouvelle image à l’aide des instructions de hello dans votre fichier Dockerfile, d’affectation de noms (-t marquage) l’image hello « helloworldapp ». Génération d’une image extrait l’image de base hello vers le bas à partir du Hub d’ancrage et crée une image qui ajoute votre application sur l’image de base hello.  

Une fois la commande de génération hello terminée, exécutez hello `docker images` toosee plus d’informations sur la nouvelle image de hello de commandes :

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Exécutez hello application localement
Vérifiez que votre application en conteneur s’exécute localement avant d’en exécutant un push du Registre de conteneur hello.  

Exécutez l’application hello, mappage du conteneur de votre ordinateur port 4000 toohello exposées le port 80 :

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*nom* donne un toohello nom du conteneur (au lieu de l’ID de conteneur hello) en cours d’exécution.

Se connecter toohello conteneur en cours d’exécution.  Ouvrez un navigateur web pointant adresse toohello renvoyé sur le port 4000, par exemple « http://localhost:4000 ». Vous devez voir hello titre « Hello World ! » afficher dans le navigateur de hello.

![Hello World!][hello-world]

toostop votre conteneur, exécutez :

```bash
docker stop my-web-site
```

Supprimer le conteneur de hello à partir de votre ordinateur de développement :

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Registre de conteneur push hello image toohello
Après avoir vérifié que l’application hello s’exécute dans Docker, push de Registre de tooyour hello image dans le Registre de conteneur Azure.

Exécutez `docker login` toolog dans le Registre de conteneur tooyour avec votre [informations d’identification du Registre](../container-registry/container-registry-authentication.md).

Hello exemple suivant passe hello ID et mot de passe d’Azure Active Directory [principal du service](../active-directory/active-directory-application-objects.md). Par exemple, vous avez peut-être affectés un Registre tooyour principal de service pour un scénario d’automatisation.  Ou bien, vous pouvez vous connecter à l’aide de votre nom d’utilisateur de registre et mot de passe.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hello commande suivante crée une balise ou un alias de l’image de hello, avec un Registre tooyour de chemin d’accès qualifié complet. Cet exemple place hello image Bonjour `samples` encombrement de l’espace de noms tooavoid dans la racine du Registre de hello hello.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Registre de conteneur tooyour push hello image :

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>Le package d’image de Docker hello avec Yeoman
Hello SDK de l’infrastructure de Service pour Linux comprend un [Yeoman](http://yeoman.io/) générateur qui rend toocreate facilement votre application et ajouter une image de conteneur. Nous allons utiliser Yeoman toocreate appelée par une application avec un seul conteneur Docker *SimpleContainerApp*.

toocreate une application conteneur de l’infrastructure de Service, ouvrez une fenêtre de terminal et exécutez `yo azuresfcontainer`.  

Nommez votre application (par exemple, « mycontainer »). 

Fournir les URL de hello pour les images de conteneur hello dans un Registre de conteneur (par exemple, « »). 

Cette image a une charge de travail-point d’entrée défini, donc besoin tooexplicitly de spécifier des commandes d’entrée (les commandes exécutées à l’intérieur du conteneur hello, qui conserve conteneur hello en cours d’exécution après le démarrage). 

Spécifiez un nombre d’instances de « 1 ».

![Générateur Yeoman Service Fabric pour les conteneurs][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Configurer l’authentification de référentiel de conteneur et le mappage de port
Votre service en conteneur a besoin d’un point de terminaison pour la communication.  Maintenant ajouter hello protocole, port et type tooan `Endpoint` dans le fichier ServiceManifest.xml de hello. Pour cet article, hello placées dans des conteneurs service écoute le port 4000 : 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Fournissant hello `UriScheme` automatiquement registres hello le point de terminaison de conteneur avec hello Service Fabric d’affectation de noms de service pour la fonctionnalité de découverte. Un exemple de fichier ServiceManifest.xml complète est fournie à la fin de hello de cet article. 

Configurer le mappage de port de port du conteneur-hôte hello en spécifiant un `PortBinding` stratégie dans `ContainerHostPolicies` du fichier de ApplicationManifest.xml hello.  Pour cet article, `ContainerPort` est 80 (conteneur de hello expose le port 80, comme spécifié dans hello Dockerfile) et `EndpointRef` est « myserviceTypeEndpoint » (point de terminaison d’hello défini dans le manifeste de service hello).  Les demandes entrantes du service sur le port 4000 toohello sont mappées tooport 80 sur le conteneur de hello.  Si votre conteneur doit tooauthenticate avec un référentiel privé, puis ajoutez `RepositoryCredentials`.  Pour cet article, ajouter le nom du compte hello et un mot de passe pour le Registre de conteneur myregistry.azurecr.io hello. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Génération et package d’application de Service Fabric hello
modèles de Service Fabric Yeoman Hello incluent un script de génération pour [Gradle](https://gradle.org/), vous pouvez utiliser application hello toobuild hello Terminal Server. toobuild et package d’application hello, exécutez hello suivante :

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Déployer l’application hello
Une fois que l’application hello est générée, vous pouvez le déployer toohello cluster local à l’aide de hello CLI de l’infrastructure de Service.

Connectez le cluster Service Fabric local de toohello.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Hello d’utilisation script d’installation fournies dans hello modèle toocopy application hello magasin d’images du cluster toohello du package, inscrire le type d’application hello et créer une instance de l’application hello.

```bash
./install.sh
```

Ouvrez un navigateur et accédez tooService Fabric Explorer dans http://localhost:19080/Explorateur (remplacer localhost avec adresse IP privée hello Hello machine virtuelle si vous utilisez Vagrant sur Mac OS X). Développez le nœud Applications de hello et notez qu’il existe désormais une entrée pour votre type d’application et un autre pour la première instance de ce type de hello.

Se connecter toohello conteneur en cours d’exécution.  Ouvrez un navigateur web pointant adresse toohello renvoyé sur le port 4000, par exemple « http://localhost:4000 ». Vous devez voir hello titre « Hello World ! » afficher dans le navigateur de hello.

![Hello World!][hello-world]

## <a name="clean-up"></a>Nettoyer
Utiliser un script de désinstallation hello fournies dans l’instance d’application hello modèle toodelete hello du cluster de développement local hello et annuler l’inscription du type de l’application hello.

```bash
./uninstall.sh
```

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
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>Ajout d’application existante de plusieurs services tooan

effectuer d’une autre application tooan service conteneur déjà créée à l’aide d’yeoman, tooadd hello comme suit :

1. Modifier la racine toohello du répertoire d’application existant hello.  Par exemple, `cd ~/YeomanSamples/MyApplication`si `MyApplication` est l’application hello créée par Yeoman.
2. Exécutez `yo azuresfcontainer:AddService`.

<a id="manually"></a>


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

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
