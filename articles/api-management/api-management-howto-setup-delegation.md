---
title: "Délégation de l'inscription des utilisateurs et des abonnements aux produits"
description: "Découvrez comment déléguer à un tiers l'enregistrement de l'utilisateur et la souscription à des produits dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="39b79-103">Délégation de l'inscription des utilisateurs et des abonnements aux produits</span><span class="sxs-lookup"><span data-stu-id="39b79-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="39b79-104">La délégation vous permet d'utiliser votre site web existant pour gérer les connexions/inscriptions des développeurs et l'abonnement aux produits au lieu de faire appel aux fonctionnalités intégrées du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="39b79-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="39b79-105">Ceci permet à votre site web de conserver les données utilisateur et de valider ces étapes de façon personnalisée.</span><span class="sxs-lookup"><span data-stu-id="39b79-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="39b79-106"><a name="delegate-signin-up"> </a>Délégation de la connexion et de l’inscription des développeurs</span><span class="sxs-lookup"><span data-stu-id="39b79-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="39b79-107">Pour déléguer les connexions et inscriptions des développeurs à votre site web existant, vous devez créer un point de terminaison de délégation spécifique sur votre site qui agit en tant que point d'entrée pour toutes les demandes de ce type émanant du portail des développeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="39b79-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="39b79-108">Le processus final se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="39b79-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="39b79-109">Le développeur clique sur le lien de connexion ou d'inscription sur le portail des développeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="39b79-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="39b79-110">Le navigateur est redirigé vers le point de terminaison de délégation.</span><span class="sxs-lookup"><span data-stu-id="39b79-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="39b79-111">À son tour, le point de terminaison de délégation présente une interface demandant à l'utilisateur de se connecter ou de s'inscrire, ou bien le redirige vers cette interface.</span><span class="sxs-lookup"><span data-stu-id="39b79-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="39b79-112">Si l'authentification est réussie, l'utilisateur revient à la page du portail des développeurs Gestion des API d'où il est parti.</span><span class="sxs-lookup"><span data-stu-id="39b79-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="39b79-113">Pour commencer, configurons Gestion des API pour que les demandes soient acheminées via votre point de terminaison de délégation.</span><span class="sxs-lookup"><span data-stu-id="39b79-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="39b79-114">Dans le portail des éditeurs de la gestion des API, cliquez sur **Sécurité**, puis sur l’onglet **Délégation**.</span><span class="sxs-lookup"><span data-stu-id="39b79-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="39b79-115">Activez la case à cocher pour activer la connexion et l'inscription déléguées.</span><span class="sxs-lookup"><span data-stu-id="39b79-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Delegation page][api-management-delegation-signin-up]

