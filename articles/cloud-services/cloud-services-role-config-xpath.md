---
title: "aide-mémoire aaaCloud rôle des Services Configuration XPath | Documents Microsoft"
description: "Bonjour divers paramètres XPath que vous pouvez utiliser dans les paramètres du rôle config tooexpose pour hello cloud service comme une variable d’environnement."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>Exposer les paramètres de configuration de rôle comme variable d'environnement avec XPath
Dans le traitement du service cloud hello ou fichier de définition de service de rôle web, vous pouvez exposer les valeurs de configuration d’exécution en tant que variables d’environnement. Hello les valeurs XPath suivantes est prises en charge (qui correspondent à des valeurs de tooAPI).

Ces valeurs XPath sont également disponibles via hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) bibliothèque. 

## <a name="app-running-in-emulator"></a>Application qui s'exécute dans l'émulateur
Indique que cette application hello est en cours d’exécution dans l’émulateur de hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@emulated" |
| Code |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>ID de déploiement
Récupère l’ID de déploiement hello pour l’instance de hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@id" |
| Code |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>ID de rôle
Récupère l’ID du rôle actuel hello pour l’instance de hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@id" |
| Code |var id = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>Mettre à jour le domaine
Récupère le domaine de mise à jour hello d’instance de hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@updateDomain" |
| Code |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>Domaine d'erreur
Récupère le domaine par défaut de l’instance de hello hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@faultDomain" |
| Code |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>Nom de rôle
Récupère le nom du rôle d’instances de hello hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@roleName" |
| Code |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>Paramètre de configuration
Valeur hello récupère hello spécifiée de configuration.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value" |
| Code |var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>Chemin de stockage local
Récupère le chemin d’accès de stockage local hello pour l’instance de hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path" |
| Code |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath; |

## <a name="local-storage-size"></a>Taille du stockage local
Récupère la taille de hello de hello le stockage local pour l’instance de hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB" |
| Code |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>Protocole du point de terminaison
Récupère le protocole de point de terminaison hello pour l’instance de hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol" |
| Code |var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol; |

## <a name="endpoint-ip"></a>IP du point de terminaison
Obtient hello spécifié l’adresse du point de terminaison.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address" |
| Code |var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address |

## <a name="endpoint-port"></a>Port du point de terminaison
Récupère le port du point de terminaison hello pour l’instance de hello.

| Type | Exemple |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port" |
| Code |var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port; |

## <a name="example"></a>Exemple
Voici un exemple d’un rôle de travail qui crée une tâche de démarrage avec une variable d’environnement nommée `TestIsEmulated` définir toohello [ @emulated valeur xpath](#app-running-in-emulator). 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) fichier.

Créer un package [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .

Activer le [Bureau à distance](cloud-services-role-enable-remote-desktop.md) pour un rôle.

