---
title: "aaaHow toodelegate d’inscription et de produit abonnement d’utilisateur"
description: "Découvrez comment tooa abonnement toodelegate utilisateur d’inscription et le produit tiers de gestion des API Azure."
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
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="ec117-103">Comment les abonnement toodelegate utilisateur d’inscription et de produit</span><span class="sxs-lookup"><span data-stu-id="ec117-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="ec117-104">Délégation contrainte vous permet de toouse votre site Web existant pour la gestion des tooproducts signe-dans/connexion-haut et un abonnement de développeur en tant qu’et non pas les fonctionnalités intégrées de toousing hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="ec117-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="ec117-105">Cela permet à vos données d’utilisateur du site Web tooown hello et effectuer une validation de hello de ces étapes d’une manière personnalisée.</span><span class="sxs-lookup"><span data-stu-id="ec117-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="ec117-106"><a name="delegate-signin-up"></a>Délégation de la connexion et de l’inscription des développeurs</span><span class="sxs-lookup"><span data-stu-id="ec117-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="ec117-107">toodelegate développeur tooyour de se connecter et d’abonnement à un site Web existant que vous devez toocreate un point de terminaison spécial de délégation sur votre site qui agit en tant que hello point d’entrée pour cette demande initiée à partir du portail des développeurs gestion des API hello.</span><span class="sxs-lookup"><span data-stu-id="ec117-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="ec117-108">flux de travail final Hello seront comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec117-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="ec117-109">Développeur clique sur le lien de connexion ou d’inscription de hello en hello portail des développeurs gestion des API</span><span class="sxs-lookup"><span data-stu-id="ec117-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="ec117-110">Navigateur est redirigé toohello point de terminaison de délégation</span><span class="sxs-lookup"><span data-stu-id="ec117-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="ec117-111">Point de terminaison de délégation redirige en retour tooor présente l’interface utilisateur vous demande utilisateur dans toosign ou d’abonnement</span><span class="sxs-lookup"><span data-stu-id="ec117-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="ec117-112">En cas de réussite, utilisateur de hello est redirigé toohello arrière gestion des API développeur page du portail de qu'ils ont démarré à partir</span><span class="sxs-lookup"><span data-stu-id="ec117-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="ec117-113">toobegin, nous allons premier tooroute de gestion des API de configuration des demandes effectuées avec votre point de terminaison de délégation.</span><span class="sxs-lookup"><span data-stu-id="ec117-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="ec117-114">Dans le portail de publication de gestion des API hello, cliquez sur **sécurité** puis cliquez sur hello **délégation** onglet. Cliquez sur tooenable de case à cocher hello 'Délégué connexion & d’abonnement'.</span><span class="sxs-lookup"><span data-stu-id="ec117-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Delegation page][api-management-delegation-signin-up]

