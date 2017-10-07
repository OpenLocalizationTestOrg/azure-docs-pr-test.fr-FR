---
title: "identité aaaCreate pour une application Azure avec Azure CLI | Documents Microsoft"
description: "Décrit comment contrôlent les toouse CLI d’Azure toocreate une application Azure Active Directory et principal du service et accordez il accéder tooresources via l’accès en fonction du rôle. Il montre comment application tooauthenticate avec un mot de passe ou un certificat."
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
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="9381f-104">Utilisez Azure CLI toocreate une ressources tooaccess principal du service</span><span class="sxs-lookup"><span data-stu-id="9381f-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="9381f-105">Lorsque vous avez une application ou un script nécessitant des ressources de tooaccess, vous pouvez configurer une identité pour l’application hello et authentifier l’application hello avec ses propres informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9381f-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="9381f-106">Cette identité est connue en tant que principal de service.</span><span class="sxs-lookup"><span data-stu-id="9381f-106">This identity is known as a service principal.</span></span> <span data-ttu-id="9381f-107">Cette approche vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9381f-107">This approach enables you to:</span></span>

* <span data-ttu-id="9381f-108">Affecter des autorisations identité d’application toohello différents de vos propres autorisations.</span><span class="sxs-lookup"><span data-stu-id="9381f-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="9381f-109">En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.</span><span class="sxs-lookup"><span data-stu-id="9381f-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="9381f-110">Utilisez un certificat pour l’authentification lors de l’exécution d’un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="9381f-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="9381f-111">Cet article vous montre comment toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset d’un toorun application sous ses propres informations d’identification et l’identité.</span><span class="sxs-lookup"><span data-stu-id="9381f-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="9381f-112">Installer la version la plus récente de hello [Azure CLI 1.0](../cli-install-nodejs.md) toomake que votre environnement correspond aux exemples hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="9381f-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="9381f-113">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="9381f-113">Required permissions</span></span>
<span data-ttu-id="9381f-114">toocomplete cette rubrique, vous devez disposer des autorisations suffisantes dans Azure Active Directory et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9381f-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="9381f-115">Plus précisément, vous devez être en mesure de toocreate une application Bonjour Azure Active Directory et affecter des rôle tooa principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="9381f-116">Hello toocheck de façon plus simple si votre compte dispose des autorisations adéquates est via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="9381f-117">Consultez [Vérifier l’autorisation requise dans le portail](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="9381f-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="9381f-118">Maintenant, soit poursuivre tooa section [mot de passe](#create-service-principal-with-password) ou [certificat](#create-service-principal-with-certificate) l’authentification.</span><span class="sxs-lookup"><span data-stu-id="9381f-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="9381f-119">Créer un principal du service avec un mot de passe</span><span class="sxs-lookup"><span data-stu-id="9381f-119">Create service principal with password</span></span>
<span data-ttu-id="9381f-120">Dans cette section, vous effectuez hello étapes toocreate hello application AD avec un mot de passe et assigner de principal du service toohello hello lecture du rôle.</span><span class="sxs-lookup"><span data-stu-id="9381f-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="9381f-121">Tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="9381f-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="9381f-122">toocreate une identité de l’application, fournir nom hello de l’application hello et un mot de passe, comme indiqué dans hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9381f-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="9381f-123">nouveau service Hello principal est retourné.</span><span class="sxs-lookup"><span data-stu-id="9381f-123">hello new service principal is returned.</span></span> <span data-ttu-id="9381f-124">Hello, Id d’objet est nécessaire lors de l’octroi d’autorisations.</span><span class="sxs-lookup"><span data-stu-id="9381f-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="9381f-125">guid Hello répertorié par hello noms principaux de Service est nécessaire lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="9381f-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="9381f-126">Ce guid est hello même valeur que l’id de l’application hello. Dans les exemples d’applications hello, cette valeur est désignée tooas hello `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="9381f-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
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

3. <span data-ttu-id="9381f-127">Accorder des autorisations de principal de service hello sur votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9381f-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="9381f-128">Dans cet exemple, vous ajoutez hello service principal toohello rôle Lecteur, qui accorde l’autorisation tooread toutes les ressources dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="9381f-129">Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9381f-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="9381f-130">Pour le paramètre objectid de hello, fournir hello Id d’objet que vous avez utilisé lors de la création d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="9381f-131">Avant d’exécuter cette commande, vous devez laissez-lui du temps hello de nouveau service principal toopropagate dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9381f-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="9381f-132">Lorsque vous exécutez ces commandes manuellement, en général il s’est écoulé suffisamment de temps entre les tâches.</span><span class="sxs-lookup"><span data-stu-id="9381f-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="9381f-133">Dans un script, vous devez ajouter un toosleep étape entre commandes hello (comme `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="9381f-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="9381f-134">Si vous voyez qu'un hello indiquant erreur principal n’existe pas dans le répertoire de hello, réexécutez la commande hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="9381f-135">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="9381f-135">That's it!</span></span> <span data-ttu-id="9381f-136">Votre application Active Directory et votre principal du service sont maintenant configurés.</span><span class="sxs-lookup"><span data-stu-id="9381f-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="9381f-137">section suivante de Hello vous montre comment toolog avec hello des informations d’identification via l’interface CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9381f-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="9381f-138">Si vous souhaitez que les informations d’identification de toouse hello dans votre application de code, il est inutile toocontinue avec cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="9381f-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="9381f-139">Vous pouvez également accéder directement toohello [exemples d’applications](#sample-applications) pour obtenir des exemples de connexion avec votre id d’application et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9381f-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="9381f-140">Fournir des informations d’identification via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9381f-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="9381f-141">Maintenant, vous devez toolog dans en tant qu’opérations de tooperform application hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="9381f-142">Chaque fois que vous êtes connecté en tant que service principal, vous avez besoin d’id de client hello tooprovide du répertoire de hello pour votre application AD.</span><span class="sxs-lookup"><span data-stu-id="9381f-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="9381f-143">Un locataire est une instance d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9381f-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="9381f-144">id de client tooretrieve hello pour votre abonnement actuellement authentifié, utilisez :</span><span class="sxs-lookup"><span data-stu-id="9381f-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="9381f-145">Résultat :</span><span class="sxs-lookup"><span data-stu-id="9381f-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="9381f-146">Si vous avez besoin d’id de client hello tooget d’un autre abonnement, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9381f-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="9381f-147">Si vous devez tooretrieve hello client id toouse pour la connexion, utilisez :</span><span class="sxs-lookup"><span data-stu-id="9381f-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="9381f-148">toouse de valeur Hello pour la connexion est un guid hello répertoriée dans les noms principaux de service hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
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
3. <span data-ttu-id="9381f-149">Ouvrez une session en tant que principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="9381f-150">Vous êtes invité au mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-150">You are prompted for hello password.</span></span> <span data-ttu-id="9381f-151">Fournissent un mot de passe hello spécifié lors de la création d’application hello AD.</span><span class="sxs-lookup"><span data-stu-id="9381f-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="9381f-152">Vous êtes désormais authentifié en tant que principal du service hello de principal du service hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="9381f-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="9381f-153">Ou bien, vous pouvez appeler des opérations REST à partir de toolog de ligne de commande hello dans.</span><span class="sxs-lookup"><span data-stu-id="9381f-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="9381f-154">À partir de la réponse d’authentification hello, vous pouvez récupérer le jeton d’accès hello pour une utilisation avec d’autres opérations.</span><span class="sxs-lookup"><span data-stu-id="9381f-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="9381f-155">Pour obtenir un exemple de la récupération du jeton d’accès hello en appelant les opérations REST, consultez [générer un jeton d’accès](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="9381f-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="9381f-156">Créer un principal du service avec un certificat</span><span class="sxs-lookup"><span data-stu-id="9381f-156">Create service principal with certificate</span></span>
<span data-ttu-id="9381f-157">Dans cette section, vous les étapes hello pour :</span><span class="sxs-lookup"><span data-stu-id="9381f-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="9381f-158">créer un certificat auto-signé ;</span><span class="sxs-lookup"><span data-stu-id="9381f-158">create a self-signed certificate</span></span>
* <span data-ttu-id="9381f-159">créer hello application AD avec hello et de certificat principal de service hello</span><span class="sxs-lookup"><span data-stu-id="9381f-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="9381f-160">affecter le principal du service toohello hello lecture du rôle</span><span class="sxs-lookup"><span data-stu-id="9381f-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="9381f-161">toocomplete ces étapes, vous devez avoir [OpenSSL](http://www.openssl.org/) installé.</span><span class="sxs-lookup"><span data-stu-id="9381f-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="9381f-162">Vous pouvez créer un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="9381f-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="9381f-163">Hello précédant étape créé deux fichiers - privkey.pem et cert.pem.</span><span class="sxs-lookup"><span data-stu-id="9381f-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="9381f-164">Combiner les clés publiques et privées hello dans un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="9381f-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="9381f-165">Ouvrez hello **examplecert.pem** de fichiers et recherchez hello longue séquence de caractères entre **---BEGIN CERTIFICATE---** et **---END CERTIFICATE---**.</span><span class="sxs-lookup"><span data-stu-id="9381f-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="9381f-166">Copiez les données de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-166">Copy hello certificate data.</span></span> <span data-ttu-id="9381f-167">Vous passez ces données en tant que paramètre lors de la création de hello principal du service.</span><span class="sxs-lookup"><span data-stu-id="9381f-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="9381f-168">Tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="9381f-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="9381f-169">principal du service toocreate hello, fournir nom hello de l’application hello et les données de certificat hello, comme indiqué dans hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9381f-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="9381f-170">nouveau service Hello principal est retourné.</span><span class="sxs-lookup"><span data-stu-id="9381f-170">hello new service principal is returned.</span></span> <span data-ttu-id="9381f-171">Hello, Id d’objet est nécessaire lors de l’octroi d’autorisations.</span><span class="sxs-lookup"><span data-stu-id="9381f-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="9381f-172">guid Hello répertorié par hello noms principaux de Service est nécessaire lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="9381f-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="9381f-173">Ce guid est hello même valeur que l’id de l’application hello. Dans les exemples d’applications hello, cette valeur est désignée tooas hello ID Client.</span><span class="sxs-lookup"><span data-stu-id="9381f-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
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
6. <span data-ttu-id="9381f-174">Accorder des autorisations de principal de service hello sur votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9381f-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="9381f-175">Dans cet exemple, vous ajoutez hello service principal toohello rôle Lecteur, qui accorde l’autorisation tooread toutes les ressources dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="9381f-176">Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9381f-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="9381f-177">Pour le paramètre objectid de hello, fournir hello Id d’objet que vous avez utilisé lors de la création d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="9381f-178">Avant d’exécuter cette commande, vous devez laissez-lui du temps hello de nouveau service principal toopropagate dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9381f-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="9381f-179">Lorsque vous exécutez ces commandes manuellement, en général il s’est écoulé suffisamment de temps entre les tâches.</span><span class="sxs-lookup"><span data-stu-id="9381f-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="9381f-180">Dans un script, vous devez ajouter un toosleep étape entre commandes hello (comme `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="9381f-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="9381f-181">Si vous voyez qu'un hello indiquant erreur principal n’existe pas dans le répertoire de hello, réexécutez la commande hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="9381f-182">Fournir un certificat via un script Azure CLI automatisé</span><span class="sxs-lookup"><span data-stu-id="9381f-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="9381f-183">Maintenant, vous devez toolog dans en tant qu’opérations de tooperform application hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="9381f-184">Chaque fois que vous êtes connecté en tant que service principal, vous avez besoin d’id de client hello tooprovide du répertoire de hello pour votre application AD.</span><span class="sxs-lookup"><span data-stu-id="9381f-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="9381f-185">Un locataire est une instance d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9381f-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="9381f-186">id de client tooretrieve hello pour votre abonnement actuellement authentifié, utilisez :</span><span class="sxs-lookup"><span data-stu-id="9381f-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="9381f-187">Résultat :</span><span class="sxs-lookup"><span data-stu-id="9381f-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="9381f-188">Si vous avez besoin d’id de client hello tooget d’un autre abonnement, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9381f-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="9381f-189">tooretrieve hello empreinte numérique du certificat et supprimez les caractères inutiles, utilisez :</span><span class="sxs-lookup"><span data-stu-id="9381f-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="9381f-190">Vous obtenez alors une valeur d’empreinte semblable à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="9381f-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="9381f-191">Si vous devez tooretrieve hello client id toouse pour la connexion, utilisez :</span><span class="sxs-lookup"><span data-stu-id="9381f-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="9381f-192">toouse de valeur Hello pour la connexion est un guid hello répertoriée dans les noms principaux de service hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
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
4. <span data-ttu-id="9381f-193">Ouvrez une session en tant que principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="9381f-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="9381f-194">Vous êtes désormais authentifié en tant que principal de service hello pour hello application Azure Active Directory que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="9381f-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="9381f-195">Modifier les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="9381f-195">Change credentials</span></span>

<span data-ttu-id="9381f-196">informations d’identification de hello toochange pour une application AD, soit en raison d’une compromission de la sécurité ou une date d’expiration des informations d’identification, utilisent `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="9381f-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="9381f-197">toochange un mot de passe, utilisez :</span><span class="sxs-lookup"><span data-stu-id="9381f-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="9381f-198">toochange une valeur de certificat, utilisez :</span><span class="sxs-lookup"><span data-stu-id="9381f-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="9381f-199">Déboguer</span><span class="sxs-lookup"><span data-stu-id="9381f-199">Debug</span></span>

<span data-ttu-id="9381f-200">Vous pouvez rencontrer les erreurs suivantes lors de la création d’un principal de service de hello :</span><span class="sxs-lookup"><span data-stu-id="9381f-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="9381f-201">**« Authentication_Unauthorized »** ou **« aucun abonnement ne trouvé dans le contexte de hello. »**</span><span class="sxs-lookup"><span data-stu-id="9381f-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="9381f-202">-Vous recevez cette erreur lorsque votre compte ne dispose pas de hello [autorisations requises](#required-permissions) sur hello Azure Active Directory tooregister une application.</span><span class="sxs-lookup"><span data-stu-id="9381f-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="9381f-203">En règle générale, vous obtenez cette erreur lorsque seuls des utilisateurs administrateurs dans votre annuaire Azure Active Directory peuvent inscrire des applications et que votre compte n’est pas un compte d’administrateur. Demandez à votre tooeither administrateur affecter le rôle administrateur tooan ou tooenable utilisateurs tooregister applications.</span><span class="sxs-lookup"><span data-stu-id="9381f-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="9381f-204">Votre compte **« n’a pas action de tooperform d’autorisation 'Microsoft.Authorization/roleAssignments/write' sur l’étendue '/ subscriptions / {guid}'. »**  -Vous recevez cette erreur lorsque votre compte n’a pas suffisamment autorisations tooassign une identité tooan du rôle.</span><span class="sxs-lookup"><span data-stu-id="9381f-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="9381f-205">Demandez à votre tooadd d’administrateur abonnement rôle administrateur de l’accès tooUser.</span><span class="sxs-lookup"><span data-stu-id="9381f-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="9381f-206">Exemples d'applications</span><span class="sxs-lookup"><span data-stu-id="9381f-206">Sample applications</span></span>
<span data-ttu-id="9381f-207">Pour plus d’informations sur la connexion en tant qu’application hello via différentes plateformes, consultez :</span><span class="sxs-lookup"><span data-stu-id="9381f-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="9381f-208">.NET</span><span class="sxs-lookup"><span data-stu-id="9381f-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="9381f-209">Java</span><span class="sxs-lookup"><span data-stu-id="9381f-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="9381f-210">Node.JS</span><span class="sxs-lookup"><span data-stu-id="9381f-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="9381f-211">Python</span><span class="sxs-lookup"><span data-stu-id="9381f-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="9381f-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="9381f-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="9381f-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9381f-213">Next steps</span></span>
* <span data-ttu-id="9381f-214">Pour obtenir des instructions détaillées sur l’intégration d’une application dans Azure pour la gestion des ressources, consultez [tooauthorization du guide du développeur avec hello API Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9381f-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="9381f-215">tooget plus d’informations sur l’utilisation de certificats et CLI d’Azure, consultez [l’authentification basée sur le certificat avec les principaux du Service Azure à partir de la ligne de commande Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="9381f-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="9381f-216">Pour obtenir la liste des actions disponibles qui peuvent être accordées ou refusées toousers, consultez [opérations du fournisseur de ressources Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="9381f-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
