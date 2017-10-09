---
title: "guide de dépannage DNS aaaAzure | Documents Microsoft"
description: "Comment tootroubleshoot commun problèmes avec le système DNS Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="e6dff-103">Guide de résolution des problèmes d’Azure DNS</span><span class="sxs-lookup"><span data-stu-id="e6dff-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="e6dff-104">Cette page fournit des informations de résolution des problèmes pour les questions Azure DNS les plus fréquentes.</span><span class="sxs-lookup"><span data-stu-id="e6dff-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="e6dff-105">Si cette procédure ne résout pas votre problème, vous pouvez également rechercher ou publier votre problème sur notre [forum de support communautaire sur MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="e6dff-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="e6dff-106">Vous pouvez également ouvrir une demande de support Azure.</span><span class="sxs-lookup"><span data-stu-id="e6dff-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="e6dff-107">Impossible de créer une zone DNS</span><span class="sxs-lookup"><span data-stu-id="e6dff-107">I can't create a DNS zone</span></span>

<span data-ttu-id="e6dff-108">tooresolve les problèmes courants, essayez une ou plusieurs des hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e6dff-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="e6dff-109">Hello de révision de l’audit Azure DNS enregistre la raison de l’échec toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="e6dff-110">Chaque nom de zone DNS doit être unique au sein de son groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e6dff-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="e6dff-111">Autrement dit, deux zones DNS avec hello même nom ne peuvent pas partager un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e6dff-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="e6dff-112">Essayez d’utiliser un autre nom de zone ou un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e6dff-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="e6dff-113">Vous pouvez voir une erreur « Vous avez atteint ou dépassé le nombre maximal de hello de zones dans l’abonnement {id d’abonnement}. »</span><span class="sxs-lookup"><span data-stu-id="e6dff-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="e6dff-114">Soit utiliser un autre abonnement Azure, supprimez certaines zones ou contactez le Support Azure tooraise votre limite d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="e6dff-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="e6dff-115">Vous pouvez voir une erreur « zone de hello '{nom de zone}' n’est pas disponible. »</span><span class="sxs-lookup"><span data-stu-id="e6dff-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="e6dff-116">Cette erreur signifie que le système DNS Azure était impossible tooallocate des serveurs de noms de cette zone DNS.</span><span class="sxs-lookup"><span data-stu-id="e6dff-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="e6dff-117">Essayez d’utiliser un autre nom de zone.</span><span class="sxs-lookup"><span data-stu-id="e6dff-117">Try using a different zone name.</span></span> <span data-ttu-id="e6dff-118">Ou bien, si vous êtes propriétaire du nom de domaine hello, contactez le support Azure, ce qui peut allouer des serveurs de noms pour vous.</span><span class="sxs-lookup"><span data-stu-id="e6dff-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="e6dff-119">**Documents recommandés**</span><span class="sxs-lookup"><span data-stu-id="e6dff-119">**Recommended documents**</span></span>

