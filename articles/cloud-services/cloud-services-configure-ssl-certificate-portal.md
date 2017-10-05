---
title: Configuration de SSL pour un service cloud | Microsoft Docs
description: "Découvrez comment spécifier un point de terminaison HTTPS pour un rôle web et télécharger un certificat SSL pour sécuriser votre application. Ces exemples utilisent le portail Azure."
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
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="8f40b-104">Configuration de SSL pour une application dans Azure</span><span class="sxs-lookup"><span data-stu-id="8f40b-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f40b-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8f40b-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="8f40b-106">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="8f40b-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="8f40b-107">Le chiffrement SSL (Secure Socket Layer) est la méthode de sécurisation la plus couramment utilisée pour envoyer des données sécurisées sur Internet.</span><span class="sxs-lookup"><span data-stu-id="8f40b-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="8f40b-108">Cette tâche présente la spécification d'un point de terminaison HTTPS pour un rôle Web et le téléchargement d'un certificat SSL pour sécuriser votre application.</span><span class="sxs-lookup"><span data-stu-id="8f40b-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="8f40b-109">Les procédures décrites dans cette tâche s’appliquent à Azure Cloud Services ; pour App Services, consultez [cette page](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="8f40b-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="8f40b-110">Cette tâche utilise un déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="8f40b-110">This task uses a production deployment.</span></span> <span data-ttu-id="8f40b-111">Vous trouverez des informations sur l’utilisation d’un déploiement intermédiaire à la fin de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="8f40b-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="8f40b-112">Lisez tout d’abord [ceci](cloud-services-how-to-create-deploy-portal.md) si vous n’avez pas encore créé de service cloud.</span><span class="sxs-lookup"><span data-stu-id="8f40b-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="8f40b-113">Étape 1 : obtention d’un certificat SSL</span><span class="sxs-lookup"><span data-stu-id="8f40b-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="8f40b-114">Pour configurer le chiffrement SSL pour une application, vous devez d’abord obtenir un certificat SSL signé par une autorité de certification, un tiers approuvé qui émet des certificats à cet effet.</span><span class="sxs-lookup"><span data-stu-id="8f40b-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="8f40b-115">Si vous n’en possédez pas, vous devez en obtenir un auprès de la société qui vend des certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="8f40b-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="8f40b-116">Le certificat SSL doit répondre aux prérequis suivants dans Azure :</span><span class="sxs-lookup"><span data-stu-id="8f40b-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="8f40b-117">Le certificat doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="8f40b-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="8f40b-118">Le certificat doit être créé pour l'échange de clés et pouvoir faire l'objet d'un export au format Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="8f40b-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="8f40b-119">Le nom d'objet du certificat doit correspondre au domaine servant à accéder au service cloud.</span><span class="sxs-lookup"><span data-stu-id="8f40b-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="8f40b-120">Vous ne pouvez pas obtenir de certificat SSL d'une autorité de certification pour le domaine cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="8f40b-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="8f40b-121">Vous devez acquérir un nom de domaine personnalisé à utiliser pour accéder à votre service.</span><span class="sxs-lookup"><span data-stu-id="8f40b-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="8f40b-122">Lorsque vous demandez un certificat auprès d’une autorité de certification, le nom d’objet du certificat doit correspondre au nom de domaine personnalisé que vous utilisez pour accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="8f40b-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="8f40b-123">Par exemple, si votre nom de domaine personnalisé est **contoso.com**, vous demandez un certificat auprès de votre autorité de certification pour **.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8f40b-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="8f40b-124">Le certificat doit utiliser au minimum un chiffrement à 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="8f40b-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="8f40b-125">Dans le cadre d’un test, vous pouvez [créer](cloud-services-certs-create.md) et utiliser un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="8f40b-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="8f40b-126">Un certificat auto-signé n'est pas authentifié par une autorité de certification et peut utiliser le domaine cloudapp.net comme URL de site Web.</span><span class="sxs-lookup"><span data-stu-id="8f40b-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="8f40b-127">Par exemple, la tâche ci-dessous utilise un certificat auto-signé dans lequel le nom commun utilisé dans le certificat est **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="8f40b-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="8f40b-128">Ensuite, vous devez ajouter des informations sur le certificat dans votre définition de service et dans les fichiers de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="8f40b-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="8f40b-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="8f40b-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="8f40b-130">Étape 2 : modification des fichiers de définition de service et de configuration</span><span class="sxs-lookup"><span data-stu-id="8f40b-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="8f40b-131">Votre application doit être configurée pour utiliser le certificat, et un point de terminaison HTTPS doit être ajouté.</span><span class="sxs-lookup"><span data-stu-id="8f40b-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="8f40b-132">Suite à cette opération, les fichiers de définition de service et de configuration de service doivent être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="8f40b-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="8f40b-133">Dans votre environnement de développement, ouvrez le fichier de définition du service (CSDEF), ajoutez une section **Certificates** dans la section **WebRole**, puis ajoutez les informations qui suivent sur le certificat (et les certificats intermédiaires) :</span><span class="sxs-lookup"><span data-stu-id="8f40b-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

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

   <span data-ttu-id="8f40b-134">La section **Certificates** définit le nom du certificat, son emplacement et le nom du magasin dans lequel il se trouve.</span><span class="sxs-lookup"><span data-stu-id="8f40b-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="8f40b-135">Les autorisations (attribut `permisionLevel`) peuvent être définies sur les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="8f40b-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="8f40b-136">Valeur de l’autorisation</span><span class="sxs-lookup"><span data-stu-id="8f40b-136">Permission Value</span></span> | <span data-ttu-id="8f40b-137">Description</span><span class="sxs-lookup"><span data-stu-id="8f40b-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="8f40b-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="8f40b-138">limitedOrElevated</span></span> |<span data-ttu-id="8f40b-139">**(Par défaut)** Tous les processus de rôle peuvent accéder à la clé privée.</span><span class="sxs-lookup"><span data-stu-id="8f40b-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="8f40b-140">elevated</span><span class="sxs-lookup"><span data-stu-id="8f40b-140">elevated</span></span> |<span data-ttu-id="8f40b-141">Seuls les processus élevés peuvent accéder à la clé privée.</span><span class="sxs-lookup"><span data-stu-id="8f40b-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="8f40b-142">Dans votre fichier de définition du service, ajoutez un élément **InputEndpoint** dans la section **Endpoints** pour activer HTTPS :</span><span class="sxs-lookup"><span data-stu-id="8f40b-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

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

3. <span data-ttu-id="8f40b-143">Dans votre fichier de définition du service, ajoutez un élément **Binding** dans la section **Sites**.</span><span class="sxs-lookup"><span data-stu-id="8f40b-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="8f40b-144">Cet élément ajoute une liaison HTTPS pour mapper le point de terminaison à votre site :</span><span class="sxs-lookup"><span data-stu-id="8f40b-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

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

   <span data-ttu-id="8f40b-145">Toutes les modifications nécessaires ont été apportées au fichier de définition de service, mais vous devez encore y ajouter les informations de certificat.</span><span class="sxs-lookup"><span data-stu-id="8f40b-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="8f40b-146">Dans votre fichier de configuration de service (CSCFG), ServiceConfiguration.Cloud.cscfg, ajoutez la valeur de votre certificat dans **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="8f40b-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="8f40b-147">L’exemple de code suivant fournit des détails sur la section **Certificats**, à l’exception de la valeur de l’empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="8f40b-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

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

<span data-ttu-id="8f40b-148">(Cet exemple utilise **sha1** comme algorithme d’empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="8f40b-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="8f40b-149">Spécifiez la valeur correspondant à l'algorithme d'empreinte numérique de votre certificat.)</span><span class="sxs-lookup"><span data-stu-id="8f40b-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="8f40b-150">Maintenant que les fichiers de définition du service et de configuration de service ont été mis à jour, créez un package pour votre déploiement afin de le télécharger dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8f40b-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="8f40b-151">Si vous utilisez **cspack**, n’utilisez pas l’indicateur **/generateConfigurationFile**, car les informations de certificat que vous venez juste d’entrer seraient écrasées.</span><span class="sxs-lookup"><span data-stu-id="8f40b-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="8f40b-152">Étape 3 : chargement d’un certificat</span><span class="sxs-lookup"><span data-stu-id="8f40b-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="8f40b-153">Connectez-vous au portail Azure et...</span><span class="sxs-lookup"><span data-stu-id="8f40b-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="8f40b-154">Dans la section **Toutes les ressources** du portail, sélectionnez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="8f40b-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![Publier votre service cloud](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="8f40b-156">Cliquez sur **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="8f40b-156">Click **Certificates**.</span></span>

    ![Cliquer sur l’icône Certificats](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="8f40b-158">Cliquez sur **Charger** en haut de la zone de certificats.</span><span class="sxs-lookup"><span data-stu-id="8f40b-158">Click **Upload** at the top of the certificates area.</span></span>

    ![Cliquez sur l’élément de menu de chargement](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="8f40b-160">Fournissez le **fichier**, entrez le **mot de passe**, puis cliquez sur **Charger** en bas de la zone de saisie de données.</span><span class="sxs-lookup"><span data-stu-id="8f40b-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="8f40b-161">Étape 4 : connexion à l’instance de rôle à l’aide de HTTPS</span><span class="sxs-lookup"><span data-stu-id="8f40b-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="8f40b-162">Maintenant que votre déploiement est opérationnel dans Azure, vous pouvez vous y connecter via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8f40b-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="8f40b-163">Cliquez sur **l’URL du site** pour ouvrir le navigateur web.</span><span class="sxs-lookup"><span data-stu-id="8f40b-163">Click the **Site URL** to open up the web browser.</span></span>

   ![Cliquez sur l'URL du site](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="8f40b-165">Dans votre navigateur Web, modifiez le lien pour utiliser **HTTPS** au lieu de **HTTP**, puis accédez à la page.</span><span class="sxs-lookup"><span data-stu-id="8f40b-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f40b-166">Si vous utilisez un certificat auto-signé, lorsque vous accédez à un point de terminaison HTTPS qui lui est associé, vous pourriez obtenir une erreur de certificat dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="8f40b-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="8f40b-167">Pour remédier à ce problème, utilisez un certificat signé par une autorité de certification approuvée. En attendant, vous pouvez ignorer cette erreur.</span><span class="sxs-lookup"><span data-stu-id="8f40b-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="8f40b-168">(Une autre possibilité est d'ajouter le certificat auto-signé au magasin de certificats d'autorité de certification approuvé de l'utilisateur.)</span><span class="sxs-lookup"><span data-stu-id="8f40b-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Aperçu du site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="8f40b-170">Si vous voulez utiliser SSL pour un déploiement intermédiaire au lieu d'un déploiement de production, vous devez d'abord déterminer l'URL utilisée pour le déploiement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="8f40b-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="8f40b-171">Une fois le service cloud déployé, l’URL de l’environnement intermédiaire est déterminée par le GUID **ID de déploiement** au format suivant : `https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="8f40b-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="8f40b-172">Créez un certificat avec le nom commun (CN) similaire à l’URL basée sur GUID (par exemple, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="8f40b-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="8f40b-173">Utilisez le portail pour ajouter le certificat à votre service cloud intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="8f40b-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="8f40b-174">Ensuite, ajoutez les informations du certificat à vos fichiers CSDEF et CSCFG, recréez le package de votre application et mettez à jour votre déploiement intermédiaire pour utiliser le nouveau package.</span><span class="sxs-lookup"><span data-stu-id="8f40b-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="8f40b-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f40b-175">Next steps</span></span>
* <span data-ttu-id="8f40b-176">[Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8f40b-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="8f40b-177">Découvrez comment [déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8f40b-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="8f40b-178">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8f40b-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="8f40b-179">[Gérez votre service cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8f40b-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
