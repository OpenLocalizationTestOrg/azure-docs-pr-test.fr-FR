---
title: Configuration de l'authentification mutuelle TLS pour une application Web
description: "Découvrez comment configurer votre application Web pour utiliser l'authentification par certificat client sur TLS."
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: db69852cffd1ff331ac4a640b04ea4360d00bf75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="1df2b-103">Configuration de l'authentification mutuelle TLS pour une application Web</span><span class="sxs-lookup"><span data-stu-id="1df2b-103">How To Configure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="1df2b-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1df2b-104">Overview</span></span>
<span data-ttu-id="1df2b-105">Vous pouvez restreindre l'accès à votre application Web Azure en activant différents types d'authentification.</span><span class="sxs-lookup"><span data-stu-id="1df2b-105">You can restrict access to your Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="1df2b-106">Une méthode consiste à authentifier à l'aide d'un certificat client lorsque la requête est exécutée sur TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="1df2b-106">One way to do so is to authenticate using a client certificate when the request is over TLS/SSL.</span></span> <span data-ttu-id="1df2b-107">Ce mécanisme est appelé authentification mutuelle TLS ou authentification par certificat client. Cet article décrit en détail comment configurer votre application Web pour utiliser l'authentification par certificat client.</span><span class="sxs-lookup"><span data-stu-id="1df2b-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how to setup your web app to use client certificate authentication.</span></span>

> <span data-ttu-id="1df2b-108">**Remarque :** si vous accédez à votre site sur HTTP et non HTTPS, vous ne recevez pas de certificat client.</span><span class="sxs-lookup"><span data-stu-id="1df2b-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="1df2b-109">Par conséquent, si votre application requiert des certificats clients, vous ne devez pas autoriser les demandes à votre application sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="1df2b-109">So if your application requires client certificates you should not allow requests to your application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="1df2b-110">Configuration d'une application Web pour l'authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="1df2b-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="1df2b-111">Pour configurer votre application Web afin qu'elle exige des certificats clients, vous devez ajouter le paramètre de site clientCertEnabled pour votre application Web et lui donner la valeur true.</span><span class="sxs-lookup"><span data-stu-id="1df2b-111">To setup your web app to require client certificates you need to add the clientCertEnabled site setting for your web app and set it to true.</span></span> <span data-ttu-id="1df2b-112">Ce paramètre n’est actuellement pas disponible par le biais de l’expérience de gestion dans le portail et vous devrez utiliser l’API REST pour y parvenir.</span><span class="sxs-lookup"><span data-stu-id="1df2b-112">This setting is not currently available through the management experience in the Portal, and the REST API will need to be used to accomplish this.</span></span>

<span data-ttu-id="1df2b-113">Vous pouvez utiliser l' [outil ARMClient](https://github.com/projectkudu/ARMClient) pour faciliter l’élaboration de l’appel de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="1df2b-113">You can use the [ARMClient tool](https://github.com/projectkudu/ARMClient) to make it easy to craft the REST API call.</span></span> <span data-ttu-id="1df2b-114">Une fois que vous êtes connecté avec l'outil, vous devez émettre la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1df2b-114">After you log in with the tool you will need to issue the following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="1df2b-115">en remplaçant tous les éléments {} par des informations de votre application Web et en créant un fichier appelé enableclientcert.json avec le contenu JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="1df2b-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with the following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="1df2b-116">Veillez à modifier la valeur de « location » par l'emplacement de votre application Web ; par exemple, Nord du centre des États-Unis ou Ouest des États-Unis, etc.</span><span class="sxs-lookup"><span data-stu-id="1df2b-116">Make sure to change the value of "location" to wherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="1df2b-117">Vous pouvez également utiliser https://resources.azure.com pour basculer la propriété `clientCertEnabled` sur `true`.</span><span class="sxs-lookup"><span data-stu-id="1df2b-117">You can also use https://resources.azure.com to flip the `clientCertEnabled` property to `true`.</span></span>

> <span data-ttu-id="1df2b-118">**Remarque :** si vous exécutez ARMClient à partir de PowerShell, vous devez placer dans une séquence d’échappement le symbole @ pour le fichier JSON avec une apostrophe inversée (\`).</span><span class="sxs-lookup"><span data-stu-id="1df2b-118">**Note:** If you run ARMClient from Powershell, you will need to escape the @ symbol for the JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-the-client-certificate-from-your-web-app"></a><span data-ttu-id="1df2b-119">Accès au certificat client à partir de votre application Web</span><span class="sxs-lookup"><span data-stu-id="1df2b-119">Accessing the Client Certificate From Your Web App</span></span>
<span data-ttu-id="1df2b-120">Si vous utilisez ASP.NET et configurez votre application pour utiliser l’authentification de certificat client, le certificat est disponible au moyen de la propriété **HttpRequest.ClientCertificate** .</span><span class="sxs-lookup"><span data-stu-id="1df2b-120">If you are using ASP.NET and configure your app to use client certificate authentication, the certificate will be available through the **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="1df2b-121">Pour les autres piles d’application, le certificat client est disponible dans votre application par le biais d’une valeur codée en base64 dans l’en-tête de la requête « X-ARR-ClientCert ».</span><span class="sxs-lookup"><span data-stu-id="1df2b-121">For other application stacks, the client cert will be available in your app through a base64 encoded value in the "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="1df2b-122">Votre application peut créer un certificat à partir de cette valeur et ensuite l'utiliser à des fins d'authentification et d'autorisation dans votre application.</span><span class="sxs-lookup"><span data-stu-id="1df2b-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="1df2b-123">Considérations spéciales pour la validation de certificat</span><span class="sxs-lookup"><span data-stu-id="1df2b-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="1df2b-124">Le certificat client qui est envoyé à l'application n'est soumis à aucune validation par la plateforme Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1df2b-124">The client certificate that is sent to the application does not go through any validation by the Azure Web Apps platform.</span></span> <span data-ttu-id="1df2b-125">La validation de ce certificat est la responsabilité de l'application Web.</span><span class="sxs-lookup"><span data-stu-id="1df2b-125">Validating this certificate is the responsibility of the web app.</span></span> <span data-ttu-id="1df2b-126">Voici un exemple de code ASP.NET qui valide les propriétés du certificat pour l'authentification.</span><span class="sxs-lookup"><span data-stu-id="1df2b-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read the certificate from the header into an X509Certificate2 object
            // Display properties of the certificate on the page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept the certificate as a valid certificate if all the conditions below are met:
                // 1. The certificate is not expired and is active for the current time on server.
                // 2. The subject name of the certificate has the common name nildevecc
                // 3. The issuer name of the certificate has the common name nildevecc and organization name Microsoft Corp
                // 4. The thumbprint of the certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained to a Trusted Root Authority (or revoked) on the server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want to test if the certificate chains to a Trusted Root Authority you can uncomment the code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