* <span data-ttu-id="ec117-116">Décider de hello les URL de votre point de terminaison spécial délégation sera être et entrez-la dans hello **URL de point de terminaison de délégation** champ.</span><span class="sxs-lookup"><span data-stu-id="ec117-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="ec117-117">Au sein de hello **clé d’authentification de délégation** champ Entrez un mot de passe sera utilisé toocompute un tooyou signature fourni pour vérification tooensure qui hello demande provient effectivement gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="ec117-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="ec117-118">Vous pouvez cliquer sur hello **générer** bouton toohave API liste générer de façon aléatoire une clé pour vous.</span><span class="sxs-lookup"><span data-stu-id="ec117-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="ec117-119">Maintenant vous devez toocreate hello **point de terminaison de délégation**.</span><span class="sxs-lookup"><span data-stu-id="ec117-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="ec117-120">Il a tooperform un certain nombre d’actions :</span><span class="sxs-lookup"><span data-stu-id="ec117-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="ec117-121">Reçoit une demande dans hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="ec117-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="ec117-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&amp;returnUrl={URL of source page}&amp;salt={string}&amp;sig={string}*</span><span class="sxs-lookup"><span data-stu-id="ec117-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="ec117-123">Paramètres de requête pour les cas de connexion / inscription hello :</span><span class="sxs-lookup"><span data-stu-id="ec117-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="ec117-124">**operation** : identifie le type de demande de délégation. Il ne peut s’agir ici que de **SignIn**</span><span class="sxs-lookup"><span data-stu-id="ec117-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="ec117-125">**returnUrl**: hello URL de page hello si utilisateur de hello l'clique sur un lien de connexion ou d’abonnement</span><span class="sxs-lookup"><span data-stu-id="ec117-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="ec117-126">**salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ec117-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="ec117-127">**SIG**: un toobe de hachage calculée de sécurité utilisé pour tooyour de comparaison propre de hachage calculé</span><span class="sxs-lookup"><span data-stu-id="ec117-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="ec117-128">Vérifiez que demande hello provient de gestion des API Azure (facultatif, mais fortement recommandé pour la sécurité)</span><span class="sxs-lookup"><span data-stu-id="ec117-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="ec117-129">Calculer un hachage HMAC-SHA512 d’une chaîne en fonction de hello **returnUrl** et **salt** des paramètres de requête ([exemple de code ci-dessous]) :</span><span class="sxs-lookup"><span data-stu-id="ec117-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="ec117-130">HMAC(**salt** + ’\n’ + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="ec117-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="ec117-131">Comparer la valeur toohello hello hello hachage calculé ci-dessus **sig** paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="ec117-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="ec117-132">Si hello deux hachages correspondent, déplacer sur l’étape suivante de toohello, sinon refuser la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ec117-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="ec117-133">Vérifiez que vous recevez une demande de connexion dans/la connexion des : hello **opération** paramètre de requête est défini trop «**SignIn**».</span><span class="sxs-lookup"><span data-stu-id="ec117-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="ec117-134">Utilisateur hello actuel avec l’interface utilisateur dans toosign ou d’abonnement</span><span class="sxs-lookup"><span data-stu-id="ec117-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="ec117-135">Si l’utilisateur hello est inscription vous avez toocreate un compte correspondant pour eux dans Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="ec117-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="ec117-136">[Créer un utilisateur] avec hello API REST de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="ec117-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="ec117-137">Lorsque vous procédez ainsi, vous assurer que hello utilisateur ID toohello même qu'il se trouve dans votre magasin de l’utilisateur ou l’ID de tooan que vous pouvez effectuer le suivi de.</span><span class="sxs-lookup"><span data-stu-id="ec117-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="ec117-138">Lorsque l’utilisateur de hello est authentifié avec succès :</span><span class="sxs-lookup"><span data-stu-id="ec117-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="ec117-139">[demander un jeton de single-sign-on (SSO)] via l’API REST de gestion des API de hello</span><span class="sxs-lookup"><span data-stu-id="ec117-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="ec117-140">Ajouter un toohello de paramètre de requête returnUrl URL SSO que vous avez reçu de l’appel d’API de hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="ec117-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="ec117-141">Par exemple, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="ec117-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="ec117-142">redirection hello utilisateur toohello ci-dessus produit URL</span><span class="sxs-lookup"><span data-stu-id="ec117-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="ec117-143">En outre toohello **SignIn** opération, vous pouvez également effectuer la gestion des comptes en suivant les étapes précédentes hello et en utilisant l’une des hello opérations suivantes.</span><span class="sxs-lookup"><span data-stu-id="ec117-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="ec117-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="ec117-144">**ChangePassword**</span></span>
* <span data-ttu-id="ec117-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="ec117-145">**ChangeProfile**</span></span>
* <span data-ttu-id="ec117-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="ec117-146">**CloseAccount**</span></span>

