---
title: "Activer HTTPS sur un domaine personnalisé Azure CDN | Microsoft Docs"
description: "Découvrez comment activer HTTPS sur votre point de terminaison Azure CDN avec un domaine personnalisé."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="b1f33-103">Activer HTTPS sur un domaine personnalisé Azure CDN</span><span class="sxs-lookup"><span data-stu-id="b1f33-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="b1f33-104">La prise en charge de HTTPS pour les domaines personnalisés Azure CDN vous permet de diffuser du contenu sécurisé via SSL à l’aide de votre propre nom de domaine afin d’améliorer la sécurité des données lors de leur transit.</span><span class="sxs-lookup"><span data-stu-id="b1f33-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="b1f33-105">Le workflow de bout en bout visant à activer HTTPS pour votre domaine personnalisé est simplifié via l’activation en un clic et la gestion complète des certificats, le tout sans coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="b1f33-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="b1f33-106">Il est essentiel de garantir la confidentialité et l’intégrité de toutes les données sensibles de vos applications web lors de leur transit.</span><span class="sxs-lookup"><span data-stu-id="b1f33-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="b1f33-107">L’utilisation du protocole HTTPS garantit que vos données sensibles sont chiffrées lorsqu’elles sont envoyées sur Internet.</span><span class="sxs-lookup"><span data-stu-id="b1f33-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="b1f33-108">Il assure la confiance et l’authentification, mais protège également vos applications web contre les attaques.</span><span class="sxs-lookup"><span data-stu-id="b1f33-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="b1f33-109">Actuellement, Azure CDN prend en charge HTTPS sur un point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="b1f33-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="b1f33-110">Ainsi, si vous créez un point de terminaison CDN à partir d’Azure CDN (par exemple, https://contoso.azureedge.net), HTTPS est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="b1f33-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="b1f33-111">Désormais, avec HTTPS sur votre domaine personnalisé, vous pouvez également activer la fourniture sécurisée pour un domaine personnalisé (par exemple, https://www.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="b1f33-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="b1f33-112">Voici quelques-uns des attributs clés de la fonctionnalité HTTPS :</span><span class="sxs-lookup"><span data-stu-id="b1f33-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="b1f33-113">Aucun coût supplémentaire : l’acquisition ou le renouvellement de certificat n’entraîne aucun coût supplémentaire, tout comme le trafic HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b1f33-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="b1f33-114">Vous payez uniquement pour l’acheminement des Go du CDN.</span><span class="sxs-lookup"><span data-stu-id="b1f33-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="b1f33-115">Activation simple : l’approvisionnement en un clic est disponible à partir du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1f33-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b1f33-116">Vous pouvez également utiliser l’API REST ou d’autres outils de développeur pour activer la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b1f33-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="b1f33-117">Gestion complète de certificats : l’approvisionnement et la gestion de tous les certificats sont assurés pour vous.</span><span class="sxs-lookup"><span data-stu-id="b1f33-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="b1f33-118">Les certificats sont automatiquement approvisionnés et renouvelés avant l’expiration.</span><span class="sxs-lookup"><span data-stu-id="b1f33-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="b1f33-119">Cela élimine tout risque d’interruption de service suite à une expiration du certificat.</span><span class="sxs-lookup"><span data-stu-id="b1f33-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="b1f33-120">Avant d’activer la prise en charge du protocole HTTPS, vous devez avoir déjà établi un [domaine personnalisé Azure CDN](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b1f33-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="b1f33-121">Étape 1 : Activation de la fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="b1f33-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="b1f33-122">Dans le [portail Azure](https://portal.azure.com), accédez à votre profil CDN Verizon Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="b1f33-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="b1f33-123">Dans la liste des points de terminaison, cliquez sur celui contenant votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b1f33-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="b1f33-124">Cliquez sur le domaine personnalisé pour lequel vous souhaitez activer le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b1f33-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![Panneau Point de terminaison](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="b1f33-126">Cliquez sur **Activé** pour activer HTTPS et enregistrez la modification.</span><span class="sxs-lookup"><span data-stu-id="b1f33-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![Boîte de dialogue HTTPS personnalisé](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="b1f33-128">Étape 2 : Validation du domaine</span><span class="sxs-lookup"><span data-stu-id="b1f33-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="b1f33-129">Vous devez effectuer la validation de domaine avant que le protocole HTTPS soit activé sur votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b1f33-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="b1f33-130">Vous disposez de 6 jours ouvrables pour approuver le domaine.</span><span class="sxs-lookup"><span data-stu-id="b1f33-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="b1f33-131">La demande sera annulée si aucune approbation n’intervient dans ce délai.</span><span class="sxs-lookup"><span data-stu-id="b1f33-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="b1f33-132">Une fois le protocole HTTPS activé sur votre domaine personnalisé, notre fournisseur de certificat HTTPS DigiCert validera la propriété de votre domaine en contactant l’inscrit pour ce domaine, en fonction des informations sur l’inscrit WHOIS, par e-mail (par défaut) ou par téléphone.</span><span class="sxs-lookup"><span data-stu-id="b1f33-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="b1f33-133">DigiCert enverra également l’e-mail de vérification aux adresses suivantes.</span><span class="sxs-lookup"><span data-stu-id="b1f33-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="b1f33-134">Si les informations sur l’inscrit whois sont privées, vérifiez que vous pouvez effectuer directement l’approbation à partir de ces adresses.</span><span class="sxs-lookup"><span data-stu-id="b1f33-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="b1f33-135">admin@<votre-nom-de-domaine.com> administrator@<votre-nom-de-domaine.com></span><span class="sxs-lookup"><span data-stu-id="b1f33-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="b1f33-136">webmaster@<votre-nom-de-domaine.com></span><span class="sxs-lookup"><span data-stu-id="b1f33-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="b1f33-137">hostmaster@<votre-nom-de-domaine.com></span><span class="sxs-lookup"><span data-stu-id="b1f33-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="b1f33-138">postmaster@<votre-nom-de-domaine.com></span><span class="sxs-lookup"><span data-stu-id="b1f33-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="b1f33-139">Lors de la réception de l’e-mail, vous avez deux options de vérification :</span><span class="sxs-lookup"><span data-stu-id="b1f33-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="b1f33-140">Vous pouvez approuver toutes les commandes futures passées via le même compte pour le même domaine racine, par exemple, consoto.com.</span><span class="sxs-lookup"><span data-stu-id="b1f33-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="b1f33-141">Il s’agit de l’approche recommandée si vous envisagez d’ajouter d’autres domaines personnalisés à l’avenir pour le même domaine racine.</span><span class="sxs-lookup"><span data-stu-id="b1f33-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="b1f33-142">Vous pouvez approuver simplement le nom d’hôte spécifique utilisé dans cette demande.</span><span class="sxs-lookup"><span data-stu-id="b1f33-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="b1f33-143">L’approbation supplémentaire sera nécessaire pour les demandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="b1f33-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="b1f33-144">Exemple d’e-mail :</span><span class="sxs-lookup"><span data-stu-id="b1f33-144">Example email:</span></span>
    
    ![Boîte de dialogue HTTPS personnalisé](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="b1f33-146">Après l’approbation, DigiCert ajoutera votre nom de domaine personnalisé au certificat SAN.</span><span class="sxs-lookup"><span data-stu-id="b1f33-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="b1f33-147">Le certificat est valide pendant un an et sera automatiquement renouvelé avant son expiration.</span><span class="sxs-lookup"><span data-stu-id="b1f33-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="b1f33-148">Étape 3 : Attente de la propagation et utilisation de votre fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="b1f33-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="b1f33-149">Une fois que le nom de domaine est validé, cela prendra jusqu’à 6 à 8 heures pour activer la fonctionnalité HTTPS de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b1f33-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="b1f33-150">Une fois le processus terminé, l’état « HTTPS personnalisé » dans le portail Azure sera défini sur « Activé ».</span><span class="sxs-lookup"><span data-stu-id="b1f33-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="b1f33-151">Le protocole HTTPS avec votre domaine personnalisé est maintenant prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="b1f33-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="b1f33-152">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="b1f33-152">Frequently asked questions</span></span>

1. <span data-ttu-id="b1f33-153">*Qui est le fournisseur de certificats et quel est le type de certificat utilisé ?*</span><span class="sxs-lookup"><span data-stu-id="b1f33-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="b1f33-154">Nous utilisons le certificat SAN (Subject Alternative Names) fourni par DigiCert.</span><span class="sxs-lookup"><span data-stu-id="b1f33-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="b1f33-155">Un certificat SAN peut sécuriser plusieurs noms de domaine qualifiés complets avec un certificat.</span><span class="sxs-lookup"><span data-stu-id="b1f33-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="b1f33-156">*Puis-je utiliser mon certificat dédié ?*</span><span class="sxs-lookup"><span data-stu-id="b1f33-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="b1f33-157">Pas actuellement, mais nous y travaillons.</span><span class="sxs-lookup"><span data-stu-id="b1f33-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="b1f33-158">*Que se passe-t-il si je ne reçois pas l’e-mail de vérification de domaine de DigiCert ?*</span><span class="sxs-lookup"><span data-stu-id="b1f33-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="b1f33-159">Contactez Microsoft si vous ne recevez pas l’e-mail dans les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="b1f33-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="b1f33-160">*Un certificat SAN est-il moins sécurisé qu’un certificat dédié ?*</span><span class="sxs-lookup"><span data-stu-id="b1f33-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="b1f33-161">Un certificat SAN suit les mêmes normes de sécurité et de chiffrement qu’un certificat dédié.</span><span class="sxs-lookup"><span data-stu-id="b1f33-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="b1f33-162">Tous les certificats SSL émis utilisent la norme SHA-256 pour une sécurité améliorée du serveur.</span><span class="sxs-lookup"><span data-stu-id="b1f33-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="b1f33-163">*Puis-je utiliser le protocole HTTPS de domaine personnalisé avec Azure CDN Akamai ?*</span><span class="sxs-lookup"><span data-stu-id="b1f33-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="b1f33-164">Actuellement, cette fonctionnalité est uniquement disponible avec Azure CDN Verizon.</span><span class="sxs-lookup"><span data-stu-id="b1f33-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="b1f33-165">Nous travaillons pour que la prise en charge de cette fonctionnalité par Azure CDN Akamai soit disponible dans les prochains mois.</span><span class="sxs-lookup"><span data-stu-id="b1f33-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b1f33-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1f33-166">Next steps</span></span>

- <span data-ttu-id="b1f33-167">Découvrez comment configurer un [domaine personnalisé sur votre point de terminaison Azure CDN](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="b1f33-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


