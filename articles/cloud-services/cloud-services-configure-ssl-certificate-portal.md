---
title: aaaConfigure SSL pour un service cloud | Documents Microsoft
description: "Découvrez comment toospecify un point de terminaison HTTPS pour un rôle web et comment tooupload une connexion SSL certificat toosecure de votre application. Ces exemples utilisent hello portail Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="40bc5-104">Configuration de SSL pour une application dans Azure</span><span class="sxs-lookup"><span data-stu-id="40bc5-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40bc5-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="40bc5-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="40bc5-106">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="40bc5-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="40bc5-107">Le chiffrement Secure Socket Layer (SSL) est la méthode hello couramment utilisé de la sécurisation des données envoyées sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="40bc5-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="40bc5-108">Cette tâche courante explique comment toospecify un point de terminaison HTTPS pour un rôle web et comment tooupload une connexion SSL certificat toosecure de votre application.</span><span class="sxs-lookup"><span data-stu-id="40bc5-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="40bc5-109">les procédures de Hello dans cette tâche s’appliquent les Services de cloud computing tooAzure ; pour les Services d’application, consultez [cela](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="40bc5-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="40bc5-110">Cette tâche utilise un déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="40bc5-110">This task uses a production deployment.</span></span> <span data-ttu-id="40bc5-111">Vous trouverez des informations sur l’utilisation d’un déploiement intermédiaire à fin hello de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="40bc5-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="40bc5-112">Lisez tout d’abord [ceci](cloud-services-how-to-create-deploy-portal.md) si vous n’avez pas encore créé de service cloud.</span><span class="sxs-lookup"><span data-stu-id="40bc5-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="40bc5-113">Étape 1 : obtention d’un certificat SSL</span><span class="sxs-lookup"><span data-stu-id="40bc5-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="40bc5-114">tooconfigure SSL pour une application, vous devez tout d’abord tooget un certificat SSL qui a été signé par un certificat autorité (CA), un tiers de confiance qui émet des certificats à cet effet.</span><span class="sxs-lookup"><span data-stu-id="40bc5-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="40bc5-115">Si vous n’en avez pas déjà, vous devez tooobtain une à partir d’une société qui vend des certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="40bc5-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="40bc5-116">certificat de Hello doit respecter hello suivant les exigences pour les certificats SSL dans Azure :</span><span class="sxs-lookup"><span data-stu-id="40bc5-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="40bc5-117">certificat de Hello doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="40bc5-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="40bc5-118">certificat de Hello doit être créé pour l’échange de clés, exportable tooa fichier d’échange d’informations personnelles (.pfx).</span><span class="sxs-lookup"><span data-stu-id="40bc5-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="40bc5-119">Hello nom du sujet du certificat doit correspondre au service de cloud hello domaine utilisé tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="40bc5-120">Impossible d’obtenir un certificat SSL à partir d’une autorité de certification (CA) pour le domaine cloudapp.net de hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="40bc5-121">Vous devez vous procurer un toouse de nom de domaine personnalisé lorsque accéder à votre service.</span><span class="sxs-lookup"><span data-stu-id="40bc5-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="40bc5-122">Lorsque vous demandez un certificat à partir d’une autorité de certification, nom du sujet du certificat hello doit correspondre à hello domaine personnalisé nom utilisé tooaccess votre application.</span><span class="sxs-lookup"><span data-stu-id="40bc5-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="40bc5-123">Par exemple, si votre nom de domaine personnalisé est **contoso.com**, vous demandez un certificat auprès de votre autorité de certification pour **.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="40bc5-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="40bc5-124">certificat de Hello doit utiliser un minimum de chiffrement de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="40bc5-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="40bc5-125">Dans le cadre d’un test, vous pouvez [créer](cloud-services-certs-create.md) et utiliser un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="40bc5-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="40bc5-126">Un certificat auto-signé n’est pas authentifié par une autorité de certification et pouvez utiliser le domaine cloudapp.net de hello en tant qu’URL du site Web hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="40bc5-127">Par exemple, hello tâche suivante utilise un certificat auto-signé qui Bonjour nom commun (CN) utilisé dans le certificat de hello est **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="40bc5-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="40bc5-128">Ensuite, vous devez inclure plus d’informations sur les certificats hello dans votre définition de service et les fichiers de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="40bc5-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="40bc5-129"><a name="modify"></a></span><span class="sxs-lookup"><span data-stu-id="40bc5-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="40bc5-130">Étape 2 : Modifier les fichiers de définition et de configuration de service hello</span><span class="sxs-lookup"><span data-stu-id="40bc5-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="40bc5-131">Votre application doit être configuré toouse hello et un point de terminaison HTTPS doit être ajouté.</span><span class="sxs-lookup"><span data-stu-id="40bc5-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="40bc5-132">Par conséquent, hello définition de service et les fichiers de configuration de service doivent toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="40bc5-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="40bc5-133">Dans votre environnement de développement, ouvrez le fichier de définition de service (CSDEF) hello, ajoutez un **certificats** section hello **WebRole** section et inclure hello informations suivantes le certificat (et les certificats intermédiaires) :</span><span class="sxs-lookup"><span data-stu-id="40bc5-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

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

   <span data-ttu-id="40bc5-134">Hello **certificats** section définit le nom hello de notre certificat, son emplacement et le nom de hello du magasin hello où il se trouve.</span><span class="sxs-lookup"><span data-stu-id="40bc5-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="40bc5-135">Autorisations (`permisionLevel` attribut) peut être tooone de jeu de hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="40bc5-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="40bc5-136">Valeur de l’autorisation</span><span class="sxs-lookup"><span data-stu-id="40bc5-136">Permission Value</span></span> | <span data-ttu-id="40bc5-137">Description</span><span class="sxs-lookup"><span data-stu-id="40bc5-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="40bc5-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="40bc5-138">limitedOrElevated</span></span> |<span data-ttu-id="40bc5-139">**(Par défaut)**  Tous les processus de rôle peuvent accéder à clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="40bc5-140">elevated</span><span class="sxs-lookup"><span data-stu-id="40bc5-140">elevated</span></span> |<span data-ttu-id="40bc5-141">Seuls les processus élevés peuvent accéder à clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="40bc5-142">Dans votre fichier de définition de service, ajoutez un **InputEndpoint** élément hello **points de terminaison** section tooenable HTTPS :</span><span class="sxs-lookup"><span data-stu-id="40bc5-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

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

3. <span data-ttu-id="40bc5-143">Dans votre fichier de définition de service, ajoutez un **liaison** élément hello **Sites** section.</span><span class="sxs-lookup"><span data-stu-id="40bc5-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="40bc5-144">Cet élément ajoute une toomap de liaison du site tooyour de point de terminaison HTTPS :</span><span class="sxs-lookup"><span data-stu-id="40bc5-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

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

   <span data-ttu-id="40bc5-145">Fichier de définition de tous les hello modifications requises toohello service ont été effectuées ; Toutefois, vous avez besoin d’informations de certificat de hello tooadd au fichier de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="40bc5-146">Dans votre fichier de configuration de service (CSCFG), ServiceConfiguration.Cloud.cscfg, ajoutez la valeur de votre certificat dans **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="40bc5-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="40bc5-147">Hello exemple de code suivant fournit des détails de hello **certificats** section, à l’exception de valeur d’empreinte numérique hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

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

<span data-ttu-id="40bc5-148">(Cet exemple utilise **sha1** pour l’algorithme d’empreinte numérique hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="40bc5-149">Spécifiez la valeur appropriée de hello pour l’algorithme d’empreinte numérique de votre certificat.)</span><span class="sxs-lookup"><span data-stu-id="40bc5-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="40bc5-150">Maintenant que les fichiers de configuration des service et de définition de hello service ont été mis à jour, votre déploiement pour le téléchargement tooAzure du package.</span><span class="sxs-lookup"><span data-stu-id="40bc5-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="40bc5-151">Si vous utilisez **cspack**, n’utilisez pas l’indicateur **/generateConfigurationFile**, car les informations de certificat que vous venez juste d’entrer seraient écrasées.</span><span class="sxs-lookup"><span data-stu-id="40bc5-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="40bc5-152">Étape 3 : chargement d’un certificat</span><span class="sxs-lookup"><span data-stu-id="40bc5-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="40bc5-153">Se connecter toohello portail Azure et...</span><span class="sxs-lookup"><span data-stu-id="40bc5-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="40bc5-154">Bonjour **toutes les ressources** section Hello portail, sélectionnez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="40bc5-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![Publier votre service cloud](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="40bc5-156">Cliquez sur **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="40bc5-156">Click **Certificates**.</span></span>

    ![Cliquez sur icône de certificats hello](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="40bc5-158">Cliquez sur **télécharger** haut hello de zone de certificats hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Cliquez sur l’élément de menu hello téléchargement](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="40bc5-160">Fournir hello **fichier**, **mot de passe**, puis cliquez sur **télécharger** bas hello de zone d’entrée de données hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="40bc5-161">Étape 4 : Connecter l’instance de rôle toohello à l’aide de HTTPS</span><span class="sxs-lookup"><span data-stu-id="40bc5-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="40bc5-162">Maintenant que votre déploiement est en cours d’exécution dans Azure, vous pouvez vous connecter tooit à l’aide de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="40bc5-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="40bc5-163">Cliquez sur hello **URL du Site** tooopen navigateur web de hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Cliquez sur hello URL du Site](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="40bc5-165">Dans votre navigateur web, modifiez hello lien toouse **https** au lieu de **http**, puis consultez la page de hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="40bc5-166">Si vous utilisez un certificat auto-signé, lorsque vous parcourez tooan point de terminaison HTTPS a associé à un certificat auto-signé de hello, vous voyez une erreur de certificat dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="40bc5-167">À l’aide d’un certificat signé par une autorité de certification approuvée élimine le problème ; Bonjour attendant, vous pouvez ignorer les erreurs hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="40bc5-168">(Une autre option consiste à magasin Autorités de certification approuvée de certificat d’utilisateur toohello tooadd hello certificat auto-signé.)</span><span class="sxs-lookup"><span data-stu-id="40bc5-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Aperçu du site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="40bc5-170">Si vous souhaitez toouse SSL pour un déploiement intermédiaire au lieu d’un déploiement de production, vous devez tout d’abord les URL de hello toodetermine utilisée pour le déploiement intermédiaire de hello.</span><span class="sxs-lookup"><span data-stu-id="40bc5-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="40bc5-171">Une fois que votre service cloud a été déployé, toohello d’URL hello environnement intermédiaire est déterminée par hello **ID de déploiement** GUID au format suivant :`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="40bc5-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="40bc5-172">Créez un certificat avec hello courantes URL basée sur le GUID de nom (CN) égal toohello (par exemple, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="40bc5-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="40bc5-173">Utilisez hello tooadd portail hello certificat tooyour mises en lots de service cloud.</span><span class="sxs-lookup"><span data-stu-id="40bc5-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="40bc5-174">Ensuite, ajoutez hello informations tooyour CSDEF et CSCFG fichiers de certificat, réorganiser votre application et mettre à jour votre déploiement intermédiaire toouse hello nouveau package.</span><span class="sxs-lookup"><span data-stu-id="40bc5-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="40bc5-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40bc5-175">Next steps</span></span>
* <span data-ttu-id="40bc5-176">[Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40bc5-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="40bc5-177">Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40bc5-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="40bc5-178">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40bc5-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="40bc5-179">[Gérez votre service cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40bc5-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
