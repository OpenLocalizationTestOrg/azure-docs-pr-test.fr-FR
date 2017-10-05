---
title: "Créer des enregistrements DNS personnalisés pour une application web | Microsoft Docs"
description: "Comment créer des enregistrements DNS de domaine personnalisés pour une application web à l’aide d’Azure DNS"
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
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="c425d-103">Créer des enregistrements DNS pour une application web dans un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="c425d-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="c425d-104">Vous pouvez utiliser Azure DNS pour héberger un domaine personnalisé pour vos applications web.</span><span class="sxs-lookup"><span data-stu-id="c425d-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="c425d-105">Par exemple, vous créez une application web Azure et vous voulez que vos utilisateurs y accèdent en utilisant contoso.com ou www.contoso.com comme FQDN.</span><span class="sxs-lookup"><span data-stu-id="c425d-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="c425d-106">Pour cela, vous devez créer deux enregistrements :</span><span class="sxs-lookup"><span data-stu-id="c425d-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="c425d-107">un enregistrement « A » racine pointant vers contoso.com</span><span class="sxs-lookup"><span data-stu-id="c425d-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="c425d-108">un enregistrement « CNAME » pour le nom www qui pointe vers l’enregistrement A</span><span class="sxs-lookup"><span data-stu-id="c425d-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="c425d-109">N'oubliez pas que si vous créez un enregistrement A pour une application web dans Azure, l'enregistrement A doit être mis à jour manuellement si l’adresse IP sous-jacente pour l'application web change.</span><span class="sxs-lookup"><span data-stu-id="c425d-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c425d-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c425d-110">Before you begin</span></span>