<span data-ttu-id="e6dff-120">[Enregistrements et zones DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="e6dff-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="e6dff-121">
[Création d’une zone DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e6dff-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="e6dff-122">Impossible de créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="e6dff-122">I can't create a DNS record</span></span>

<span data-ttu-id="e6dff-123">tooresolve les problèmes courants, essayez une ou plusieurs des hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e6dff-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="e6dff-124">Hello de révision de l’audit Azure DNS enregistre la raison de l’échec toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="e6dff-125">Jeu d’enregistrements hello existe déjà ?</span><span class="sxs-lookup"><span data-stu-id="e6dff-125">Does hello record set exist already?</span></span>  <span data-ttu-id="e6dff-126">DNS Azure gère les enregistrements à l’aide d’enregistrement *définit*, qui sont la collection hello d’enregistrements de hello même nom et hello même type.</span><span class="sxs-lookup"><span data-stu-id="e6dff-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="e6dff-127">Si un enregistrement hello même nom et le type déjà existe, puis tooadd un autre tel enregistrement, vous devez modifier hello enregistrement existant définie.</span><span class="sxs-lookup"><span data-stu-id="e6dff-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="e6dff-128">Vous essayez de toocreate un enregistrement au sommet de zone DNS hello (hello « root » de la zone de hello) ?</span><span class="sxs-lookup"><span data-stu-id="e6dff-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="e6dff-129">Si hello convention DNS est donc toouse hello ' @' caractère en tant que nom de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="e6dff-130">Notez également que les normes DNS hello n’autorisent pas les enregistrements CNAME au sommet de zone hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="e6dff-131">Constatez-vous un conflit d’enregistrement CNAME ?</span><span class="sxs-lookup"><span data-stu-id="e6dff-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="e6dff-132">les normes DNS Hello ne permettent pas d’un enregistrement CNAME avec le même nom qu’un enregistrement d’un autre type de hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="e6dff-133">Si vous avez un CNAME existant, création d’un enregistrement avec hello échoue du même nom d’un type différent.</span><span class="sxs-lookup"><span data-stu-id="e6dff-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="e6dff-134">De même, la création d’un enregistrement CNAME échoue si le nom de hello correspond à un enregistrement existant d’un type différent.</span><span class="sxs-lookup"><span data-stu-id="e6dff-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="e6dff-135">Supprimer les conflits hello en supprimant les hello autre enregistrement ou choisir un nom de l’autre enregistrement.</span><span class="sxs-lookup"><span data-stu-id="e6dff-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="e6dff-136">Vous avez atteint hello hello nombre limite de jeux d’enregistrements autorisé dans une zone DNS ? Nombre actuel de Hello d’enregistrement définit et hello nombre maximal de jeux d’enregistrements est affiché dans hello portail Azure, sous « Propriétés hello » pour la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="e6dff-137">Si vous avez atteint cette limite, puis supprimez certains jeux d’enregistrements ou contactez le Support Azure tooraise votre limite de jeu d’enregistrements pour cette zone, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="e6dff-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="e6dff-138">**Documents recommandés**</span><span class="sxs-lookup"><span data-stu-id="e6dff-138">**Recommended documents**</span></span>

<span data-ttu-id="e6dff-139">[Enregistrements et zones DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="e6dff-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="e6dff-140">
[Création d’une zone DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e6dff-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="e6dff-141">Impossible de résoudre mon enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="e6dff-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="e6dff-142">La résolution de noms DNS est un processus en plusieurs étapes. Elle peut échouer pour de nombreuses raisons.</span><span class="sxs-lookup"><span data-stu-id="e6dff-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="e6dff-143">Hello étapes suivantes vous aider à identifier pourquoi la résolution DNS échoue pour un enregistrement DNS dans une zone hébergée dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="e6dff-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="e6dff-144">Vérifiez que les enregistrements DNS hello ont été configurées correctement dans le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="e6dff-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="e6dff-145">Passez en revue les enregistrements DNS de hello Bonjour portail Azure, la vérification que le nom de la zone hello, nom de l’enregistrement et type d’enregistrement sont corrects.</span><span class="sxs-lookup"><span data-stu-id="e6dff-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="e6dff-146">Vérifiez que les enregistrements DNS hello résoudre correctement sur les serveurs DNS de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="e6dff-147">Si vous effectuez des requêtes DNS à partir de votre ordinateur local, vous pouvez voir les résultats mis en cache qui ne reflètent l’état actuel de hello hello de serveurs de noms.</span><span class="sxs-lookup"><span data-stu-id="e6dff-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="e6dff-148">En outre, les réseaux d’entreprise utilisent souvent des serveurs proxy DNS, ce qui empêche les requêtes DNS dirigées vers les serveurs de noms toospecific.</span><span class="sxs-lookup"><span data-stu-id="e6dff-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="e6dff-149">tooavoid ces problèmes, utilisez un service de résolution de nom basée sur le web telles que [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="e6dff-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="e6dff-150">Être toospecify que des serveurs de nom correct de hello pour votre zone DNS, comme indiqué dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e6dff-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="e6dff-151">Vérifiez que nom DNS de hello est correct (vous avez toospecify hello complet nom, y compris le nom de la zone hello) et le type d’enregistrement hello est correct</span><span class="sxs-lookup"><span data-stu-id="e6dff-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="e6dff-152">Vérifiez que nom de domaine DNS hello a été correctement [délégué des serveurs DNS de Azure toohello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="e6dff-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="e6dff-153">[De nombreux sites web tiers proposent la validation de délégation DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="e6dff-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="e6dff-154">Ce test est un *zone* test de délégation, donc vous devez uniquement entrer un nom de zone DNS hello et pas hello enregistrement nom complet.</span><span class="sxs-lookup"><span data-stu-id="e6dff-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="e6dff-155">Une fois terminée hello ci-dessus, votre enregistrement DNS doit maintenant correctement résolues.</span><span class="sxs-lookup"><span data-stu-id="e6dff-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="e6dff-156">tooverify, vous pouvez à nouveau utiliser [digwebinterface](http://digwebinterface.com), cette fois à l’aide des paramètres de serveur de nom hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="e6dff-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="e6dff-157">**Documents recommandés**</span><span class="sxs-lookup"><span data-stu-id="e6dff-157">**Recommended documents**</span></span>

[<span data-ttu-id="e6dff-158">Déléguer un tooAzure de domaine DNS</span><span class="sxs-lookup"><span data-stu-id="e6dff-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="e6dff-159">Comment spécifier hello « service » et « protocole » pour un enregistrement SRV ?</span><span class="sxs-lookup"><span data-stu-id="e6dff-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="e6dff-160">DNS Azure gère les enregistrements DNS en tant que jeux d’enregistrements : hello ensemble d’enregistrements par hello même nom et hello même type.</span><span class="sxs-lookup"><span data-stu-id="e6dff-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="e6dff-161">Pour un jeu d’enregistrements SRV, hello « service » et « protocole » doivent toobe spécifié en tant que partie du nom du jeu d’enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="e6dff-162">Hello autres paramètres SRV ('priority', « weight », « port » et « cible ») sont spécifiés séparément pour chaque enregistrement dans le jeu d’enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="e6dff-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="e6dff-163">Exemples de noms d’enregistrement SRV (nom de service « sip », protocole « tcp ») :</span><span class="sxs-lookup"><span data-stu-id="e6dff-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="e6dff-164">\_SIP. \_tcp (qui crée un enregistrement défini au sommet de zone hello)</span><span class="sxs-lookup"><span data-stu-id="e6dff-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="e6dff-165">\_sip.\_tcp.sipservice (crée un jeu d’enregistrements nommé « sipservice »)</span><span class="sxs-lookup"><span data-stu-id="e6dff-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="e6dff-166">**Documents recommandés**</span><span class="sxs-lookup"><span data-stu-id="e6dff-166">**Recommended documents**</span></span>

<span data-ttu-id="e6dff-167">[Enregistrements et zones DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="e6dff-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="e6dff-168">
[Créer des jeux d’enregistrements DNS et les enregistrements à l’aide de hello portail Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="e6dff-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="e6dff-169">
[Type d’enregistrement SRV (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="e6dff-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="e6dff-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6dff-170">Next steps</span></span>

* <span data-ttu-id="e6dff-171">En savoir plus sur les [Enregistrements et zones DNS](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="e6dff-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="e6dff-172">toostart à l’aide de DNS Azure, découvrez comment trop[créer une zone DNS](dns-getstarted-create-dnszone-portal.md) et [créer des enregistrements DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6dff-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="e6dff-173">toomigrate une zone DNS existante, découvrez comment trop[importer et exporter un fichier de zone DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="e6dff-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

