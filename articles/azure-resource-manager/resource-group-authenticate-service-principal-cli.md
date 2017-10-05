---
title: "Créer une identité pour une application Azure avec Azure CLI | Microsoft Docs"
description: "Explique comment utiliser Azure CLI pour créer une application et un principal du service Azure Active Directory, et comment accorder à l’application l’accès aux ressources par le biais du contrôle d’accès en fonction du rôle. Cet article montre comment authentifier l’application avec un mot de passe ou un certificat."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="d0f3c-104">Créer un principal du service pour accéder aux ressources à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d0f3c-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="d0f3c-105">Lorsque vous avez une application ou un script qui doit pouvoir accéder à des ressources, vous pouvez configurer une identité pour l’application et authentifier l’application avec ses propres informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="d0f3c-106">Cette identité est connue en tant que principal de service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-106">This identity is known as a service principal.</span></span> <span data-ttu-id="d0f3c-107">Cette approche vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-107">This approach enables you to:</span></span>

* <span data-ttu-id="d0f3c-108">Affecter à l’identité de l’application des autorisations différentes de vos propres autorisations.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="d0f3c-109">En règle générale, ces autorisations sont strictement limitées à ce que l’application doit faire.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="d0f3c-110">Utiliser un certificat pour l’authentification lors de l’exécution d’un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="d0f3c-111">Cet article explique comment utiliser [Azure CLI 1.0](../cli-install-nodejs.md) pour configurer une application qui s’exécute sous ses propres informations d’identification et sous sa propre identité.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="d0f3c-112">Installez la dernière version d’[Azure CLI 1.0](../cli-install-nodejs.md) pour vous assurer que votre environnement correspond aux exemples utilisés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="d0f3c-113">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="d0f3c-113">Required permissions</span></span>
<span data-ttu-id="d0f3c-114">Pour effectuer cette rubrique, vous devez disposer des autorisations suffisantes dans votre annuaire Azure Active Directory et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="d0f3c-115">Plus précisément, vous devez être en mesure de créer une application dans l’annuaire Azure Active Directory et d’affecter un rôle au principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="d0f3c-116">Le moyen le plus simple pour vérifier que votre compte dispose des autorisations adéquates est d’utiliser le portail.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="d0f3c-117">Consultez [Vérifier l’autorisation requise dans le portail](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="d0f3c-118">Passez maintenant à la section appropriée pour vous authentifier à l’aide d’un [mot de passe](#create-service-principal-with-password) ou d’un [certificat](#create-service-principal-with-certificate).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="d0f3c-119">Créer un principal du service avec un mot de passe</span><span class="sxs-lookup"><span data-stu-id="d0f3c-119">Create service principal with password</span></span>
<span data-ttu-id="d0f3c-120">Dans cette section, vous allez suivre la procédure qui vous permettra de créer l’application AD à l’aide d’un mot de passe et d’affecter le rôle Lecteur au principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="d0f3c-121">Connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="d0f3c-122">Pour créer une identité d’application, fournissez le nom de l’application et un mot de passe, comme dans la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="d0f3c-123">Le nouveau principal du service est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-123">The new service principal is returned.</span></span> <span data-ttu-id="d0f3c-124">L’ID d’objet est nécessaire lorsque vous accordez des autorisations.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="d0f3c-125">Le GUID répertorié avec les noms de principal du service est nécessaire lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="d0f3c-126">Ce guid est la même valeur que l’id de l’application.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="d0f3c-127">Dans les exemples d’applications, cette valeur est désignée sous le nom `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="d0f3c-128">Accordez des autorisations sur votre abonnement au principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="d0f3c-129">Dans cet exemple, vous ajoutez le principal du service au rôle Lecteur, ce qui l’autorise à lire toutes les ressources de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="d0f3c-130">Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="d0f3c-131">Pour le paramètre objectid, fournissez l’ID objet que vous avez utilisé lors de la création de l’application.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="d0f3c-132">Avant d’exécuter cette commande, vous devez donner le temps au nouveau principal du service de se propager dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d0f3c-133">Lorsque vous exécutez ces commandes manuellement, en général il s’est écoulé suffisamment de temps entre les tâches.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="d0f3c-134">Dans un script, vous devez ajouter une étape de veille entre les commandes (telle que `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="d0f3c-135">Si une erreur s’affiche indiquant que le principal n’existe pas dans le répertoire, réexécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="d0f3c-136">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="d0f3c-136">That's it!</span></span> <span data-ttu-id="d0f3c-137">Votre application Active Directory et votre principal du service sont maintenant configurés.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="d0f3c-138">La section suivante vous montre comment vous connecter avec les informations d’identification via Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="d0f3c-139">Si vous souhaitez utiliser les informations d’identification dans votre application de code, vous pouvez ignorer cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="d0f3c-140">Vous pouvez passer directement aux [exemples d’applications](#sample-applications) pour obtenir des exemples de connexion à l’aide d’un ID d’application et d’un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="d0f3c-141">Fournir des informations d’identification via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d0f3c-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="d0f3c-142">Maintenant, vous devez vous connecter en tant qu’application pour effectuer des opérations.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="d0f3c-143">Chaque fois que vous vous connectez en tant que principal de service, vous devez fournir l’ID de locataire du répertoire de votre application AD.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="d0f3c-144">Un locataire est une instance d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="d0f3c-145">Pour récupérer l’ID de locataire pour l’abonnement actuellement authentifié, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="d0f3c-146">Résultat :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="d0f3c-147">Si vous avez besoin d’obtenir l’ID de locataire d’un autre abonnement, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="d0f3c-148">Si vous avez besoin de récupérer l’id de client à utiliser pour la connexion, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="d0f3c-149">La valeur à utiliser pour la connexion est le guid répertorié dans les noms de principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="d0f3c-150">Connectez-vous en tant que principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="d0f3c-151">Vous êtes invité à entrer le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-151">You are prompted for the password.</span></span> <span data-ttu-id="d0f3c-152">Entrez le mot de passe que vous avez indiqué lors de la création de l’application AD.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="d0f3c-153">Vous êtes maintenant authentifié en tant que principal du service pour le principal du service que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="d0f3c-154">Vous pouvez également appeler des opérations REST à partir de la ligne de commande pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="d0f3c-155">Dans la réponse d’authentification, vous pouvez récupérer le jeton d’accès en vue de l’utiliser avec d’autres opérations.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="d0f3c-156">Pour un exemple de récupération du jeton d’accès en appelant des opérations REST, consultez [Génération d’un jeton d’accès](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="d0f3c-157">Créer un principal du service avec un certificat</span><span class="sxs-lookup"><span data-stu-id="d0f3c-157">Create service principal with certificate</span></span>
<span data-ttu-id="d0f3c-158">Cette section explique comment :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="d0f3c-159">créer un certificat auto-signé ;</span><span class="sxs-lookup"><span data-stu-id="d0f3c-159">create a self-signed certificate</span></span>
* <span data-ttu-id="d0f3c-160">créer l’application Active Directory avec le certificat, ainsi que le principal du service ;</span><span class="sxs-lookup"><span data-stu-id="d0f3c-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="d0f3c-161">affecter le rôle Lecteur au principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="d0f3c-162">Pour ce faire, [OpenSSL](http://www.openssl.org/) doit être installé.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="d0f3c-163">Vous pouvez créer un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="d0f3c-164">L’étape précédente a permis de créer deux fichiers : privkey.pem et cert.pem.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="d0f3c-165">Combinez les clés publique et privée dans un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="d0f3c-166">Ouvrez le fichier **examplecert.pem** et recherchez la longue séquence de caractères entre **-----BEGIN CERTIFICATE-----** et **-----END CERTIFICATE-----**.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="d0f3c-167">Copiez les données du certificat.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-167">Copy the certificate data.</span></span> <span data-ttu-id="d0f3c-168">Vous transmettrez ces données en tant que paramètre lors de la création du principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="d0f3c-169">Connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="d0f3c-170">Pour créer le principal de service, fournissez le nom de l’application et les données de certificat, comme indiqué dans la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="d0f3c-171">Le nouveau principal du service est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-171">The new service principal is returned.</span></span> <span data-ttu-id="d0f3c-172">L’ID d’objet est nécessaire lorsque vous accordez des autorisations.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="d0f3c-173">Le GUID répertorié avec les noms de principal du service est nécessaire lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="d0f3c-174">Ce guid est la même valeur que l’id de l’application.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="d0f3c-175">Dans les exemples d’applications, cette valeur est appelée ID client.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="d0f3c-176">Accordez des autorisations sur votre abonnement au principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="d0f3c-177">Dans cet exemple, vous ajoutez le principal du service au rôle Lecteur, ce qui l’autorise à lire toutes les ressources de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="d0f3c-178">Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="d0f3c-179">Pour le paramètre objectid, fournissez l’ID objet que vous avez utilisé lors de la création de l’application.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="d0f3c-180">Avant d’exécuter cette commande, vous devez donner le temps au nouveau principal du service de se propager dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d0f3c-181">Lorsque vous exécutez ces commandes manuellement, en général il s’est écoulé suffisamment de temps entre les tâches.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="d0f3c-182">Dans un script, vous devez ajouter une étape de veille entre les commandes (telle que `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="d0f3c-183">Si une erreur s’affiche indiquant que le principal n’existe pas dans le répertoire, réexécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="d0f3c-184">Fournir un certificat via un script Azure CLI automatisé</span><span class="sxs-lookup"><span data-stu-id="d0f3c-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="d0f3c-185">Maintenant, vous devez vous connecter en tant qu’application pour effectuer des opérations.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="d0f3c-186">Chaque fois que vous vous connectez en tant que principal de service, vous devez fournir l’ID de locataire du répertoire de votre application AD.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="d0f3c-187">Un locataire est une instance d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="d0f3c-188">Pour récupérer l’ID de locataire pour l’abonnement actuellement authentifié, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="d0f3c-189">Résultat :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="d0f3c-190">Si vous avez besoin d’obtenir l’ID de locataire d’un autre abonnement, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="d0f3c-191">Pour récupérer l’empreinte de certificat et supprimer les caractères inutiles, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="d0f3c-192">Vous obtenez alors une valeur d’empreinte semblable à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="d0f3c-193">Si vous avez besoin de récupérer l’id de client à utiliser pour la connexion, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="d0f3c-194">La valeur à utiliser pour la connexion est le guid répertorié dans les noms de principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="d0f3c-195">Connectez-vous en tant que principal du service.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="d0f3c-196">Vous êtes maintenant authentifié en tant que principal du service pour l’application Azure Active Directory que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="d0f3c-197">Modifier les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="d0f3c-197">Change credentials</span></span>

<span data-ttu-id="d0f3c-198">Pour modifier les informations d’identification pour une application Active Directory, en raison d’une faille de sécurité ou de l’expiration des informations d’identification, utilisez `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="d0f3c-199">Pour modifier un mot de passe, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="d0f3c-200">Pour modifier une valeur de certificat, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="d0f3c-201">Déboguer</span><span class="sxs-lookup"><span data-stu-id="d0f3c-201">Debug</span></span>

<span data-ttu-id="d0f3c-202">Lors de la création d’un principal de service, vous pouvez rencontrer les erreurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="d0f3c-203">**« Authentication_Unauthorized »** ou **« Aucun abonnement trouvé dans le contexte. »**</span><span class="sxs-lookup"><span data-stu-id="d0f3c-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="d0f3c-204">- Vous voyez cette erreur lorsque votre compte ne possède pas les [autorisations requises](#required-permissions) sur Azure Active Directory pour inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="d0f3c-205">En règle générale, vous obtenez cette erreur lorsque seuls des utilisateurs administrateurs dans votre annuaire Azure Active Directory peuvent inscrire des applications et que votre compte n’est pas un compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="d0f3c-206">Demandez à votre administrateur de vous affecter à un rôle d’administrateur ou d’autoriser les utilisateurs ordinaires à inscrire des applications.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="d0f3c-207">Le message indique que votre compte **« n’est pas autorisé à effectuer l’action ’Microsoft.Authorization/roleAssignments/write’ sur l’étendue ’/subscriptions/{guid}’ »** - Vous voyez cette erreur lorsque votre compte ne dispose pas d’autorisations suffisantes pour affecter un rôle à une identité.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="d0f3c-208">Demandez à votre administrateur d’abonnement de vous ajouter au rôle Administrateur de l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d0f3c-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="d0f3c-209">Exemples d'applications</span><span class="sxs-lookup"><span data-stu-id="d0f3c-209">Sample applications</span></span>
<span data-ttu-id="d0f3c-210">Pour plus d’informations sur la connexion en tant qu’application via différentes plateformes, voir :</span><span class="sxs-lookup"><span data-stu-id="d0f3c-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="d0f3c-211">.NET</span><span class="sxs-lookup"><span data-stu-id="d0f3c-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="d0f3c-212">Java</span><span class="sxs-lookup"><span data-stu-id="d0f3c-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="d0f3c-213">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d0f3c-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="d0f3c-214">Python</span><span class="sxs-lookup"><span data-stu-id="d0f3c-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="d0f3c-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="d0f3c-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="d0f3c-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0f3c-216">Next steps</span></span>
* <span data-ttu-id="d0f3c-217">Pour obtenir des instructions détaillées sur l’intégration d’une application à Azure pour la gestion des ressources, consultez [Guide du développeur pour l’authentification avec l’API Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="d0f3c-218">Pour obtenir des informations supplémentaires sur l’utilisation de certificats et d’Azure CLI, voir [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx)(Authentification par certificat à l’aide de principaux du service Azure à partir de la ligne de commande Linux).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="d0f3c-219">Pour une liste des actions disponibles qui peuvent être accordées ou refusées aux utilisateurs, consultez [Opérations du fournisseur de ressources Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d0f3c-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
