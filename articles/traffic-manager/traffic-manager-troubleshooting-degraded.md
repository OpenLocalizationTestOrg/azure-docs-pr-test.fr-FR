---
title: "Résolution des problèmes liés à l’état détérioré d’Azure Traffic Manager"
description: "Comment résoudre les profils Traffic Manager lorsque l’état est affiché comme dégradé."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: b1d00fb84695d2289f37647f55a7c56cf28c8c96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="409dd-103">Résolution des problèmes liés à l’état détérioré d’Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="409dd-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="409dd-104">Cet article décrit comment résoudre les problèmes d’un profil Azure Traffic Manager qui présente un état détérioré.</span><span class="sxs-lookup"><span data-stu-id="409dd-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="409dd-105">Pour ce scénario, considérez que vous avez configuré un profil Traffic Manager pointant vers certains de vos services hébergés cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="409dd-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="409dd-106">Si le statut de l’intégrité de votre Traffic Manager est **Dégradé**, le statut d’un ou plusieurs points de terminaison peut être **Dégradé** :</span><span class="sxs-lookup"><span data-stu-id="409dd-106">If the health of your Traffic Manager displays a **Degraded** status, then the status of one or more endpoints may be **Degraded**:</span></span>

![statut du point de terminaison dégradé](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="409dd-108">Si le statut de l’intégrité de votre Traffic Manager est **Inactif**, les deux points de terminaison peuvent être **Inactifs** :</span><span class="sxs-lookup"><span data-stu-id="409dd-108">If the health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Statut Traffic Manager inactif](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="409dd-110">Présentation des sondes de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="409dd-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="409dd-111">Traffic Manager considère qu’un point de terminaison est EN LIGNE uniquement si la sonde reçoit une réponse HTTP 200 en retour du chemin d’accès de la sonde.</span><span class="sxs-lookup"><span data-stu-id="409dd-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="409dd-112">Toute réponse autre que 200 traduite un échec.</span><span class="sxs-lookup"><span data-stu-id="409dd-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="409dd-113">Une redirection 30 x échoue, même si l’URL redirigée retourne 200.</span><span class="sxs-lookup"><span data-stu-id="409dd-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="409dd-114">Pour les sondes HTTPs, les erreurs de certificat sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="409dd-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="409dd-115">Le contenu réel du chemin d’accès de la sonde n’importe pas, aussi longtemps que la valeur retournée est 200.</span><span class="sxs-lookup"><span data-stu-id="409dd-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="409dd-116">Le sondage d’une URL pour détecter du contenu statique, tel que « /favicon.ico », est une technique courante.</span><span class="sxs-lookup"><span data-stu-id="409dd-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="409dd-117">Un contenu dynamique, par exemple, des pages ASP, ne retourne pas toujours 200, même quand l’application est intègre.</span><span class="sxs-lookup"><span data-stu-id="409dd-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="409dd-118">La meilleure pratique consiste à définir le chemin d’accès de la sonde vers un élément disposant d’une logique suffisante pour déterminer si le site fonctionne ou est à l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="409dd-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="409dd-119">Dans l’exemple précédent, en définissant le chemin d’accès « /favicon.ico », vous ne faites que tester le fait que w3wp.exe répond.</span><span class="sxs-lookup"><span data-stu-id="409dd-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="409dd-120">Cette sonde n’indique pas que votre application web est intègre.</span><span class="sxs-lookup"><span data-stu-id="409dd-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="409dd-121">Une meilleure option consisterait à définir un chemin d’accès vers un élément tel que « /Probe.aspx » disposant de la logique nécessaire pour déterminer l’intégrité du site.</span><span class="sxs-lookup"><span data-stu-id="409dd-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="409dd-122">Par exemple, vous pourriez utiliser des compteurs de performances pour l’utilisation du processeur, ou mesurer le nombre de demandes ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="409dd-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="409dd-123">Vous pourriez également tenter d’accéder aux ressources de base de données ou à l’état de la session pour vous assurer que l’application web fonctionne.</span><span class="sxs-lookup"><span data-stu-id="409dd-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="409dd-124">Si tous les points de terminaison d’un profil sont détériorés, Traffic Manager traite tous les points de terminaison comme intègres, et achemine le trafic vers tous les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="409dd-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="409dd-125">Ce comportement garantit que les problèmes liés au mécanisme de sondage n’entraînent pas d’interruption complète de votre service.</span><span class="sxs-lookup"><span data-stu-id="409dd-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="409dd-126">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="409dd-126">Troubleshooting</span></span>

<span data-ttu-id="409dd-127">Pour résoudre un problème d’échec d’analyse, vous avez besoin d’un outil qui affiche le code d’état HTTP retourné à partir de l’URL de la sonde.</span><span class="sxs-lookup"><span data-stu-id="409dd-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="409dd-128">Il existe de nombreux outils qui affichent la réponse HTTP brute.</span><span class="sxs-lookup"><span data-stu-id="409dd-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="409dd-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="409dd-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="409dd-130">curl</span><span class="sxs-lookup"><span data-stu-id="409dd-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="409dd-131">wget</span><span class="sxs-lookup"><span data-stu-id="409dd-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="409dd-132">En outre, vous pouvez utiliser l’onglet réseau des outils de débogage F12 dans Internet Explorer pour afficher les réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="409dd-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="409dd-133">Pour cet exemple, voulons voir la réponse de l’URL de notre sonde : http://watestsdp2008r2.cloudapp.net:80/Probe.</span><span class="sxs-lookup"><span data-stu-id="409dd-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="409dd-134">L’exemple PowerShell suivant illustre le problème.</span><span class="sxs-lookup"><span data-stu-id="409dd-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="409dd-135">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="409dd-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="409dd-136">Notez que nous avons reçu une réponse redirigée.</span><span class="sxs-lookup"><span data-stu-id="409dd-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="409dd-137">Comme indiqué précédemment, tout StatusCode autre que 200 est considéré comme un échec.</span><span class="sxs-lookup"><span data-stu-id="409dd-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="409dd-138">Traffic Manager modifie l’état du point de terminaison en Hors connexion.</span><span class="sxs-lookup"><span data-stu-id="409dd-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="409dd-139">Pour résoudre le problème, vérifiez la configuration de site web pour vous assurer que le StatusCode approprié peut être retourné à partir du chemin d’accès de la sonde.</span><span class="sxs-lookup"><span data-stu-id="409dd-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="409dd-140">Reconfigurez la sonde Traffic Manager pour qu’elle pointe vers un chemin d’accès qui renvoie la valeur 200.</span><span class="sxs-lookup"><span data-stu-id="409dd-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="409dd-141">Si votre sonde utilise le protocole HTTPS, vous devez peut-être désactiver la vérification du certificat pour éviter les erreurs SSL/TLS pendant votre test.</span><span class="sxs-lookup"><span data-stu-id="409dd-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="409dd-142">Les instructions PowerShell suivantes désactivent la validation de certificat pour la session PowerShell :</span><span class="sxs-lookup"><span data-stu-id="409dd-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="409dd-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="409dd-143">Next Steps</span></span>

[<span data-ttu-id="409dd-144">À propos des méthodes de routage du trafic de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="409dd-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="409dd-145">Qu’est-ce que Traffic Manager ?</span><span class="sxs-lookup"><span data-stu-id="409dd-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="409dd-146">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="409dd-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="409dd-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="409dd-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="409dd-148">Opérations sur Traffic Manager (Référence sur l’API REST)</span><span class="sxs-lookup"><span data-stu-id="409dd-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="409dd-149">[Applets de commande Azure Traffic Manager][1]</span><span class="sxs-lookup"><span data-stu-id="409dd-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
