---
title: "AAA « activer HTTPS sur un domaine personnalisé CDN Azure | Documents Microsoft »"
description: "Découvrez comment tooenable HTTPS sur votre point de terminaison CDN Azure avec un domaine personnalisé."
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
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="0b038-103">Activer HTTPS sur un domaine personnalisé Azure CDN</span><span class="sxs-lookup"><span data-stu-id="0b038-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="0b038-104">Prise en charge HTTPS pour les domaines personnalisés CDN Azure vous permet de toodeliver de contenu sécurisée via SSL à l’aide de votre propre sécurité hello de domaine nom tooimprove de données en cours de transit.</span><span class="sxs-lookup"><span data-stu-id="0b038-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="0b038-105">tooenable de flux de travail de bout en bout Hello HTTPS pour votre domaine personnalisé est simplifié via l’activation en un clic, la gestion des certificats terminée et toutes les données avec sans coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="0b038-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="0b038-106">Il s’agit de confidentialité de hello tooensure critiques et l’intégrité des données de toutes les données sensibles applications web en cours de transit.</span><span class="sxs-lookup"><span data-stu-id="0b038-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="0b038-107">À l’aide de hello le protocole HTTPS garantit que vos données sensibles sont chiffrées lorsqu’elles sont envoyées sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="0b038-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="0b038-108">Il assure la confiance et l’authentification, mais protège également vos applications web contre les attaques.</span><span class="sxs-lookup"><span data-stu-id="0b038-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="0b038-109">Actuellement, Azure CDN prend en charge HTTPS sur un point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="0b038-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="0b038-110">Ainsi, si vous créez un point de terminaison CDN à partir d’Azure CDN (par exemple, https://contoso.azureedge.net), HTTPS est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="0b038-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="0b038-111">Désormais, avec HTTPS sur votre domaine personnalisé, vous pouvez également activer la fourniture sécurisée pour un domaine personnalisé (par exemple, https://www.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="0b038-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="0b038-112">Certains des attributs de clé hello de fonctionnalité HTTPS sont :</span><span class="sxs-lookup"><span data-stu-id="0b038-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="0b038-113">Aucun coût supplémentaire : l’acquisition ou le renouvellement de certificat n’entraîne aucun coût supplémentaire, tout comme le trafic HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0b038-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="0b038-114">Vous payez uniquement pour les sorties Go à partir de hello CDN.</span><span class="sxs-lookup"><span data-stu-id="0b038-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="0b038-115">L’activation du simple : cliquez sur un l'approvisionnement est disponible à partir de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0b038-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0b038-116">Vous pouvez également utiliser l’API REST ou autre fonctionnalité de hello tooenable developer tools.</span><span class="sxs-lookup"><span data-stu-id="0b038-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="0b038-117">Gestion complète de certificats : l’approvisionnement et la gestion de tous les certificats sont assurés pour vous.</span><span class="sxs-lookup"><span data-stu-id="0b038-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="0b038-118">Les certificats sont automatiquement configurés et renouvellement tooexpiration préalable.</span><span class="sxs-lookup"><span data-stu-id="0b038-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="0b038-119">Cette opération supprime complètement risques hello d’interruption de service à la suite d’une expiration du certificat.</span><span class="sxs-lookup"><span data-stu-id="0b038-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="0b038-120">Tooenabling préalable support HTTPS, vous devez avoir déjà établi un [domaine Azure CDN personnalisé](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="0b038-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="0b038-121">Étape 1 : Activer la fonctionnalité de hello</span><span class="sxs-lookup"><span data-stu-id="0b038-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="0b038-122">Bonjour [portail Azure](https://portal.azure.com), recherchez le profil CDN tooyour Verizon standard ou premium.</span><span class="sxs-lookup"><span data-stu-id="0b038-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="0b038-123">Dans hello de points de terminaison, cliquez sur le point de terminaison hello contenant votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0b038-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="0b038-124">Cliquez sur le domaine personnalisé de hello pour lequel vous souhaitez tooenable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0b038-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![Panneau Point de terminaison](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="0b038-126">Cliquez sur **sur** tooenable HTTPS, puis enregistrez les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="0b038-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![Boîte de dialogue HTTPS personnalisé](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="0b038-128">Étape 2 : Validation du domaine</span><span class="sxs-lookup"><span data-stu-id="0b038-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="0b038-129">Vous devez effectuer la validation de domaine avant que le protocole HTTPS soit activé sur votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0b038-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="0b038-130">Vous avez 6 jours tooapprove hello domaine.</span><span class="sxs-lookup"><span data-stu-id="0b038-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="0b038-131">La demande sera annulée si aucune approbation n’intervient dans ce délai.</span><span class="sxs-lookup"><span data-stu-id="0b038-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="0b038-132">Après l’activation de HTTPS sur votre domaine personnalisé, notre fournisseur du certificat HTTPS DigiCert validera la propriété de votre domaine en contactant un abonné de hello pour votre domaine, en fonction des informations d’abonné WHOIS, par courrier électronique (par défaut) ou par téléphone.</span><span class="sxs-lookup"><span data-stu-id="0b038-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="0b038-133">DigiCert envoie également toohello de courrier électronique de vérification hello adresses suivantes.</span><span class="sxs-lookup"><span data-stu-id="0b038-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="0b038-134">Si les informations sur l’inscrit whois sont privées, vérifiez que vous pouvez effectuer directement l’approbation à partir de ces adresses.</span><span class="sxs-lookup"><span data-stu-id="0b038-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="0b038-135">admin@<votre-nom-de-domaine.com> administrator@<votre-nom-de-domaine.com></span><span class="sxs-lookup"><span data-stu-id="0b038-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="0b038-136">webmaster@<votre-nom-de-domaine.com></span><span class="sxs-lookup"><span data-stu-id="0b038-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="0b038-137">hostmaster@<votre-nom-de-domaine.com></span><span class="sxs-lookup"><span data-stu-id="0b038-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="0b038-138">postmaster@<votre-nom-de-domaine.com></span><span class="sxs-lookup"><span data-stu-id="0b038-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="0b038-139">Lors de la réception de courrier électronique de hello, vous avez deux options de vérification :</span><span class="sxs-lookup"><span data-stu-id="0b038-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="0b038-140">Vous pouvez approuver toutes les futures commandes placées via hello même compte pour hello même domaine racine, par exemple, consoto.com. Cette approche est recommandée si vous envisagez de domaines personnalisés supplémentaires de tooadd Bonjour future pour hello même domaine racine.</span><span class="sxs-lookup"><span data-stu-id="0b038-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="0b038-141">Vous pouvez simplement l’approuver nom d’hôte spécifique hello utilisée dans cette demande.</span><span class="sxs-lookup"><span data-stu-id="0b038-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="0b038-142">L’approbation supplémentaire sera nécessaire pour les demandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="0b038-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="0b038-143">Exemple d’e-mail :</span><span class="sxs-lookup"><span data-stu-id="0b038-143">Example email:</span></span>
    
    ![Boîte de dialogue HTTPS personnalisé](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="0b038-145">Après l’approbation, DigiCert ajouterez votre certificat de SAN de toohello de nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0b038-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="0b038-146">certificat de Hello est valide pendant un an et sera automatiquement renouvelé avant qu’il a expiré.</span><span class="sxs-lookup"><span data-stu-id="0b038-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="0b038-147">Étape 3 : Attendez que la propagation hello puis démarrer à l’aide de la fonction</span><span class="sxs-lookup"><span data-stu-id="0b038-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="0b038-148">Après la validation de nom de domaine hello il occupera too6-8 heures pour la fonctionnalité hello domaine personnalisé HTTPS toobe active.</span><span class="sxs-lookup"><span data-stu-id="0b038-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="0b038-149">Une fois hello est terminée, l’état « HTTPS personnalisé » hello Bonjour portail Azure est défini trop « activé ».</span><span class="sxs-lookup"><span data-stu-id="0b038-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="0b038-150">Le protocole HTTPS avec votre domaine personnalisé est maintenant prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="0b038-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="0b038-151">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="0b038-151">Frequently asked questions</span></span>

1. <span data-ttu-id="0b038-152">*Qui est le fournisseur de certificats hello et le type de certificat est utilisé ?*</span><span class="sxs-lookup"><span data-stu-id="0b038-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="0b038-153">Nous utilisons le certificat SAN (Subject Alternative Names) fourni par DigiCert.</span><span class="sxs-lookup"><span data-stu-id="0b038-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="0b038-154">Un certificat SAN peut sécuriser plusieurs noms de domaine qualifiés complets avec un certificat.</span><span class="sxs-lookup"><span data-stu-id="0b038-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="0b038-155">*Puis-je utiliser mon certificat dédié ?*</span><span class="sxs-lookup"><span data-stu-id="0b038-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="0b038-156">Pas actuellement, mais son on hello feuille de route.</span><span class="sxs-lookup"><span data-stu-id="0b038-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="0b038-157">*Que se passe-t-il si je ne plus recevoir par courrier électronique de vérification de domaine hello de DigiCert ?*</span><span class="sxs-lookup"><span data-stu-id="0b038-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="0b038-158">Contactez Microsoft si vous ne recevez pas l’e-mail dans les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="0b038-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="0b038-159">*Un certificat SAN est-il moins sécurisé qu’un certificat dédié ?*</span><span class="sxs-lookup"><span data-stu-id="0b038-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="0b038-160">Un certificat SAN suit hello mêmes normes de chiffrement et de sécurité comme un certificat dédié. Tous les certificats SSL émis utilisent la norme SHA-256 pour une sécurité améliorée du serveur.</span><span class="sxs-lookup"><span data-stu-id="0b038-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="0b038-161">*Puis-je utiliser le protocole HTTPS de domaine personnalisé avec Azure CDN Akamai ?*</span><span class="sxs-lookup"><span data-stu-id="0b038-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="0b038-162">Actuellement, cette fonctionnalité est uniquement disponible avec Azure CDN Verizon.</span><span class="sxs-lookup"><span data-stu-id="0b038-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="0b038-163">Nous travaillons sur la prise en charge de cette fonctionnalité avec le CDN Azure à partir d’Akamai dans les mois à venir hello.</span><span class="sxs-lookup"><span data-stu-id="0b038-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0b038-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b038-164">Next steps</span></span>

- <span data-ttu-id="0b038-165">Découvrez comment tooset d’un [domaine personnalisé sur votre point de terminaison CDN Azure](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="0b038-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


