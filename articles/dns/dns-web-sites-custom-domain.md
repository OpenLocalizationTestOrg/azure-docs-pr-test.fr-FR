---
title: "aaaCreate les enregistrements DNS personnalisés pour une application web | Documents Microsoft"
description: "Modification des enregistrements DNS du domaine personnalisé toocreate pour l’application web à l’aide d’Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>Créer des enregistrements DNS pour une application web dans un domaine personnalisé

Vous pouvez utiliser Azure DNS toohost un domaine personnalisé pour vos applications web. Par exemple, vous créez une application web Azure et que vous souhaitez que vos utilisateurs tooaccess en l’utilisant contoso.com ou www.contoso.com comme nom de domaine complet.

toodo, vous avez deux enregistrements de toocreate :

* Un toocontoso.com de pointage enregistrement racine « A »
* « « L’enregistrement CNAME pour nom www hello qui pointe toohello un enregistrement

Gardez à l’esprit que si vous créez un enregistrement A pour une application web dans Azure, hello Qu'un enregistrement doit être mis à jour manuellement si hello sous-jacent adresse IP pour la modification de l’application web hello.

## <a name="before-you-begin"></a>Avant de commencer

Avant de commencer, vous devez tout d’abord créer une zone DNS dans le système DNS d’Azure et déléguer hello dans votre tooAzure bureau d’enregistrement DNS.

1. toocreate une zone DNS, suivez les étapes de hello dans [créer une zone DNS](dns-getstarted-create-dnszone.md).
2. toodelegate votre tooAzure DNS DNS, suivez les étapes hello dans [délégation de domaine DNS](dns-domain-delegation.md).

Après la création d’une zone et délégation tooAzure DNS, vous pouvez ensuite créer des enregistrements pour votre domaine personnalisé.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Création d’un enregistrement A pour votre domaine personnalisé

Un enregistrement est toomap utilisé une adresse IP tooits. Bonjour à l’exemple suivant, nous allons désigner comme une tooan d’enregistrement une adresse IPv4 :

### <a name="step-1"></a>Étape 1

Créer un enregistrement A et affecter tooa $rs variable

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>Étape 2

Ajouter le jeu d’enregistrements toohello créé précédemment valeur hello IPv4 « @ » à l’aide de la variable hello $rs assignée. Hello valeur IPv4 attribuée sera adresse hello pour votre application web.

adresse toofind hello pour une application web, suivez les étapes de hello dans [configurer un nom de domaine personnalisé dans Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>Étape 3 :

Valider le jeu d’enregistrements toohello modifications hello. Utilisez `Set-AzureRMDnsRecordSet` hello de tooupload change toohello tooAzure de jeu d’enregistrements DNS :

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Créer un enregistrement CNAME pour votre domaine personnalisé

Si votre domaine est déjà géré par le système DNS Azure (consultez [délégation de domaine DNS](dns-domain-delegation.md), vous pouvez utiliser hello suivant hello exemple toocreate un enregistrement CNAME pour contoso.azurewebsites.net.

### <a name="step-1"></a>Étape 1

Ouvrez PowerShell et créez un nouveau jeu d’enregistrements CNAME et affecter tooa $rs variable. Cet exemple crée un type de jeu d’enregistrements CNAME à une « heure toolive » de 600 secondes dans la zone DNS nommé « contoso.com ».

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

Hello, l’exemple suivant est la réponse de hello.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Étape 2

Une fois hello jeu d’enregistrements CNAME est créé, vous devez toocreate une valeur d’alias qui pointe toohello l’application web.

À l’aide de hello précédemment affecté la variable « $rs » vous pouvez utiliser la commande PowerShell de hello ci-dessous alias de hello toocreate pour hello web application contoso.azurewebsites.net.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

Hello, l’exemple suivant est la réponse de hello.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Étape 3 :

Valider les modifications hello à l’aide de hello `Set-AzureRMDnsRecordSet` applet de commande :

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

Vous pouvez valider les enregistrements hello a été créé correctement en interrogeant hello « www.contoso.com » à l’aide de nslookup, comme indiqué ci-dessous :

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>Créer un enregistrement « awverify » pour des applications web

Si vous décidez de toouse un enregistrement A pour votre application web, vous devez accéder via une tooensure de processus de vérification vous domaine personnalisé de hello propre. Cette étape de vérification est effectuée en créant un enregistrement CNAME spécial nommé « awverify ». Cette section concerne uniquement les enregistrements tooA.

### <a name="step-1"></a>Étape 1

Créer un enregistrement de « awverify » hello. Dans l’exemple hello ci-dessous, nous allons créer l’enregistrement de « aweverify » hello pour la propriété tooverify de contoso.com pour le domaine personnalisé de hello.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

Hello, l’exemple suivant est la réponse de hello.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Étape 2

Une fois que le jeu d’enregistrements hello « awverify » est créé, attribuez jeu alias d’enregistrements CNAME hello. Dans l’exemple hello ci-dessous, nous assignons tooawverify.contoso.azurewebsites.net d’alias hello CNAMe jeu d’enregistrements.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

Hello, l’exemple suivant est la réponse de hello.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Étape 3 :

Valider les modifications hello à l’aide de hello `Set-AzureRMDnsRecordSet cmdlet`, comme illustré dans la commande hello ci-dessous.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Étapes suivantes

Suivez les étapes de hello dans [configuration d’un nom de domaine personnalisé pour le Service d’applications](../app-service-web/web-sites-custom-domain-name.md) tooconfigure votre toouse d’application web un domaine personnalisé.