<span data-ttu-id="ec117-147">Vous devez passer hello suivant les paramètres de requête pour les opérations de gestion de compte.</span><span class="sxs-lookup"><span data-stu-id="ec117-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="ec117-148">**operation**: identifie le type de demande de délégation dont il s’agit (ChangePassword, ChangeProfile ou CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="ec117-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="ec117-149">**userId**: id d’utilisateur hello de hello compte toomanage</span><span class="sxs-lookup"><span data-stu-id="ec117-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="ec117-150">**salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ec117-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="ec117-151">**SIG**: un toobe de hachage calculée de sécurité utilisé pour tooyour de comparaison propre de hachage calculé</span><span class="sxs-lookup"><span data-stu-id="ec117-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="ec117-152"><a name="delegate-product-subscription"></a>Délégation de l’abonnement aux produits</span><span class="sxs-lookup"><span data-stu-id="ec117-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="ec117-153">Délégation de l’abonnement du produit fonctionne de façon similaire toodelegating utilisateur connectez-vous/à distance.</span><span class="sxs-lookup"><span data-stu-id="ec117-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="ec117-154">flux de travail final Hello devrait se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec117-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="ec117-155">Développeur sélectionne un produit dans le portail des développeurs gestion des API hello et clique sur le bouton d’abonnement hello</span><span class="sxs-lookup"><span data-stu-id="ec117-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="ec117-156">Navigateur est redirigé toohello point de terminaison de délégation</span><span class="sxs-lookup"><span data-stu-id="ec117-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="ec117-157">Point de terminaison de délégation effectue les étapes d’abonnement de produit requis - il s’agit des tooyou et peut entraîner de redirection tooanother page toorequest, informations de facturation, poser des questions supplémentaires, ou simplement le stockage d’informations de hello et ne pas nécessitant une action de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ec117-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="ec117-158">fonctionnalités de hello tooenable, sur hello **délégation** page, cliquez sur **déléguer abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ec117-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="ec117-159">Puis vérifiez le point de terminaison de délégation hello effectue hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="ec117-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="ec117-160">Reçoit une demande dans hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="ec117-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="ec117-161">*http://www.yourwebsite.com/apimdelegation?Operation= {opération} & productId = {toosubscribe produit à} & userId = {user demande} & salt = {string} & sig = {string}*</span><span class="sxs-lookup"><span data-stu-id="ec117-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="ec117-162">Paramètres de requête pour les cas d’abonnement hello produit :</span><span class="sxs-lookup"><span data-stu-id="ec117-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="ec117-163">**operation**: identifie le type de demande de délégation.</span><span class="sxs-lookup"><span data-stu-id="ec117-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="ec117-164">Pour un abonnement demandes hello les options valides sont :</span><span class="sxs-lookup"><span data-stu-id="ec117-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="ec117-165">« S’abonner » : un toosubscribe de demande hello tooa utilisateur donnée produit avec fourni d’ID (voir ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="ec117-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="ec117-166">« Vous désabonner » : un toounsubscribe demande un utilisateur à partir d’un produit</span><span class="sxs-lookup"><span data-stu-id="ec117-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="ec117-167">« Renouveler » : un toorenew demande un abonnement (par exemple, qui peut être expirer)</span><span class="sxs-lookup"><span data-stu-id="ec117-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="ec117-168">**productId**: hello des ID d’utilisateur de hello hello produit demandé toosubscribe à</span><span class="sxs-lookup"><span data-stu-id="ec117-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="ec117-169">**userId**: hello ID d’utilisateur hello pour lequel hello est demandé</span><span class="sxs-lookup"><span data-stu-id="ec117-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="ec117-170">**salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ec117-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="ec117-171">**SIG**: un toobe de hachage calculée de sécurité utilisé pour tooyour de comparaison propre de hachage calculé</span><span class="sxs-lookup"><span data-stu-id="ec117-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="ec117-172">Vérifiez que demande hello provient de gestion des API Azure (facultatif, mais fortement recommandé pour la sécurité)</span><span class="sxs-lookup"><span data-stu-id="ec117-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="ec117-173">Calcul d’un code HMAC-SHA512 d’une chaîne en fonction de hello **productId**, **userId** et **salt** des paramètres de requête :</span><span class="sxs-lookup"><span data-stu-id="ec117-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="ec117-174">HMAC(**salt** + ’\n’ + **productId** + ’\n’ + **userId**)</span><span class="sxs-lookup"><span data-stu-id="ec117-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="ec117-175">Comparer la valeur toohello hello hello hachage calculé ci-dessus **sig** paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="ec117-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="ec117-176">Si hello deux hachages correspondent, déplacer sur l’étape suivante de toohello, sinon refuser la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ec117-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="ec117-177">Exécuter tout traitement d’abonnement de produit en fonction de type hello de l’opération demandée dans **opération** -par exemple, la facturation, d’autres questions, etc..</span><span class="sxs-lookup"><span data-stu-id="ec117-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="ec117-178">Sur l’abonnement avec succès les produits de toohello hello utilisateur de votre côté, abonnez-vous au produit de gestion des API hello utilisateurs toohello par [hello appel API REST pour l’abonnement].</span><span class="sxs-lookup"><span data-stu-id="ec117-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="ec117-179"><a name="delegate-example-code"></a> Exemple de Code</span><span class="sxs-lookup"><span data-stu-id="ec117-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="ec117-180">Ces afficher des exemples de code comment tootake hello *clé de validation de délégation*toocreate un code HMAC qui est ensuite utilisé toovalidate hello signature, ce qui prouve validité hello Hello, qui est défini dans l’écran de délégation hello du portail de publication hello returnUrl passé.</span><span class="sxs-lookup"><span data-stu-id="ec117-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="ec117-181">Hello même code fonctionne pour hello productId et userId légères modifications.</span><span class="sxs-lookup"><span data-stu-id="ec117-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="ec117-182">**Hachage toogenerate code c# de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="ec117-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="ec117-183">**Hachage toogenerate NodeJS code returnUrl**</span><span class="sxs-lookup"><span data-stu-id="ec117-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="ec117-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec117-184">Next steps</span></span>
<span data-ttu-id="ec117-185">Pour plus d’informations sur la délégation, consultez hello suivant vidéo.</span><span class="sxs-lookup"><span data-stu-id="ec117-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[demander un jeton de single-sign-on (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[hello appel API REST pour l’abonnement]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[exemple de code ci-dessous]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