<span data-ttu-id="c425d-111">Avant de commencer, vous devez créer une zone DNS dans Azure DNS et déléguer cette zone de votre bureau d’enregistrement à Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c425d-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="c425d-112">Pour créer une zone DNS, suivez la procédure décrite dans [Créer une zone DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="c425d-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="c425d-113">Pour déléguer votre DNS à Azure DNS, suivez la procédure décrite dans [Délégation de domaine DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="c425d-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="c425d-114">Après avoir créé une zone et l’avoir déléguée à Azure DNS, vous pouvez ensuite créer des enregistrements pour votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c425d-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="c425d-115">1. Création d’un enregistrement A pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="c425d-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="c425d-116">Un enregistrement A est utilisé pour mapper un nom vers son adresse IP.</span><span class="sxs-lookup"><span data-stu-id="c425d-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="c425d-117">Dans l’exemple suivant, nous allons assigner @ en tant qu’enregistrement A pour une adresse IPv4 :</span><span class="sxs-lookup"><span data-stu-id="c425d-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="c425d-118">Étape 1</span><span class="sxs-lookup"><span data-stu-id="c425d-118">Step 1</span></span>

<span data-ttu-id="c425d-119">Créez un enregistrement A et assignez-le à une variable $rs</span><span class="sxs-lookup"><span data-stu-id="c425d-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="c425d-120">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c425d-120">Step 2</span></span>

<span data-ttu-id="c425d-121">Ajoutez la valeur IPv4 au jeu d’enregistrements précédemment créé « @ » en utilisant la variable $rs affectée.</span><span class="sxs-lookup"><span data-stu-id="c425d-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="c425d-122">La valeur IPv4 attribuée sera l'adresse IP de votre application web.</span><span class="sxs-lookup"><span data-stu-id="c425d-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="c425d-123">Pour trouver l’adresse IP d’une application web, suivez la procédure décrite dans [Configurer un nom de domaine personnalisé dans Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c425d-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="c425d-124">Étape 3</span><span class="sxs-lookup"><span data-stu-id="c425d-124">Step 3</span></span>

<span data-ttu-id="c425d-125">Validez les modifications apportées au jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="c425d-125">Commit the changes to the record set.</span></span> <span data-ttu-id="c425d-126">Utilisez `Set-AzureRMDnsRecordSet` pour charger les modifications apportées au jeu d’enregistrements dans Azure DNS :</span><span class="sxs-lookup"><span data-stu-id="c425d-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="c425d-127">2. Créer un enregistrement CNAME pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="c425d-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="c425d-128">Si votre domaine est déjà géré par Azure DNS (consultez [Délégation de domaine DNS](dns-domain-delegation.md)), vous pouvez utiliser l’exemple suivant pour créer un enregistrement CNAME pour contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="c425d-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="c425d-129">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="c425d-129">Step 1</span></span>

<span data-ttu-id="c425d-130">Ouvrez PowerShell et créez un jeu d’enregistrements CNAME, puis affectez-le à une variable $rs.</span><span class="sxs-lookup"><span data-stu-id="c425d-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="c425d-131">Cet exemple crée un type de jeu d’enregistrements CNAME avec une durée de vie de 600 secondes dans la zone DNS nommée « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="c425d-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="c425d-132">L’exemple suivant est la réponse.</span><span class="sxs-lookup"><span data-stu-id="c425d-132">The following example is the response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="c425d-133">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c425d-133">Step 2</span></span>

<span data-ttu-id="c425d-134">Une fois le jeu d'enregistrements CNAME créé, vous devez créer une valeur d'alias qui pointe vers l'application web.</span><span class="sxs-lookup"><span data-stu-id="c425d-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="c425d-135">À l'aide de la variable « $rs » attribuée précédemment, vous pouvez utiliser la commande PowerShell ci-dessous pour créer l'alias pour l’application web contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="c425d-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="c425d-136">L’exemple suivant est la réponse.</span><span class="sxs-lookup"><span data-stu-id="c425d-136">The following example is the response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="c425d-137">Étape 3</span><span class="sxs-lookup"><span data-stu-id="c425d-137">Step 3</span></span>

<span data-ttu-id="c425d-138">Validez vos modifications en utilisant l’applet de commande `Set-AzureRMDnsRecordSet` :</span><span class="sxs-lookup"><span data-stu-id="c425d-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="c425d-139">Vous pouvez valider l'enregistrement correctement créé en interrogeant « www.contoso.com » à l'aide de nslookup, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c425d-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="c425d-140">Créer un enregistrement « awverify » pour des applications web</span><span class="sxs-lookup"><span data-stu-id="c425d-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="c425d-141">Si vous décidez d'utiliser un enregistrement A pour votre application web, vous devez réaliser un processus de vérification pour confirmer que vous êtes le propriétaire du domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c425d-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="c425d-142">Cette étape de vérification est effectuée en créant un enregistrement CNAME spécial nommé « awverify ».</span><span class="sxs-lookup"><span data-stu-id="c425d-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="c425d-143">Cette section s’applique seulement aux enregistrements A.</span><span class="sxs-lookup"><span data-stu-id="c425d-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="c425d-144">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="c425d-144">Step 1</span></span>

<span data-ttu-id="c425d-145">Créez l’enregistrement « awverify ».</span><span class="sxs-lookup"><span data-stu-id="c425d-145">Create the "awverify" record.</span></span> <span data-ttu-id="c425d-146">Dans l’exemple ci-dessous, nous créons l’enregistrement « awverify » pour contoso.com pour vérifier la propriété du domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c425d-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="c425d-147">L’exemple suivant est la réponse.</span><span class="sxs-lookup"><span data-stu-id="c425d-147">The following example is the response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="c425d-148">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c425d-148">Step 2</span></span>

<span data-ttu-id="c425d-149">Une fois le jeu d’enregistrements « awverify » créé, affectez l’alias du jeu d’enregistrements CNAME.</span><span class="sxs-lookup"><span data-stu-id="c425d-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="c425d-150">Dans l’exemple ci-dessous, nous affectons l’alias de jeu d’enregistrements CNAME à awverify.contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="c425d-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="c425d-151">L’exemple suivant est la réponse.</span><span class="sxs-lookup"><span data-stu-id="c425d-151">The following example is the response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="c425d-152">Étape 3</span><span class="sxs-lookup"><span data-stu-id="c425d-152">Step 3</span></span>

<span data-ttu-id="c425d-153">Validez les modifications avec `Set-AzureRMDnsRecordSet cmdlet`, comme indiqué dans la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c425d-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="c425d-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c425d-154">Next steps</span></span>

<span data-ttu-id="c425d-155">Suivez la procédure décrite dans [Configuration d’un nom de domaine personnalisé pour App Service](../app-service-web/web-sites-custom-domain-name.md) pour configurer votre application web pour l’utilisation d’un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c425d-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
