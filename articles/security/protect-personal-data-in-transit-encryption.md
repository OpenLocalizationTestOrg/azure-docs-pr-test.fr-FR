---
title: "aaaProtect des données personnelles en transit avec chiffrement dans Azure | Documents Microsoft"
description: "L’utilisation du chiffrement dans les données personnelles tooprotect Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="b24b2-103">technologies de chiffrement Azure : Protéger les données personnelles en transit avec un chiffrement</span><span class="sxs-lookup"><span data-stu-id="b24b2-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="b24b2-104">Cet article vous aidera à comprendre et utiliser les données de toosecure de technologies de chiffrement Azure en transit.</span><span class="sxs-lookup"><span data-stu-id="b24b2-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="b24b2-105">Protection confidentialité hello de données personnelles qu’il transite sur le réseau de hello est un élément essentiel d’une stratégie de sécurité de défense en profondeur multicouche.</span><span class="sxs-lookup"><span data-stu-id="b24b2-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="b24b2-106">Le chiffrement en transit est conçue tooprevent une personne malveillante qui intercepte les transmissions d’être en mesure de données de hello tooview ou l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="b24b2-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="b24b2-107">Scénario</span><span class="sxs-lookup"><span data-stu-id="b24b2-107">Scenario</span></span>

<span data-ttu-id="b24b2-108">Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée, Adriatique et mer Baltique, ainsi que hello britanniques.</span><span class="sxs-lookup"><span data-stu-id="b24b2-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="b24b2-109">toosupport ces efforts, elle a acquis plusieurs lignes croisière plus petits exercées en Italie, Allemagne, Danemark et hello Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="b24b2-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="b24b2-110">la société de Hello utilise des données d’entreprise de Microsoft Azure toostore dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="b24b2-111">Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit de sa base de clients globale.</span><span class="sxs-lookup"><span data-stu-id="b24b2-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="b24b2-112">Il inclut également des informations de ressources humaines traditionnelles telles que les adresses et numéros de téléphone, numéros d’identification de taxe médicales plus d’informations sur les employés de la société dans tous les emplacements.</span><span class="sxs-lookup"><span data-stu-id="b24b2-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="b24b2-113">ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité qui inclut des informations personnelles tootrack des relations avec les clients en cours et passées.</span><span class="sxs-lookup"><span data-stu-id="b24b2-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="b24b2-114">Les données personnelles de clients sont entrées dans la base de données hello à partir de sites distants de société hello et des agents de voyage dans Bonjour.</span><span class="sxs-lookup"><span data-stu-id="b24b2-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="b24b2-115">Documents contenant des informations sur les clients sont transférées via le stockage de tooAzure réseau hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="b24b2-116">Définition du problème</span><span class="sxs-lookup"><span data-stu-id="b24b2-116">Problem statement</span></span>

<span data-ttu-id="b24b2-117">société de Hello doit protéger la confidentialité de hello de clients et données personnelles de salariés pendant qu’il sont tooand de transit à partir des services Azure.</span><span class="sxs-lookup"><span data-stu-id="b24b2-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="b24b2-118">Objectif de l’entreprise</span><span class="sxs-lookup"><span data-stu-id="b24b2-118">Company goal</span></span>

<span data-ttu-id="b24b2-119">Hello entreprise objectif tooensure que les données personnelles sont chiffrées lorsque sur disque.</span><span class="sxs-lookup"><span data-stu-id="b24b2-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="b24b2-120">Si les personnes non autorisées interceptent les données personnelles de hello hors tension le disque, il doit être dans un formulaire qui restituera illisible.</span><span class="sxs-lookup"><span data-stu-id="b24b2-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="b24b2-121">L’application du chiffrement doit être simple, ou entièrement transparent, pour les utilisateurs et les administrateurs.</span><span class="sxs-lookup"><span data-stu-id="b24b2-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="b24b2-122">Solutions</span><span class="sxs-lookup"><span data-stu-id="b24b2-122">Solutions</span></span>

