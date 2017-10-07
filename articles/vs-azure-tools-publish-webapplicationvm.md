---
title: aaaPublish-WebApplicationVM | Documents Microsoft
description: "Découvrez comment toodeploy un ordinateur virtuel de web application tooa. Ce script crée les ressources hello requis dans votre abonnement Azure si elles n’existent pas."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (script Windows PowerShell)
Déploie un ordinateur virtuel de web application tooa. script de Hello crée les ressources hello requis dans votre abonnement Azure si elles n’existent pas.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Configuration
Hello chemin d’accès toohello fichier de configuration JSON qui décrit les détails de hello du déploiement de hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

### <a name="subscriptionname"></a>SubscriptionName
nom Hello de hello abonnement Azure dans lequel vous souhaitez toocreate hello virtual machine.

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position |named |
| Valeur par défaut |Utilise le premier abonnement de hello dans le fichier d’abonnement hello |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

### <a name="webdeploypackage"></a>WebDeployPackage
Hello chemin d’accès toohello web déploiement package toopublish toohello machine virtuelle. Vous pouvez créer ce package à l’aide d’Assistant de publication Web hello dans Visual Studio. Consultez [Création d’un package de déploiement web dans Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

### <a name="allowuntrusted"></a>AllowUntrusted
Si la valeur est true, autoriser l’utilisation de hello de certificats qui ne sont pas signés par une autorité racine approuvée.

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position |named |
| Valeur par défaut |false |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

### <a name="vmpassword"></a>VMPassword
informations d’identification de Hello pour le compte d’ordinateur virtuel hello. Exemple : - VMPassword @{nom = « admin » ; Mot de passe = « password »}

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
informations d’identification de Hello pour la base de données SQL hello dans Azure. Exemple : - DatabaseServerPassword @{nom = « admin » ; Mot de passe = « password »}

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Si la valeur est true, les messages d’impression à partir de hello script toohello flux de sortie.

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position |named |
| Valeur par défaut |false |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

## <a name="remarks"></a>Remarques
Pour une explication complète de la façon dont toouse hello script toocreate développement et les environnements de Test, consultez [environnements de Test et à l’aide de Scripts Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).

fichier de configuration JSON Hello spécifie les détails de hello de nouveautés toobe déployé. Il inclut des informations de hello que vous avez spécifié lorsque vous avez créé le projet hello, telles que le nom de hello, groupe d’affinités, image de disque dur virtuel et taille de machine virtuelle de hello. Il inclut des points de terminaison hello sur l’ordinateur virtuel de hello, hello tooprovision de bases de données, le cas échéant et vous les paramètres de déploiement. Hello suivant de code montre un exemple de fichier de configuration JSON :

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Vous pouvez modifier hello JSON configuration fichier toochange, ce qui est configuré. Un ordinateur virtuel et un service cloud sont requis, mais hello de base de données section est facultative.