* <span data-ttu-id="39b79-117">Décidez de l'URL de votre point de terminaison de délégation spécial, puis entrez-la dans le champ **URL du point de terminaison de délégation** .</span><span class="sxs-lookup"><span data-stu-id="39b79-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="39b79-118">Dans le champ **Clé d'authentification de la délégation** , entrez le secret utilisé pour calculer une signature qui vous sera fournie pour vérification afin de vous assurer que la demande provient bien de Gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="39b79-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="39b79-119">Vous pouvez cliquer sur le bouton **Générer** pour que la gestion des API génère de manière aléatoire une clé pour vous.</span><span class="sxs-lookup"><span data-stu-id="39b79-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="39b79-120">À présent, vous devez créer le **point de terminaison de délégation**.</span><span class="sxs-lookup"><span data-stu-id="39b79-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="39b79-121">Il doit effectuer certaines actions :</span><span class="sxs-lookup"><span data-stu-id="39b79-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="39b79-122">Recevoir une demande au format suivant :</span><span class="sxs-lookup"><span data-stu-id="39b79-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="39b79-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="39b79-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="39b79-124">Paramètres de requête pour le cas connexion/inscription :</span><span class="sxs-lookup"><span data-stu-id="39b79-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="39b79-125">**operation** : identifie le type de demande de délégation. Il ne peut s’agir ici que de **SignIn**</span><span class="sxs-lookup"><span data-stu-id="39b79-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="39b79-126">**returnUrl**: URL de la page dans laquelle l’utilisateur a cliqué sur un lien de connexion ou d’inscription</span><span class="sxs-lookup"><span data-stu-id="39b79-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="39b79-127">**salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.</span><span class="sxs-lookup"><span data-stu-id="39b79-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="39b79-128">**sig**: code de hachage de sécurité calculé à comparer avec votre propre code de hachage calculé.</span><span class="sxs-lookup"><span data-stu-id="39b79-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="39b79-129">Vérifiez si la demande émane bien de Gestion des API Azure (facultatif, mais fortement recommandé pour assurer la sécurité).</span><span class="sxs-lookup"><span data-stu-id="39b79-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="39b79-130">Calculez un code de hachage HMAC-SHA512 d’une chaîne basée sur les paramètres de requête **returnUrl** et **salt** ([exemple de code ci-dessous]) :</span><span class="sxs-lookup"><span data-stu-id="39b79-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="39b79-131">HMAC(**salt** + ’\n’ + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="39b79-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="39b79-132">Comparez le code de hachage calculé plus haut avec la valeur du paramètre de requête **sig**.</span><span class="sxs-lookup"><span data-stu-id="39b79-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="39b79-133">Si les deux codes de hachage correspondent, passez à l'étape suivante. Sinon, rejetez la demande.</span><span class="sxs-lookup"><span data-stu-id="39b79-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="39b79-134">Vérifiez que vous recevez une demande de connexion/d’inscription : le paramètre de requête **operation** sera défini sur « **SignIn** ».</span><span class="sxs-lookup"><span data-stu-id="39b79-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="39b79-135">Présentez à l'utilisateur l'interface de connexion ou d'inscription.</span><span class="sxs-lookup"><span data-stu-id="39b79-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="39b79-136">Si l'utilisateur s'inscrit, vous devez créer un compte dans Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="39b79-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="39b79-137">[Créez un utilisateur] avec l'API REST de gestion de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="39b79-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="39b79-138">Lors de cette opération, assurez-vous de bien définir l'identifiant utilisateur afin qu'il soit identique à celui de votre magasin utilisateur ou à un identifiant que vous pouvez suivre.</span><span class="sxs-lookup"><span data-stu-id="39b79-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="39b79-139">Lorsque l'utilisateur est bien authentifié :</span><span class="sxs-lookup"><span data-stu-id="39b79-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="39b79-140">[Demandez un jeton d'authentification unique (SSO)] via l'API REST Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="39b79-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="39b79-141">Ajoutez un paramètre de requête returnUrl à l'URL SSO reçue de l'appel d'API ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="39b79-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="39b79-142">Par exemple, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="39b79-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="39b79-143">Redirigez l'utilisateur vers l'URL générée.</span><span class="sxs-lookup"><span data-stu-id="39b79-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="39b79-144">En plus de l’opération **SignIn** , vous pouvez également effectuer la gestion des comptes en suivant les étapes précédentes et en utilisant l’une des opérations suivantes.</span><span class="sxs-lookup"><span data-stu-id="39b79-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="39b79-145">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="39b79-145">**ChangePassword**</span></span>
* <span data-ttu-id="39b79-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="39b79-146">**ChangeProfile**</span></span>
* <span data-ttu-id="39b79-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="39b79-147">**CloseAccount**</span></span>

<span data-ttu-id="39b79-148">Vous devez transmettre les paramètres de requête suivants pour les opérations de gestion de compte.</span><span class="sxs-lookup"><span data-stu-id="39b79-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="39b79-149">**operation**: identifie le type de demande de délégation dont il s’agit (ChangePassword, ChangeProfile ou CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="39b79-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="39b79-150">**userId**: id d’utilisateur du compte à gérer</span><span class="sxs-lookup"><span data-stu-id="39b79-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="39b79-151">**salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.</span><span class="sxs-lookup"><span data-stu-id="39b79-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="39b79-152">**sig**: code de hachage de sécurité calculé à comparer avec votre propre code de hachage calculé.</span><span class="sxs-lookup"><span data-stu-id="39b79-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="39b79-153"><a name="delegate-product-subscription"> </a>Délégation de l’abonnement aux produits</span><span class="sxs-lookup"><span data-stu-id="39b79-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="39b79-154">La délégation de l'abonnement aux produits fonctionne de la même manière que la délégation de la connexion/inscription.</span><span class="sxs-lookup"><span data-stu-id="39b79-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="39b79-155">Le processus final se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="39b79-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="39b79-156">Le développeur sélectionne un produit dans le portail des développeurs Gestion des API, puis clique sur le bouton d'abonnement.</span><span class="sxs-lookup"><span data-stu-id="39b79-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="39b79-157">Le navigateur est redirigé vers le point de terminaison de délégation.</span><span class="sxs-lookup"><span data-stu-id="39b79-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="39b79-158">Le point de terminaison de délégation effectue les étapes nécessaires pour l'abonnement au produit. Il est de votre responsabilité d'éventuellement rediriger l'utilisateur vers une autre page pour obtenir des informations de facturation, demander des informations supplémentaires ou simplement stocker les informations sans aucune action de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="39b79-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="39b79-159">Pour activer la fonctionnalité, dans la page **Délégation**, cliquez sur **Déléguer l’abonnement au produit**.</span><span class="sxs-lookup"><span data-stu-id="39b79-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="39b79-160">Assurez-vous ensuite que le point de terminaison de délégation effectue bien les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="39b79-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="39b79-161">Recevoir une demande au format suivant :</span><span class="sxs-lookup"><span data-stu-id="39b79-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="39b79-162">*http://www.yourwebsite.com/apimdelegation?operation={opération}&productId={produit auquel s’abonner}&userId={utilisateur faisant la demande}&salt={chaîne}&sig={chaîne}*</span><span class="sxs-lookup"><span data-stu-id="39b79-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="39b79-163">Paramètres de requête pour le cas abonnement à un produit :</span><span class="sxs-lookup"><span data-stu-id="39b79-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="39b79-164">**operation**: identifie le type de demande de délégation.</span><span class="sxs-lookup"><span data-stu-id="39b79-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="39b79-165">Pour l'abonnement à un produit, les options valides sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="39b79-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="39b79-166">« Subscribe » : une demande d’abonnement de l’utilisateur à un produit donné avec l’identifiant fourni (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="39b79-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="39b79-167">« Unsubscribe » : une demande de désabonnement de l’utilisateur pour un produit.</span><span class="sxs-lookup"><span data-stu-id="39b79-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="39b79-168">« Renew » : une demande de renouvellement d’abonnement (par exemple en cas d'expiration).</span><span class="sxs-lookup"><span data-stu-id="39b79-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="39b79-169">**productId**: l’ID du produit auquel l’utilisateur demande l’abonnement</span><span class="sxs-lookup"><span data-stu-id="39b79-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="39b79-170">**userId**: l’ID de l’utilisateur pour qui la demande est envoyée</span><span class="sxs-lookup"><span data-stu-id="39b79-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="39b79-171">**salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.</span><span class="sxs-lookup"><span data-stu-id="39b79-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="39b79-172">**sig**: code de hachage de sécurité calculé à comparer avec votre propre code de hachage calculé.</span><span class="sxs-lookup"><span data-stu-id="39b79-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="39b79-173">Vérifiez si la demande émane bien de Gestion des API Azure (facultatif, mais fortement recommandé pour assurer la sécurité).</span><span class="sxs-lookup"><span data-stu-id="39b79-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="39b79-174">Calculez un code de hachage HMAC-SHA512 d’une chaîne basée sur les paramètres de requête **ProductId**, **userId** et **salt** :</span><span class="sxs-lookup"><span data-stu-id="39b79-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="39b79-175">HMAC(**salt** + ’\n’ + **productId** + ’\n’ + **userId**)</span><span class="sxs-lookup"><span data-stu-id="39b79-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="39b79-176">Comparez le code de hachage calculé plus haut avec la valeur du paramètre de requête **sig**.</span><span class="sxs-lookup"><span data-stu-id="39b79-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="39b79-177">Si les deux codes de hachage correspondent, passez à l'étape suivante. Sinon, rejetez la demande.</span><span class="sxs-lookup"><span data-stu-id="39b79-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="39b79-178">Effectuez le traitement de l'abonnement au produit en fonction du type de l'opération demandée dans **operation** , par exemple facturation, autres questions, etc.</span><span class="sxs-lookup"><span data-stu-id="39b79-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="39b79-179">Après avoir correctement abonné l'utilisateur au produit de votre côté, abonnez l'utilisateur au produit Gestion des API en [appelant l'API REST pour l'abonnement au produit].</span><span class="sxs-lookup"><span data-stu-id="39b79-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="39b79-180"><a name="delegate-example-code"> </a> Exemple de Code</span><span class="sxs-lookup"><span data-stu-id="39b79-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="39b79-181">Ces exemples de code montrent comment prendre la *clé de validation de délégation*, définie dans l’écran Délégation du portail de publication, pour créer un HMAC qui permet ensuite de valider la signature, et fournit la preuve de la validité de l’élément returnUrl transmis.</span><span class="sxs-lookup"><span data-stu-id="39b79-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="39b79-182">Le même code fonctionne pour productId et userId avec de légères modifications.</span><span class="sxs-lookup"><span data-stu-id="39b79-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="39b79-183">****Code C# pour générer le hachage de returnUrl****</span><span class="sxs-lookup"><span data-stu-id="39b79-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="39b79-184">****Code NodeJS pour générer le hachage de returnUrl****</span><span class="sxs-lookup"><span data-stu-id="39b79-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="39b79-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39b79-185">Next steps</span></span>
<span data-ttu-id="39b79-186">Pour plus d’informations sur la délégation, regardez la vidéo suivante.</span><span class="sxs-lookup"><span data-stu-id="39b79-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="39b79-187">[Demandez un jeton d'authentification unique (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="39b79-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="39b79-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="39b79-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="39b79-189">[appelant l'API REST pour l'abonnement au produit]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="39b79-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="39b79-190">[exemple de code ci-dessous]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="39b79-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