<span data-ttu-id="b24b2-123">Services Azure fournissent plusieurs toohelp d’outils et technologies vous protégez des données personnelles en transit.</span><span class="sxs-lookup"><span data-stu-id="b24b2-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="b24b2-124">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b24b2-124">Azure Storage</span></span>

<span data-ttu-id="b24b2-125">Les données stockées dans le cloud de hello doivent être déplacée à partir du client hello, qui peut être physiquement situé n’importe où dans le centre de données Azure toohello, Bonjour tout le monde.</span><span class="sxs-lookup"><span data-stu-id="b24b2-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="b24b2-126">Lorsque ces données sont récupérées par les utilisateurs, qu’elles soient à nouveau, Bonjour inverse le sens.</span><span class="sxs-lookup"><span data-stu-id="b24b2-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="b24b2-127">Données en transit sur hello Internet public est toujours au risque d’interception par des personnes malveillantes.</span><span class="sxs-lookup"><span data-stu-id="b24b2-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="b24b2-128">Il est confidentialité de hello tooprotect importantes de données personnelles à l’aide de toosecure de chiffrement au niveau du transport en tant qu’il se déplace entre les emplacements.</span><span class="sxs-lookup"><span data-stu-id="b24b2-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="b24b2-129">Hello le protocole HTTPS fournit un canal de communication sécurisé, chiffré sur hello Internet.</span><span class="sxs-lookup"><span data-stu-id="b24b2-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="b24b2-130">HTTPS doivent être des objets de tooaccess utilisé dans le stockage Azure et lors de l’appel d’API REST.</span><span class="sxs-lookup"><span data-stu-id="b24b2-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="b24b2-131">Appliquer d’utilisation du protocole HTTPS de hello lors de l’utilisation [Signatures d’accès partagé](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate tooAzure stockage DAO.</span><span class="sxs-lookup"><span data-stu-id="b24b2-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="b24b2-132">Il existe deux types de SAP : SAP de service et SAP de compte.</span><span class="sxs-lookup"><span data-stu-id="b24b2-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="b24b2-133">Comment construire une SAP de service ?</span><span class="sxs-lookup"><span data-stu-id="b24b2-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="b24b2-134">Une ressource Service SAS délégués accès tooa dans un seul des services de stockage hello (service blob, file d’attente, table ou de fichier).</span><span class="sxs-lookup"><span data-stu-id="b24b2-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="b24b2-135">tooconstruct une SAP de Service, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b24b2-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="b24b2-136">Spécifiez hello signé le champ de Version</span><span class="sxs-lookup"><span data-stu-id="b24b2-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="b24b2-137">Spécifiez hello ressource signée (objet Blob et fichier Service uniquement)</span><span class="sxs-lookup"><span data-stu-id="b24b2-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="b24b2-138">Spécifiez les paramètres de requête tooOverride les en-têtes de réponse (Service Blob et fichier Service uniquement)</span><span class="sxs-lookup"><span data-stu-id="b24b2-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="b24b2-139">Spécifiez hello nom de la Table (Table Service uniquement)</span><span class="sxs-lookup"><span data-stu-id="b24b2-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="b24b2-140">Spécifier la stratégie d’accès de hello</span><span class="sxs-lookup"><span data-stu-id="b24b2-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="b24b2-141">Spécifiez hello intervalle de validité de Signature</span><span class="sxs-lookup"><span data-stu-id="b24b2-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="b24b2-142">Spécifier des autorisations</span><span class="sxs-lookup"><span data-stu-id="b24b2-142">Specify Permissions</span></span>

9. <span data-ttu-id="b24b2-143">Spécifier l’adresse IP ou la plage d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="b24b2-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="b24b2-144">Spécifiez hello protocole HTTP</span><span class="sxs-lookup"><span data-stu-id="b24b2-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="b24b2-145">Spécifier les plages d’accès de Table</span><span class="sxs-lookup"><span data-stu-id="b24b2-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="b24b2-146">Spécifiez hello signé identificateur</span><span class="sxs-lookup"><span data-stu-id="b24b2-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="b24b2-147">Spécifiez hello Signature</span><span class="sxs-lookup"><span data-stu-id="b24b2-147">Specify hello Signature</span></span>

<span data-ttu-id="b24b2-148">Pour plus d’instructions, consultez [Construction d’une SAP de service](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="b24b2-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="b24b2-149">Comment construire une SAP de compte ?</span><span class="sxs-lookup"><span data-stu-id="b24b2-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="b24b2-150">Un compte de SAS délègue tooresources d’accès dans une ou plusieurs des services de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="b24b2-151">Vous pouvez également déléguer l’accès tooread, écriture et les opérations de suppression sur les conteneurs d’objets blob, tables, files d’attente et les partages de fichiers qui ne sont pas autorisées avec un service SAS.</span><span class="sxs-lookup"><span data-stu-id="b24b2-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="b24b2-152">Construction d’une SAP de compte est toothat similaire d’un Service.</span><span class="sxs-lookup"><span data-stu-id="b24b2-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="b24b2-153">Pour obtenir des instructions détaillées, consultez [Construction d’une SAP de compte.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="b24b2-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="b24b2-154">Comment mettre en place le protocole HTTPS lors de l’appel d’API REST ?</span><span class="sxs-lookup"><span data-stu-id="b24b2-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="b24b2-155">utilisation de hello tooenforce du protocole HTTPS lors de l’appel d’objets de tooaccess API REST de comptes de stockage, vous pouvez activer Secure transfert requis pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="b24b2-156">Bonjour portail Azure, sélectionnez **créer un compte de stockage**, ou pour un compte de stockage existant, sélectionnez **paramètres** , puis **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b24b2-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="b24b2-157">Sous **Transfert sécurisé requis**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="b24b2-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Création d’un compte de stockage](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="b24b2-159">Pour plus d’instructions, y compris comment tooenable Secure transfert requis par programme, consultez [nécessitent un transfert de sécuriser](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="b24b2-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="b24b2-160">Comment chiffrer des données dans Stockage Fichier Azure ?</span><span class="sxs-lookup"><span data-stu-id="b24b2-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="b24b2-161">tooencrypt des données en transit avec [stockage de fichiers Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), vous pouvez utiliser SMB 3.x avec Windows 8, 8.1 et 10 et Windows Server 2012 R2 et Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b24b2-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="b24b2-162">Lorsque vous utilisez le service de fichiers Azure hello, toute connexion sans chiffrement échoue lorsque « Sécuriser le transfert requis » est activée.</span><span class="sxs-lookup"><span data-stu-id="b24b2-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="b24b2-163">Cela inclut des scénarios à l’aide de SMB 2.1, SMB 3.0 sans chiffrement et certaines versions de hello client Linux SMB.</span><span class="sxs-lookup"><span data-stu-id="b24b2-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="b24b2-164">Chiffrement côté client Azure</span><span class="sxs-lookup"><span data-stu-id="b24b2-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="b24b2-165">Une autre possibilité pour protéger des données personnelles pendant leur transfert entre une application cliente et Stockage Azure consiste à utiliser un [chiffrement côté client](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="b24b2-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="b24b2-166">les données de salutation sont chiffrées avant d’être transférées dans le stockage Azure, et lorsque vous récupérez des données de hello depuis le stockage Azure, les données de salutation sont déchiffrées après sa réception côté client de hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="b24b2-167">VPN de site à site Azure</span><span class="sxs-lookup"><span data-stu-id="b24b2-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="b24b2-168">Un moyen efficace tooprotect personnel de données en transit entre un réseau d’entreprise ou un utilisateur et un réseau virtuel Azure de hello sont toouse un [site-à-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) ou [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) réseau privé virtuel (VPN, Virtual Private Network).</span><span class="sxs-lookup"><span data-stu-id="b24b2-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="b24b2-169">Une connexion VPN crée un tunnel chiffré sécurisé sur Internet de hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="b24b2-170">Comment créer une connexion VPN de site à site ?</span><span class="sxs-lookup"><span data-stu-id="b24b2-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="b24b2-171">Un VPN de site à site connecte à plusieurs utilisateurs sur tooAzure de réseau d’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="b24b2-172">toocreate une connexion site à site Bonjour portail Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b24b2-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="b24b2-173">Créez un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b24b2-173">Create a virtual network.</span></span>

2. <span data-ttu-id="b24b2-174">Spécifiez un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="b24b2-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="b24b2-175">Créer un sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="b24b2-176">Créer la passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="b24b2-177">Créer la passerelle de réseau local hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="b24b2-178">Configurez votre appareil VPN.</span><span class="sxs-lookup"><span data-stu-id="b24b2-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="b24b2-179">Créer un réseau VPN hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="b24b2-180">Vérifiez la connexion VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="b24b2-181">Pour plus d’instructions sur la connexion toocreate un site à site dans hello Azure portail, consultez [connexion de la création d’un Site à Site Bonjour portail Azure.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="b24b2-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="b24b2-182">Comment créer une connexion VPN de point à site ?</span><span class="sxs-lookup"><span data-stu-id="b24b2-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="b24b2-183">Un VPN de Point-to-Site crée une connexion sécurisée à partir d’un réseau virtuel du tooa d’ordinateur client individuel.</span><span class="sxs-lookup"><span data-stu-id="b24b2-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="b24b2-184">Cela est utile lorsque vous souhaitez tooAzure tooconnect à partir d’un emplacement distant, par exemple à partir du centre d’accueil ou un hôtel ou d’une conférence.</span><span class="sxs-lookup"><span data-stu-id="b24b2-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="b24b2-185">toocreate une connexion point-to-site Bonjour portail Azure,</span><span class="sxs-lookup"><span data-stu-id="b24b2-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="b24b2-186">Créez un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b24b2-186">Create a virtual network.</span></span>

2. <span data-ttu-id="b24b2-187">Ajoutez un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b24b2-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="b24b2-188">Spécifiez un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="b24b2-188">Specify a DNS server.</span></span> <span data-ttu-id="b24b2-189">(facultatif)</span><span class="sxs-lookup"><span data-stu-id="b24b2-189">(optional)</span></span>

4. <span data-ttu-id="b24b2-190">Créez une passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b24b2-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="b24b2-191">Générez des certificats.</span><span class="sxs-lookup"><span data-stu-id="b24b2-191">Generate certificates.</span></span>

6. <span data-ttu-id="b24b2-192">Ajouter un pool d’adresses client hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="b24b2-193">Télécharger les données de certificat public du certificat hello racine.</span><span class="sxs-lookup"><span data-stu-id="b24b2-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="b24b2-194">Générer et installer le package de configuration de client VPN hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="b24b2-195">Installez un certificat client exporté.</span><span class="sxs-lookup"><span data-stu-id="b24b2-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="b24b2-196">Se connecter tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b24b2-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="b24b2-197">Vérifiez votre connexion.</span><span class="sxs-lookup"><span data-stu-id="b24b2-197">Verify your connection.</span></span>

<span data-ttu-id="b24b2-198">Pour plus d’instructions, consultez [configurer un tooa de connexion de Point-to-Site réseau virtuel à l’aide de l’authentification par certificat : portail Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="b24b2-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="b24b2-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="b24b2-199">SSL/TLS</span></span>

<span data-ttu-id="b24b2-200">Microsoft vous recommande de toujours utiliser des données de tooexchange protocoles SSL/TLS sur les différents sites.</span><span class="sxs-lookup"><span data-stu-id="b24b2-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="b24b2-201">Les organisations qui choisissez toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove de grands jeux de données sur une liaison WAN à haut débit dédiée peut également chiffrer les données hello hello pour une protection supplémentaire à l’aide de SSL/TLS ou autres protocoles de niveau application.</span><span class="sxs-lookup"><span data-stu-id="b24b2-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="b24b2-202">Chiffrement par défaut</span><span class="sxs-lookup"><span data-stu-id="b24b2-202">Encryption by default</span></span>

<span data-ttu-id="b24b2-203">Microsoft utilise les données de tooprotect de chiffrement en transit entre les clients et services de cloud computing Azure.</span><span class="sxs-lookup"><span data-stu-id="b24b2-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="b24b2-204">Si vous interagissez avec le stockage Azure via hello portail Azure, toutes les transactions se produisent via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b24b2-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="b24b2-205">[Sécurité de la couche de transport](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) est le protocole hello que toonegotiate avec les systèmes clients qui se connectent à des services de cloud computing tooMicrosoft va tenter de centres de données Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b24b2-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="b24b2-206">TLS fournit une authentification forte, la confidentialité et l’intégrité des messages (activation de la détection de falsification, l’interception et la falsification des messages), l’interopérabilité, la flexibilité, la facilité de déploiement et l’utilisation des algorithmes.</span><span class="sxs-lookup"><span data-stu-id="b24b2-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="b24b2-207">[PFS (Perfect Forward Secrecy)](https://en.wikipedia.org/wiki/Forward_secrecy) est aussi utilisé pour que chaque connexion entre les systèmes clients des clients et les services cloud de Microsoft utilisent des clés uniques.</span><span class="sxs-lookup"><span data-stu-id="b24b2-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="b24b2-208">Services de cloud computing connexions tooMicrosoft également tirer parti du chiffrement de 2 048 bits en fonction de RSA longueurs de clé.</span><span class="sxs-lookup"><span data-stu-id="b24b2-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="b24b2-209">Hello combinaison de TLS, longueurs de clé RSA 2048 bits, et PFS rend beaucoup plus difficile pour une personne toointercept et l’accès des données en transit entre les clients et les services cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b24b2-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="b24b2-210">Les données en transit sont toujours chiffrées dans [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="b24b2-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="b24b2-211">En outre tooencrypting données toostoring préalable toopersistent média, les données de salutation sont également toujours protégées en transit à l’aide de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b24b2-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="b24b2-212">HTTPS est hello seul protocole pris en charge pour hello que REST de magasin de données Lake interfaces.</span><span class="sxs-lookup"><span data-stu-id="b24b2-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="b24b2-213">Résumé</span><span class="sxs-lookup"><span data-stu-id="b24b2-213">Summary</span></span>

<span data-ttu-id="b24b2-214">société de Hello peut accomplir son objectif de protection des données et hello confidentialité de ces données par l’application tooAzure des connexions HTTPS stockage, à l’aide de Signatures d’accès partagé et l’activation de Secure transfert requis sur les comptes de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="b24b2-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="b24b2-215">Elle peut aussi protéger les données personnelles en utilisant des connexions SMB 3.0 et en mettant en place un chiffrement côté client.</span><span class="sxs-lookup"><span data-stu-id="b24b2-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="b24b2-216">Connexions VPN de site à site à partir de hello réseau d’entreprise toohello réseau virtuel Azure et les connexions VPN de point-to-site auprès des utilisateurs crée un tunnel sécurisé par le biais duquel peuvent voyager en toute sécurité des données personnelles.</span><span class="sxs-lookup"><span data-stu-id="b24b2-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="b24b2-217">Pratiques de chiffrement par défaut de Microsoft protège davantage confidentialité hello des données personnelles.</span><span class="sxs-lookup"><span data-stu-id="b24b2-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b24b2-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b24b2-218">Next steps</span></span>

- [<span data-ttu-id="b24b2-219">Bonnes pratiques Azure en matière de chiffrement et de sécurité des données</span><span class="sxs-lookup"><span data-stu-id="b24b2-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="b24b2-220">Planification et conception de la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="b24b2-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="b24b2-221">FAQ sur la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="b24b2-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="b24b2-222">Acheter et configurer un certificat SSL pour votre service Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b24b2-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
