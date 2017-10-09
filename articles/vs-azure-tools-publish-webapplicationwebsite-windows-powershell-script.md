---
title: aaaPublish-WebApplicationWebSite (script Windows PowerShell) | Documents Microsoft
description: "Découvrez comment toopublish un site web de projet tooan site Web Azure. Ce script crée les ressources hello requis dans votre abonnement Azure si elles n’existent pas."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publish-WebApplicationWebSite (script Windows PowerShell)
## <a name="syntax"></a>Syntaxe
Publie un tooan de projet web site Web Azure. script de Hello crée les ressources hello requis dans votre abonnement Azure si elles n’existent pas.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Configuration
Hello chemin d’accès toohello fichier de configuration JSON qui décrit les détails de hello du déploiement de hello.

| Paramètre | Valeur par défaut |
| --- | --- |
| Alias |(aucun) |
| Requis ? |true |
| Position |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

## <a name="subscriptionname"></a>SubscriptionName
nom Hello Hello abonnement Azure que vous souhaitez le site Web de toocreate hello dans.

| Paramètre | Valeur par défaut |
| --- | --- |
| Alias |(aucun) |
| Requis ? |false |
| Position |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

## <a name="webdeploypackage"></a>WebDeployPackage
Hello chemin d’accès toohello web déploiement package toopublish toohello site Web. Vous pouvez créer ce package à l’aide d’Assistant de publication Web hello dans Visual Studio. Pour plus d’informations, consultez [Prise en main des services cloud Azure et d'ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Paramètre | Valeur par défaut |
| --- | --- |
| Alias |(aucun) |
| Requis ? |false |
| Position |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
nom d’utilisateur Hello et le mot de passe pour la base de données SQL hello dans Azure.

| Paramètre | Valeur par défaut |
| --- | --- |
| Alias |(aucun) |
| Requis ? |false |
| Position |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Si la valeur est true, les messages d’impression à partir de hello script toohello flux de sortie.

| Paramètre | Valeur par défaut |
| --- | --- |
| Alias |(aucun) |
| Requis ? |false |
| Position |named |
| Valeur par défaut |false |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

## <a name="remarks"></a>Remarques
Pour une explication complète de la façon dont toouse hello script toocreate développement et les environnements de Test, consultez [environnements de Test et à l’aide de Scripts Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).

fichier de configuration JSON Hello spécifie les détails de hello de nouveautés toobe déployé. Il inclut des informations de hello que vous avez spécifié lorsque vous avez créé le projet hello, telles que le nom de hello et nom d’utilisateur pour le site Web de hello. Il inclut également hello tooprovision de base de données, le cas échéant. Hello suivant de code montre un exemple de fichier de configuration JSON :

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Vous pouvez modifier hello JSON configuration fichier toochange, ce qui est déployé. Une section du site Web est requise, mais section base de données de hello est facultatif.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez [Publish-WebApplicationVM (script Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)

