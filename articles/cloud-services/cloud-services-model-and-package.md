---
title: "aaaWhat est un modèle de Service Cloud et un package | Documents Microsoft"
description: "Décrit le modèle de service cloud hello (.csdef, .cscfg) et de package (.cspkg) dans Azure"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>Nouveautés du modèle de Service de cloud computing hello et comment il package ?
Un service cloud est créé à partir de trois composants, définition de service hello *(.csdef)*, la configuration de service de hello *(.cscfg)*et un package de service *(.cspkg)*. Les deux hello **ServiceDefinition.csdef** et **ServiceConfig.cscfg** fichiers basé sur XML et décrivent structure hello du service de cloud computing hello et la façon dont il est configuré ; collectivement appelé modèle de hello. Hello **ServicePackage.cspkg** est un fichier zip qui est généré à partir de hello **ServiceDefinition.csdef** et entre autres choses, contient toutes les dépendances de fichier binaire hello requis. Azure crée un service cloud à partir de ces deux hello **ServicePackage.cspkg** et hello **ServiceConfig.cscfg**.

Une fois que le service de cloud computing hello s’exécute dans Azure, vous pouvez le reconfigurer via hello **ServiceConfig.cscfg** fichier, mais vous ne pouvez pas modifier la définition de hello.

## <a name="what-would-you-like-tooknow-more-about"></a>Sur quel contenu souhaitez-vous tooknow plus ?
* Je veux tooknow plus hello [ServiceDefinition.csdef](#csdef) et [ServiceConfig.cscfg](#cscfg) fichiers.
* Je connais déjà cela, mais donnez-moi [quelques exemples](#next-steps) de configuration.
* Je veux toocreate hello [ServicePackage.cspkg](#cspkg).
* J’utilise Visual Studio et souhaite...
  * [Création d'un service cloud][vs_create]
  * [Reconfigurer un service cloud existant][vs_reconfigure]
  * [Déployer un projet de service cloud][vs_deploy]
  * [Un Bureau à distance sur une instance de service cloud][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Hello **ServiceDefinition.csdef** fichier spécifie les paramètres de hello sont utilisées par Azure tooconfigure un service cloud. Hello [schéma de définition de Service Azure (fichier de .csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) fournit le format autorisé de hello pour un fichier de définition de service. Hello suivant montre les paramètres hello qui peuvent être définis pour hello Web et rôles de travail :

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

Vous pouvez faire référence toohello [schéma de définition du Service](https://msdn.microsoft.com/library/azure/ee758711.aspx) pour mieux comprendre le fonctionnement du schéma XML de hello utilisé ici, toutefois, voici une explication rapide de certains des éléments de hello :

**Sites**  
Contient les définitions de hello pour les applications web ou des sites Web qui sont hébergées dans IIS 7.

**InputEndpoints**  
Contient des définitions de hello pour les points de terminaison utilisé toocontact hello cloud service.

**InternalEndpoints**  
Contient les définitions de hello pour les points de terminaison qui sont utilisés par toocommunicate d’instances de rôle entre eux.

**ConfigurationSettings**  
Contient les définitions de paramètre hello pour les fonctionnalités d’un rôle spécifique.

**Certificats**  
Contient les définitions de hello pour les certificats qui sont nécessaires pour un rôle. exemple de code précédent Hello montre un certificat qui est utilisé pour la configuration de hello de Connect de Azure.

**LocalResources**  
Contient les définitions de hello pour les ressources de stockage local. Une ressource de stockage local est un répertoire réservé sur le système de fichiers hello de machine virtuelle de hello dans lequel une instance d’un rôle est en cours d’exécution.

**Imports**  
Contient les définitions de hello pour les modules importés. exemple de code précédent Hello présente les modules de hello pour la connexion Bureau à distance et Azure Connect.

**Startup**  
Contient des tâches qui sont exécutées lorsque le rôle de hello démarre. tâches de Hello sont définies dans un fichier .cmd ou fichier exécutable.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
configuration de Hello de paramètres hello pour votre service cloud est déterminée par les valeurs hello Bonjour **ServiceConfiguration.cscfg** fichier. Vous spécifiez le nombre de hello d’instances que vous souhaitez toodeploy pour chaque rôle dans ce fichier. les valeurs Hello hello paramètres de configuration que vous avez définie dans le fichier de définition de service hello sont ajoutés toohello fichier de configuration de service. empreintes numériques de Hello pour les certificats de gestion qui sont associés au service de cloud computing hello sont également ajoutés toohello fichier. Hello [schéma de Configuration du Service Azure (.cscfg fichier)](https://msdn.microsoft.com/library/azure/ee758710.aspx) fournit le format autorisé de hello pour un fichier de configuration de service.

Hello fichier de configuration de service n’est pas fourni avec l’application hello, mais est tooAzure téléchargé dans un fichier distinct et est utilisé tooconfigure hello service cloud. Vous pouvez charger un nouveau fichier de configuration de service sans redéployer votre service cloud. les valeurs de configuration Hello pour le service cloud hello peuvent être modifiés pendant l’exécution du service de cloud computing hello. Hello suivant montre les paramètres de configuration hello qui peuvent être définis pour hello Web et rôles de travail :

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

Vous pouvez faire référence toohello [schéma de Configuration de Service](https://msdn.microsoft.com/library/azure/ee758710.aspx) pour une meilleure compréhension hello XSD utilisé ici, toutefois, voici une explication rapide des éléments de hello :

**Instances**  
Configure le nombre hello de l’exécution des instances de rôle de hello. tooprevent votre cloud service devienne indisponible pendant les mises à niveau, il est recommandé de déployer plusieurs instances de vos rôles web. En déployant plusieurs instances, vous respectez les instructions toohello Bonjour [Azure Compute contrat (SLA)](http://azure.microsoft.com/support/legal/sla/), ce qui garantit une connectivité externe à 99,95 % pour les rôles Internet lorsque deux ou plusieurs rôles instances sont déployées pour un service.

**ConfigurationSettings**  
Configure les paramètres hello pour hello instances pour un rôle en cours d’exécution. nom Hello Hello `<Setting>` éléments doivent correspondre à des définitions de paramètre hello dans le fichier de définition de service hello.

**Certificats**  
Configure les certificats de hello sont utilisées par le service de hello. exemple de code Hello précédent montre comment toodefine hello certificat pour le module RemoteAccess de hello. Hello valeur Hello *l’empreinte numérique* attribut doit être défini à l’empreinte numérique toohello de hello certificat toouse.

<p/>

> [!NOTE]
> fichier de configuration toohello peut être ajouté à l’empreinte numérique Hello pour le certificat de hello, à l’aide d’un éditeur de texte. Ou, à la valeur de hello peut être ajoutée sur hello **certificats** onglet Hello **propriétés** page de rôle hello dans Visual Studio.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Définition des ports pour les instances de rôle
Azure ne permet qu’un seul rôle web de tooa de point d’entrée. En d’autres termes, tout le trafic s’effectue via une adresse IP. Vous pouvez configurer vos sites Web de tooshare un port en configurant hello hôte en-tête toodirect hello demande toohello emplacement correct. Vous pouvez également configurer les ports de toowell connue toolisten applications sur l’adresse IP de hello.

Hello exemple suivant illustre les configuration hello pour un rôle web avec un site Web et l’application web. site Web de Hello est configuré en tant qu’emplacement d’entrée hello par défaut sur le port 80, et les applications web hello sont demandes tooreceive configuré à partir d’un en-tête d’hôte de remplacement est appelé « mail.mysite.cloudapp.net ».

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a>La modification de la configuration d’un rôle hello
Vous pouvez mettre à jour de configuration hello de votre service cloud pendant son exécution dans Azure, sans mise hors service de hello. toochange les informations de configuration, vous pouvez télécharger un fichier de configuration, ou modifier le fichier de configuration hello dans placer et appliquez-le tooyour service en cours d’exécution. Hello modifications suivantes peuvent être apportées configuration toohello d’un service :

* **Modification des valeurs de paramètres de configuration hello**  
  Lorsqu’une configuration définissant les modifications, une instance de rôle choisissez tooapply hello changer pendant que l’instance de hello est en ligne, ou toorecycle hello l’instance normalement et appliquer hello lors de l’instance de hello est hors connexion.
* **La modification de topologie du service hello d’instances de rôle**  
  Les modifications de la topologie n’affectent pas les instances en cours d’exécution, sauf lorsqu’une instance est supprimée. Toutes les instances restantes n’est généralement pas nécessaire toobe recyclé ; Toutefois, vous pouvez choisir toorecycle instances de rôle dans la modification de topologie tooa de réponse.
* **Modification de l’empreinte numérique du certificat hello**  
  Vous ne pouvez mettre à jour un certificat que lorsqu’une instance de rôle est hors connexion. Si un certificat est ajouté, supprimé ou modifié pendant qu’une instance de rôle est en ligne, Azure prend le certificat de hello hello instance tooupdate hors connexion et la remettre en ligne une fois hello modification effectuée normalement.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Gestion des modifications de configuration à l’aide des événements de service Runtime
Hello [bibliothèque du Runtime Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) inclut hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) espace de noms, qui fournit des classes pour interagir avec hello environnement Azure à partir d’un rôle. Hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) classe définit hello suivant des événements qui sont déclenchés avant et après une modification de configuration :

* **[Modification](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) d’un événement**  
  Cela se produit avant la modification de la configuration hello tooa appliqué les instance spécifiée d’un rôle, ce qui vous donne un tootake chance vers le bas les instances de rôle hello si nécessaire.
* **[Événement](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) modifié**  
  Se produit après la modification de la configuration hello tooa appliqué les instance spécifiée d’un rôle.

> [!NOTE]
> Étant donné que les modifications de certificat toujours hors connexion des instances de hello d’un rôle, elles ne déclenchent pas les événements RoleEnvironment.Changing ou RoleEnvironment.Changed hello.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
toodeploy une application comme un service cloud dans Azure, vous devez première application hello de package au format approprié de hello. Vous pouvez utiliser hello **CSPack** outil de ligne de commande (installé avec hello [Azure SDK](https://azure.microsoft.com/downloads/)) fichier de package toocreate hello en tant qu’une autre tooVisual Studio.

**CSPack** utilise hello contenu hello service définition du service de fichiers et configuration toodefine hello du contenu du fichier de package de hello. **CSPack** génère un fichier de package d’application (.cspkg) que vous pouvez télécharger tooAzure à l’aide de hello [portail Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). Par défaut, le package de hello est nommé `[ServiceDefinitionFileName].cspkg`, mais vous pouvez spécifier un nom différent à l’aide de hello `/out` option de **CSPack**.

**CSPack** se situe dans  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> CSPack.exe (sous windows) est disponible en exécutant hello **invite de commandes Microsoft Azure** raccourci qui est installé avec le Kit de développement logiciel de hello.  
> 
> Réexécutez hello CSPack.exe par lui-même documentation toosee sur tous les commutateurs hello et les commandes.
> 
> 

<p />

> [!TIP]
> Exécuter votre service cloud localement Bonjour **émulateur de calcul Azure Microsoft**, utilisez hello **/copyonly** option. Cette option copie les fichiers binaires hello organisée en répertoires tooa application hello à partir duquel ils peuvent être exécutés dans l’émulateur de calcul hello.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>Exemple commande toopackage un service cloud
Hello exemple suivant crée un package d’application qui contient des informations de hello pour un rôle web. commande Hello spécifie toouse de fichier de définition de service hello, répertoire hello où les fichiers binaires peuvent être trouvés et hello nom hello du fichier de package.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Si l’application hello contient un rôle web et un rôle de travail, hello commande suivante est utilisée :

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Où les variables de hello sont définies comme suit :

| Variable | Valeur |
| --- | --- |
| \[DirectoryName\] |Bonjour sous-répertoire hello répertoire racine du projet qui contient le fichier de .csdef hello Hello projet Windows Azure. |
| \[ServiceDefinition\] |nom de Hello du fichier de définition de service hello. Par défaut, ce fichier se nomme ServiceDefinition.csdef. |
| \[OutputFileName\] |Hello nom hello généré pour le fichier de package. En règle générale, il a la valeur nom toohello de l’application hello. Si aucun nom de fichier n’est spécifié, le package d’application hello est créé en tant que \[ApplicationName\].cspkg. |
| \[RoleName\] |nom Hello du rôle hello tel que défini dans le fichier de définition de service hello. |
| \[RoleBinariesDirectory] |emplacement Hello des fichiers binaires de hello pour le rôle de hello. |
| \[VirtualPath\] |répertoires physiques de Hello pour chaque chemin d’accès virtuel défini dans la section de Sites hello de définition du service hello. |
| \[PhysicalPath\] |Bonjour répertoires physiques du contenu hello pour chaque chemin d’accès virtuel défini dans le nœud de site hello de définition du service hello. |
| \[RoleAssemblyName\] |nom de Hello du fichier binaire de hello pour le rôle de hello. |

## <a name="next-steps"></a>Étapes suivantes
Je crée un package de service cloud et je souhaite...

* [Configurer un Bureau à distance pour une instance de service cloud][remotedesktop]
* [Déployer un projet de service cloud][deploy]

J’utilise Visual Studio et souhaite...

* [Créer un nouveau service de cloud computing][vs_create]
* [Reconfigurer un service cloud existant][vs_reconfigure]
* [Déployer un projet de service cloud][vs_deploy]
* [Configurer un Bureau à distance pour une instance de service cloud][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
