---
title: aaaConfigure SSL pour un service cloud (classiques) | Documents Microsoft
description: "Découvrez comment toospecify un point de terminaison HTTPS pour un rôle web et comment tooupload une connexion SSL certificat toosecure de votre application."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="5ea62-103">Configuration de SSL pour une application dans Azure</span><span class="sxs-lookup"><span data-stu-id="5ea62-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ea62-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="5ea62-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="5ea62-105">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="5ea62-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="5ea62-106">Le chiffrement Secure Socket Layer (SSL) est la méthode hello couramment utilisé de la sécurisation des données envoyées sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="5ea62-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="5ea62-107">Cette tâche courante explique comment toospecify un point de terminaison HTTPS pour un rôle web et comment tooupload une connexion SSL certificat toosecure de votre application.</span><span class="sxs-lookup"><span data-stu-id="5ea62-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="5ea62-108">les procédures de Hello dans cette tâche s’appliquent les Services de cloud computing tooAzure ; pour les Services d’application, consultez [cela](../app-service-web/web-sites-configure-ssl-certificate.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="5ea62-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="5ea62-109">Cette tâche utilise un déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="5ea62-109">This task uses a production deployment.</span></span> <span data-ttu-id="5ea62-110">Vous trouverez des informations sur l’utilisation d’un déploiement intermédiaire à fin hello de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="5ea62-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="5ea62-111">Lisez tout d’abord [cet](cloud-services-how-to-create-deploy.md) article si vous n’avez pas encore créé de service cloud.</span><span class="sxs-lookup"><span data-stu-id="5ea62-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="5ea62-112">Étape 1 : obtention d’un certificat SSL</span><span class="sxs-lookup"><span data-stu-id="5ea62-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="5ea62-113">tooconfigure SSL pour une application, vous devez tout d’abord tooget un certificat SSL qui a été signé par un certificat autorité (CA), un tiers de confiance qui émet des certificats à cet effet.</span><span class="sxs-lookup"><span data-stu-id="5ea62-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="5ea62-114">Si vous n’en avez pas déjà, vous devez tooobtain une à partir d’une société qui vend des certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="5ea62-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="5ea62-115">certificat de Hello doit respecter hello suivant les exigences pour les certificats SSL dans Azure :</span><span class="sxs-lookup"><span data-stu-id="5ea62-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="5ea62-116">certificat de Hello doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="5ea62-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="5ea62-117">certificat de Hello doit être créé pour l’échange de clés, exportable tooa fichier d’échange d’informations personnelles (.pfx).</span><span class="sxs-lookup"><span data-stu-id="5ea62-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="5ea62-118">Hello nom du sujet du certificat doit correspondre au service de cloud hello domaine utilisé tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="5ea62-119">Impossible d’obtenir un certificat SSL à partir d’une autorité de certification (CA) pour le domaine cloudapp.net de hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="5ea62-120">Vous devez vous procurer un toouse de nom de domaine personnalisé lorsque accéder à votre service.</span><span class="sxs-lookup"><span data-stu-id="5ea62-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="5ea62-121">Lorsque vous demandez un certificat à partir d’une autorité de certification, nom du sujet du certificat hello doit correspondre à hello domaine personnalisé nom utilisé tooaccess votre application.</span><span class="sxs-lookup"><span data-stu-id="5ea62-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="5ea62-122">Par exemple, si votre nom de domaine personnalisé est **contoso.com**, vous demandez un certificat auprès de votre autorité de certification pour **.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="5ea62-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="5ea62-123">certificat de Hello doit utiliser un minimum de chiffrement de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="5ea62-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="5ea62-124">Dans le cadre d’un test, vous pouvez [créer](cloud-services-certs-create.md) et utiliser un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="5ea62-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="5ea62-125">Un certificat auto-signé n’est pas authentifié par une autorité de certification et pouvez utiliser le domaine cloudapp.net de hello en tant qu’URL du site Web hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="5ea62-126">Par exemple, hello tâche suivante utilise un certificat auto-signé qui Bonjour nom commun (CN) utilisé dans le certificat de hello est **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="5ea62-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="5ea62-127">Ensuite, vous devez inclure plus d’informations sur les certificats hello dans votre définition de service et les fichiers de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="5ea62-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="5ea62-128">Étape 2 : Modifier les fichiers de définition et de configuration de service hello</span><span class="sxs-lookup"><span data-stu-id="5ea62-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="5ea62-129">Votre application doit être configuré toouse hello et un point de terminaison HTTPS doit être ajouté.</span><span class="sxs-lookup"><span data-stu-id="5ea62-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="5ea62-130">Par conséquent, hello définition de service et les fichiers de configuration de service doivent toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="5ea62-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="5ea62-131">Dans votre environnement de développement, ouvrez le fichier de définition de service (CSDEF) hello, ajoutez un **certificats** section hello **WebRole** section et inclure hello informations suivantes le certificat (et les certificats intermédiaires) :</span><span class="sxs-lookup"><span data-stu-id="5ea62-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="5ea62-132">Hello **certificats** section définit le nom hello de notre certificat, son emplacement et le nom de hello du magasin hello où il se trouve.</span><span class="sxs-lookup"><span data-stu-id="5ea62-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="5ea62-133">Autorisations (`permisionLevel` attribut) peut être tooone de jeu de hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5ea62-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="5ea62-134">Valeur de l’autorisation</span><span class="sxs-lookup"><span data-stu-id="5ea62-134">Permission Value</span></span> | <span data-ttu-id="5ea62-135">Description</span><span class="sxs-lookup"><span data-stu-id="5ea62-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="5ea62-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="5ea62-136">limitedOrElevated</span></span> |<span data-ttu-id="5ea62-137">**(Par défaut)**  Tous les processus de rôle peuvent accéder à clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="5ea62-138">elevated</span><span class="sxs-lookup"><span data-stu-id="5ea62-138">elevated</span></span> |<span data-ttu-id="5ea62-139">Seuls les processus élevés peuvent accéder à clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="5ea62-140">Dans votre fichier de définition de service, ajoutez un **InputEndpoint** élément hello **points de terminaison** section tooenable HTTPS :</span><span class="sxs-lookup"><span data-stu-id="5ea62-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443" 
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="5ea62-141">Dans votre fichier de définition de service, ajoutez un **liaison** élément hello **Sites** section.</span><span class="sxs-lookup"><span data-stu-id="5ea62-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="5ea62-142">Cette section permet d’ajouter un toomap de liaison du site tooyour de point de terminaison HTTPS :</span><span class="sxs-lookup"><span data-stu-id="5ea62-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
    ```xml   
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="5ea62-143">Tous les fichier de définition de service de toohello de modifications requises de hello ont été effectuées, mais vous devez toujours des informations de certificat hello tooadd au fichier de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="5ea62-144">Dans votre fichier de configuration service (CSCFG), ServiceConfiguration.Cloud.cscfg, ajoutez un **certificats** section hello **rôle** section, en remplaçant la valeur d’empreinte numérique exemple hello ci-dessous avec celui de votre certificat :</span><span class="sxs-lookup"><span data-stu-id="5ea62-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
    ```xml   
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff" 
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc" 
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="5ea62-145">(hello précédant l’exemple suivant utilise **sha1** pour l’algorithme d’empreinte numérique hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="5ea62-146">Spécifiez la valeur appropriée de hello pour l’algorithme d’empreinte numérique de votre certificat.)</span><span class="sxs-lookup"><span data-stu-id="5ea62-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="5ea62-147">Maintenant que les fichiers de configuration des service et de définition de hello service ont été mis à jour, votre déploiement pour le téléchargement tooAzure du package.</span><span class="sxs-lookup"><span data-stu-id="5ea62-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="5ea62-148">Si vous utilisez **cspack**, n’utilisez pas l’indicateur **/generateConfigurationFile**, car les informations de certificat que vous venez d’entrer seraient écrasées.</span><span class="sxs-lookup"><span data-stu-id="5ea62-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="5ea62-149">Étape 3 : chargement d’un certificat</span><span class="sxs-lookup"><span data-stu-id="5ea62-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="5ea62-150">Votre package de déploiement a été le certificat de hello toouse mis à jour, et un point de terminaison HTTPS a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="5ea62-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="5ea62-151">Vous pouvez maintenant télécharger tooAzure de package et de certificat hello avec hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="5ea62-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="5ea62-152">Connectez-vous à toohello [portail Azure classic][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="5ea62-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="5ea62-153">Cliquez sur **Services de cloud computing** sur le volet de navigation de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="5ea62-154">Cliquez sur le service de cloud computing hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="5ea62-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="5ea62-155">Cliquez sur hello **certificats** onglet.</span><span class="sxs-lookup"><span data-stu-id="5ea62-155">Click hello **Certificates** tab.</span></span>
   
    ![Cliquez sur onglet de certificats hello](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="5ea62-157">Cliquez sur hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="5ea62-157">Click hello **Upload** button.</span></span>
   
    ![Télécharger](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="5ea62-159">Fournir hello **fichier**, **mot de passe**, puis cliquez sur **Complete** (hello coche).</span><span class="sxs-lookup"><span data-stu-id="5ea62-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="5ea62-160">Étape 4 : Connecter l’instance de rôle toohello à l’aide de HTTPS</span><span class="sxs-lookup"><span data-stu-id="5ea62-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="5ea62-161">Maintenant que votre déploiement est en cours d’exécution dans Azure, vous pouvez vous connecter tooit à l’aide de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5ea62-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="5ea62-162">Dans hello portail Azure classic, sélectionnez votre déploiement, puis cliquez sur lien hello sous **URL du Site**.</span><span class="sxs-lookup"><span data-stu-id="5ea62-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![Déterminer l'URL du site][2]
2. <span data-ttu-id="5ea62-164">Dans votre navigateur web, modifiez hello lien toouse **https** au lieu de **http**, puis consultez la page de hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5ea62-165">Si vous utilisez un certificat auto-signé, lorsque vous parcourez tooan point de terminaison HTTPS a associé à un certificat auto-signé de hello, vous voyez une erreur de certificat dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="5ea62-166">À l’aide d’un certificat signé par une autorité de certification approuvée élimine le problème ; Bonjour attendant, vous pouvez ignorer les erreurs hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="5ea62-167">(Une autre option consiste à magasin Autorités de certification approuvée de certificat d’utilisateur toohello tooadd hello certificat auto-signé.)</span><span class="sxs-lookup"><span data-stu-id="5ea62-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Exemple de site Web SSL][3]

<span data-ttu-id="5ea62-169">Si vous souhaitez toouse SSL pour un déploiement intermédiaire au lieu d’un déploiement de production, vous devez d’abord les URL de hello toodetermine utilisée pour le déploiement intermédiaire de hello.</span><span class="sxs-lookup"><span data-stu-id="5ea62-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="5ea62-170">Déployez votre environnement intermédiaire de cloud service toohello sans inclure un certificat ou toutes les informations de certificat.</span><span class="sxs-lookup"><span data-stu-id="5ea62-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="5ea62-171">Une fois déployé, vous pouvez déterminer les URL de type GUID hello, qui est répertoriée dans hello portail Azure classic **URL du Site** champ.</span><span class="sxs-lookup"><span data-stu-id="5ea62-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="5ea62-172">Créez un certificat avec hello courantes URL basée sur le GUID de nom (CN) égal toohello (par exemple, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="5ea62-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="5ea62-173">Utilisez hello tooadd de portail classique Azure hello certificat tooyour mises en lots de service cloud.</span><span class="sxs-lookup"><span data-stu-id="5ea62-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="5ea62-174">Ensuite, ajoutez hello informations tooyour CSDEF et CSCFG fichiers de certificat, réorganiser votre application et mettre à jour votre déploiement intermédiaire toouse hello nouveau package.</span><span class="sxs-lookup"><span data-stu-id="5ea62-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ea62-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ea62-175">Next steps</span></span>
* <span data-ttu-id="5ea62-176">[Configuration générale de votre service cloud](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5ea62-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="5ea62-177">Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5ea62-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="5ea62-178">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="5ea62-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="5ea62-179">[Gérez votre service cloud](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="5ea62-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
