---
title: Configuration de SSL pour un service cloud (classique) | Microsoft Docs
description: "Découvrez comment spécifier un point de terminaison HTTPS pour un rôle web et télécharger un certificat SSL pour sécuriser votre application."
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
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="4ab66-103">Configuration de SSL pour une application dans Azure</span><span class="sxs-lookup"><span data-stu-id="4ab66-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ab66-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4ab66-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="4ab66-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="4ab66-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="4ab66-106">Le chiffrement SSL (Secure Socket Layer) est la méthode de sécurisation la plus couramment utilisée pour envoyer des données sécurisées sur Internet.</span><span class="sxs-lookup"><span data-stu-id="4ab66-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="4ab66-107">Cette tâche présente la spécification d'un point de terminaison HTTPS pour un rôle Web et le téléchargement d'un certificat SSL pour sécuriser votre application.</span><span class="sxs-lookup"><span data-stu-id="4ab66-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="4ab66-108">Les procédures décrites dans cette tâche s’appliquent à Azure Cloud Services ; pour App Services, consultez [cet](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span><span class="sxs-lookup"><span data-stu-id="4ab66-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="4ab66-109">Cette tâche utilise un déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="4ab66-109">This task uses a production deployment.</span></span> <span data-ttu-id="4ab66-110">Vous trouverez des informations sur l’utilisation d’un déploiement intermédiaire à la fin de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="4ab66-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="4ab66-111">Lisez tout d’abord [cet](cloud-services-how-to-create-deploy.md) article si vous n’avez pas encore créé de service cloud.</span><span class="sxs-lookup"><span data-stu-id="4ab66-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="4ab66-112">Étape 1 : obtention d’un certificat SSL</span><span class="sxs-lookup"><span data-stu-id="4ab66-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="4ab66-113">Pour configurer le chiffrement SSL pour une application, vous devez d’abord obtenir un certificat SSL signé par une autorité de certification, un tiers approuvé qui émet des certificats à cet effet.</span><span class="sxs-lookup"><span data-stu-id="4ab66-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="4ab66-114">Si vous n’en possédez pas, vous devez en obtenir un auprès de la société qui vend des certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="4ab66-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="4ab66-115">Le certificat SSL doit répondre aux prérequis suivants dans Azure :</span><span class="sxs-lookup"><span data-stu-id="4ab66-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="4ab66-116">Le certificat doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="4ab66-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="4ab66-117">Le certificat doit être créé pour l'échange de clés et pouvoir faire l'objet d'un export au format Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="4ab66-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="4ab66-118">Le nom d'objet du certificat doit correspondre au domaine servant à accéder au service cloud.</span><span class="sxs-lookup"><span data-stu-id="4ab66-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="4ab66-119">Vous ne pouvez pas obtenir de certificat SSL d'une autorité de certification pour le domaine cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="4ab66-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="4ab66-120">Vous devez acquérir un nom de domaine personnalisé à utiliser pour accéder à votre service.</span><span class="sxs-lookup"><span data-stu-id="4ab66-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="4ab66-121">Lorsque vous demandez un certificat auprès d’une autorité de certification, le nom d’objet du certificat doit correspondre au nom de domaine personnalisé que vous utilisez pour accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="4ab66-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="4ab66-122">Par exemple, si votre nom de domaine personnalisé est **contoso.com**, vous demandez un certificat auprès de votre autorité de certification pour **.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="4ab66-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="4ab66-123">Le certificat doit utiliser au minimum un chiffrement à 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="4ab66-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="4ab66-124">Dans le cadre d’un test, vous pouvez [créer](cloud-services-certs-create.md) et utiliser un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="4ab66-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="4ab66-125">Un certificat auto-signé n'est pas authentifié par une autorité de certification et peut utiliser le domaine cloudapp.net comme URL de site Web.</span><span class="sxs-lookup"><span data-stu-id="4ab66-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="4ab66-126">Par exemple, la tâche ci-dessous utilise un certificat auto-signé dans lequel le nom commun utilisé dans le certificat est **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="4ab66-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="4ab66-127">Ensuite, vous devez ajouter des informations sur le certificat dans votre définition de service et dans les fichiers de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="4ab66-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="4ab66-128">Étape 2 : modification des fichiers de définition de service et de configuration</span><span class="sxs-lookup"><span data-stu-id="4ab66-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="4ab66-129">Votre application doit être configurée pour utiliser le certificat, et un point de terminaison HTTPS doit être ajouté.</span><span class="sxs-lookup"><span data-stu-id="4ab66-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="4ab66-130">Suite à cette opération, les fichiers de définition de service et de configuration de service doivent être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="4ab66-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="4ab66-131">Dans votre environnement de développement, ouvrez le fichier de définition du service (CSDEF), ajoutez une section **Certificates** dans la section **WebRole**, puis ajoutez les informations qui suivent sur le certificat (et les certificats intermédiaires) :</span><span class="sxs-lookup"><span data-stu-id="4ab66-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="4ab66-132">La section **Certificates** définit le nom du certificat, son emplacement et le nom du magasin dans lequel il se trouve.</span><span class="sxs-lookup"><span data-stu-id="4ab66-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="4ab66-133">Les autorisations (attribut `permisionLevel`) peuvent être définies sur les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ab66-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="4ab66-134">Valeur de l’autorisation</span><span class="sxs-lookup"><span data-stu-id="4ab66-134">Permission Value</span></span> | <span data-ttu-id="4ab66-135">Description</span><span class="sxs-lookup"><span data-stu-id="4ab66-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="4ab66-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="4ab66-136">limitedOrElevated</span></span> |<span data-ttu-id="4ab66-137">**(Par défaut)** Tous les processus de rôle peuvent accéder à la clé privée.</span><span class="sxs-lookup"><span data-stu-id="4ab66-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="4ab66-138">elevated</span><span class="sxs-lookup"><span data-stu-id="4ab66-138">elevated</span></span> |<span data-ttu-id="4ab66-139">Seuls les processus élevés peuvent accéder à la clé privée.</span><span class="sxs-lookup"><span data-stu-id="4ab66-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="4ab66-140">Dans votre fichier de définition du service, ajoutez un élément **InputEndpoint** dans la section **Endpoints** pour activer HTTPS :</span><span class="sxs-lookup"><span data-stu-id="4ab66-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="4ab66-141">Dans votre fichier de définition du service, ajoutez un élément **Binding** dans la section **Sites**.</span><span class="sxs-lookup"><span data-stu-id="4ab66-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="4ab66-142">Cette section ajoute une liaison HTTPS pour mapper le point de terminaison à votre site :</span><span class="sxs-lookup"><span data-stu-id="4ab66-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="4ab66-143">Toutes les modifications nécessaires ont été apportées au fichier de définition de service, mais vous devez encore y ajouter les informations de certificat.</span><span class="sxs-lookup"><span data-stu-id="4ab66-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="4ab66-144">Dans votre fichier de configuration de service (CSCFG) ServiceConfiguration.Cloud.cscfg, ajoutez une section **Certificates** dans la section **Role** en remplaçant la valeur d’empreinte numérique ci-dessous par celle de votre certificat :</span><span class="sxs-lookup"><span data-stu-id="4ab66-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="4ab66-145">(L’exemple précédent utilise **sha1** comme algorithme d’empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="4ab66-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="4ab66-146">Spécifiez la valeur correspondant à l'algorithme d'empreinte numérique de votre certificat.)</span><span class="sxs-lookup"><span data-stu-id="4ab66-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="4ab66-147">Maintenant que les fichiers de définition du service et de configuration de service ont été mis à jour, créez un package pour votre déploiement afin de le télécharger dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab66-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="4ab66-148">Si vous utilisez **cspack**, n’utilisez pas l’indicateur **/generateConfigurationFile**, car les informations de certificat que vous venez d’entrer seraient écrasées.</span><span class="sxs-lookup"><span data-stu-id="4ab66-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="4ab66-149">Étape 3 : chargement d’un certificat</span><span class="sxs-lookup"><span data-stu-id="4ab66-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="4ab66-150">Votre package de déploiement a été mis à jour pour utiliser le certificat, et un point de terminaison HTTPS a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="4ab66-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="4ab66-151">Vous pouvez maintenant télécharger le certificat dans Azure via le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="4ab66-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="4ab66-152">Connectez-vous au [portail Azure Classic][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="4ab66-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="4ab66-153">Cliquez sur **Cloud Services** dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="4ab66-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="4ab66-154">Cliquez sur le service cloud de votre choix.</span><span class="sxs-lookup"><span data-stu-id="4ab66-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="4ab66-155">Cliquer sur l’onglet **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="4ab66-155">Click the **Certificates** tab.</span></span>
   
    ![Cliquer sur l’onglet Certificats](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="4ab66-157">Cliquez sur le bouton **Télécharger** .</span><span class="sxs-lookup"><span data-stu-id="4ab66-157">Click the **Upload** button.</span></span>
   
    ![Télécharger](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="4ab66-159">Fournissez le **Fichier**, le **Mot de passe**, puis cliquez sur **Terminé** (la coche).</span><span class="sxs-lookup"><span data-stu-id="4ab66-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="4ab66-160">Étape 4 : connexion à l’instance de rôle à l’aide de HTTPS</span><span class="sxs-lookup"><span data-stu-id="4ab66-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="4ab66-161">Maintenant que votre déploiement est opérationnel dans Azure, vous pouvez vous y connecter via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4ab66-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="4ab66-162">Dans le portail Azure Classic, sélectionnez le déploiement, puis cliquez sur le lien sous **Site URL**.</span><span class="sxs-lookup"><span data-stu-id="4ab66-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![Déterminer l'URL du site][2]
2. <span data-ttu-id="4ab66-164">Dans votre navigateur Web, modifiez le lien pour utiliser **HTTPS** au lieu de **HTTP**, puis accédez à la page.</span><span class="sxs-lookup"><span data-stu-id="4ab66-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4ab66-165">Si vous utilisez un certificat auto-signé, lorsque vous accédez à un point de terminaison HTTPS qui lui est associé, vous pourriez obtenir une erreur de certificat dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="4ab66-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="4ab66-166">Pour remédier à ce problème, utilisez un certificat signé par une autorité de certification approuvée. En attendant, vous pouvez ignorer cette erreur.</span><span class="sxs-lookup"><span data-stu-id="4ab66-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="4ab66-167">(Une autre possibilité est d'ajouter le certificat auto-signé au magasin de certificats d'autorité de certification approuvé de l'utilisateur.)</span><span class="sxs-lookup"><span data-stu-id="4ab66-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Exemple de site Web SSL][3]

<span data-ttu-id="4ab66-169">Si vous voulez utiliser SSL pour un déploiement intermédiaire au lieu d’un déploiement de production, vous devez d’abord déterminer l’URL utilisée pour le déploiement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="4ab66-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="4ab66-170">Déployez votre service cloud dans l'environnement intermédiaire sans inclure de certificat ou d'informations de certificat.</span><span class="sxs-lookup"><span data-stu-id="4ab66-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="4ab66-171">Une fois le déploiement effectué, vous pouvez déterminer l'URL basée sur le GUID, qui se trouve dans le champ **Site URL** du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="4ab66-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="4ab66-172">Créez un certificat avec le nom commun (CN) similaire à l’URL basée sur GUID (par exemple, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="4ab66-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="4ab66-173">Utilisez le portail Azure Classic pour ajouter le certificat à votre service cloud intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="4ab66-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="4ab66-174">Ensuite, ajoutez les informations du certificat à vos fichiers CSDEF et CSCFG, recréez le package de votre application et mettez à jour votre déploiement intermédiaire pour utiliser le nouveau package.</span><span class="sxs-lookup"><span data-stu-id="4ab66-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ab66-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ab66-175">Next steps</span></span>
* <span data-ttu-id="4ab66-176">[Configuration générale de votre service cloud](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4ab66-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="4ab66-177">Découvrez comment [déployer un service cloud](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4ab66-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="4ab66-178">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="4ab66-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="4ab66-179">[Gérez votre service cloud](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="4ab66-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
