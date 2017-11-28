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
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="42d59-103">Créer des enregistrements DNS pour une application web dans un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="42d59-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="42d59-104">Vous pouvez utiliser Azure DNS toohost un domaine personnalisé pour vos applications web.</span><span class="sxs-lookup"><span data-stu-id="42d59-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="42d59-105">Par exemple, vous créez une application web Azure et que vous souhaitez que vos utilisateurs tooaccess en l’utilisant contoso.com ou www.contoso.com comme nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="42d59-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="42d59-106">toodo, vous avez deux enregistrements de toocreate :</span><span class="sxs-lookup"><span data-stu-id="42d59-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="42d59-107">Un toocontoso.com de pointage enregistrement racine « A »</span><span class="sxs-lookup"><span data-stu-id="42d59-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="42d59-108">« « L’enregistrement CNAME pour nom www hello qui pointe toohello un enregistrement</span><span class="sxs-lookup"><span data-stu-id="42d59-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="42d59-109">Gardez à l’esprit que si vous créez un enregistrement A pour une application web dans Azure, hello Qu'un enregistrement doit être mis à jour manuellement si hello sous-jacent adresse IP pour la modification de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="42d59-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="42d59-110">Before you begin</span></span>

<span data-ttu-id="42d59-111">Avant de commencer, vous devez tout d’abord créer une zone DNS dans le système DNS d’Azure et déléguer hello dans votre tooAzure bureau d’enregistrement DNS.</span><span class="sxs-lookup"><span data-stu-id="42d59-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="42d59-112">toocreate une zone DNS, suivez les étapes de hello dans [créer une zone DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="42d59-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="42d59-113">toodelegate votre tooAzure DNS DNS, suivez les étapes hello dans [délégation de domaine DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="42d59-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="42d59-114">Après la création d’une zone et délégation tooAzure DNS, vous pouvez ensuite créer des enregistrements pour votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="42d59-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="42d59-115">1. Création d’un enregistrement A pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="42d59-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="42d59-116">Un enregistrement est toomap utilisé une adresse IP tooits.</span><span class="sxs-lookup"><span data-stu-id="42d59-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="42d59-117">Bonjour à l’exemple suivant, nous allons désigner comme une tooan d’enregistrement une adresse IPv4 :</span><span class="sxs-lookup"><span data-stu-id="42d59-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="42d59-118">Étape 1</span><span class="sxs-lookup"><span data-stu-id="42d59-118">Step 1</span></span>

<span data-ttu-id="42d59-119">Créer un enregistrement A et affecter tooa $rs variable</span><span class="sxs-lookup"><span data-stu-id="42d59-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="42d59-120">Étape 2</span><span class="sxs-lookup"><span data-stu-id="42d59-120">Step 2</span></span>

<span data-ttu-id="42d59-121">Ajouter le jeu d’enregistrements toohello créé précédemment valeur hello IPv4 « @ » à l’aide de la variable hello $rs assignée.</span><span class="sxs-lookup"><span data-stu-id="42d59-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="42d59-122">Hello valeur IPv4 attribuée sera adresse hello pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="42d59-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="42d59-123">adresse toofind hello pour une application web, suivez les étapes de hello dans [configurer un nom de domaine personnalisé dans Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="42d59-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="42d59-124">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="42d59-124">Step 3</span></span>

<span data-ttu-id="42d59-125">Valider le jeu d’enregistrements toohello modifications hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="42d59-126">Utilisez `Set-AzureRMDnsRecordSet` hello de tooupload change toohello tooAzure de jeu d’enregistrements DNS :</span><span class="sxs-lookup"><span data-stu-id="42d59-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="42d59-127">2. Créer un enregistrement CNAME pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="42d59-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="42d59-128">Si votre domaine est déjà géré par le système DNS Azure (consultez [délégation de domaine DNS](dns-domain-delegation.md), vous pouvez utiliser hello suivant hello exemple toocreate un enregistrement CNAME pour contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="42d59-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="42d59-129">Étape 1</span><span class="sxs-lookup"><span data-stu-id="42d59-129">Step 1</span></span>

<span data-ttu-id="42d59-130">Ouvrez PowerShell et créez un nouveau jeu d’enregistrements CNAME et affecter tooa $rs variable.</span><span class="sxs-lookup"><span data-stu-id="42d59-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="42d59-131">Cet exemple crée un type de jeu d’enregistrements CNAME à une « heure toolive » de 600 secondes dans la zone DNS nommé « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="42d59-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="42d59-132">Hello, l’exemple suivant est la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-132">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="42d59-133">Étape 2</span><span class="sxs-lookup"><span data-stu-id="42d59-133">Step 2</span></span>

<span data-ttu-id="42d59-134">Une fois hello jeu d’enregistrements CNAME est créé, vous devez toocreate une valeur d’alias qui pointe toohello l’application web.</span><span class="sxs-lookup"><span data-stu-id="42d59-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="42d59-135">À l’aide de hello précédemment affecté la variable « $rs » vous pouvez utiliser la commande PowerShell de hello ci-dessous alias de hello toocreate pour hello web application contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="42d59-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="42d59-136">Hello, l’exemple suivant est la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-136">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="42d59-137">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="42d59-137">Step 3</span></span>

<span data-ttu-id="42d59-138">Valider les modifications hello à l’aide de hello `Set-AzureRMDnsRecordSet` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="42d59-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="42d59-139">Vous pouvez valider les enregistrements hello a été créé correctement en interrogeant hello « www.contoso.com » à l’aide de nslookup, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="42d59-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="42d59-140">Créer un enregistrement « awverify » pour des applications web</span><span class="sxs-lookup"><span data-stu-id="42d59-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="42d59-141">Si vous décidez de toouse un enregistrement A pour votre application web, vous devez accéder via une tooensure de processus de vérification vous domaine personnalisé de hello propre.</span><span class="sxs-lookup"><span data-stu-id="42d59-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="42d59-142">Cette étape de vérification est effectuée en créant un enregistrement CNAME spécial nommé « awverify ».</span><span class="sxs-lookup"><span data-stu-id="42d59-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="42d59-143">Cette section concerne uniquement les enregistrements tooA.</span><span class="sxs-lookup"><span data-stu-id="42d59-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="42d59-144">Étape 1</span><span class="sxs-lookup"><span data-stu-id="42d59-144">Step 1</span></span>

<span data-ttu-id="42d59-145">Créer un enregistrement de « awverify » hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-145">Create hello "awverify" record.</span></span> <span data-ttu-id="42d59-146">Dans l’exemple hello ci-dessous, nous allons créer l’enregistrement de « aweverify » hello pour la propriété tooverify de contoso.com pour le domaine personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="42d59-147">Hello, l’exemple suivant est la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-147">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="42d59-148">Étape 2</span><span class="sxs-lookup"><span data-stu-id="42d59-148">Step 2</span></span>

<span data-ttu-id="42d59-149">Une fois que le jeu d’enregistrements hello « awverify » est créé, attribuez jeu alias d’enregistrements CNAME hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="42d59-150">Dans l’exemple hello ci-dessous, nous assignons tooawverify.contoso.azurewebsites.net d’alias hello CNAMe jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="42d59-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="42d59-151">Hello, l’exemple suivant est la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="42d59-151">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="42d59-152">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="42d59-152">Step 3</span></span>

<span data-ttu-id="42d59-153">Valider les modifications hello à l’aide de hello `Set-AzureRMDnsRecordSet cmdlet`, comme illustré dans la commande hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="42d59-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="42d59-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42d59-154">Next steps</span></span>

<span data-ttu-id="42d59-155">Suivez les étapes de hello dans [configuration d’un nom de domaine personnalisé pour le Service d’applications](../app-service-web/web-sites-custom-domain-name.md) tooconfigure votre toouse d’application web un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="42d59-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
