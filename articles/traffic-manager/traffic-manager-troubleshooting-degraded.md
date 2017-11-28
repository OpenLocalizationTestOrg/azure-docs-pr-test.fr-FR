---
title: "état d’aaaTroubleshooting dégradée sur Azure Traffic Manager"
description: "Comment tootroubleshoot lorsqu’il apparaît comme étant des profils Traffic Manager de l’état dégradé."
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
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="8c343-103">Résolution des problèmes liés à l’état détérioré d’Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8c343-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="8c343-104">Cet article décrit comment tootroubleshoot un profil Traffic Manager de Azure qui affiche un état détérioré.</span><span class="sxs-lookup"><span data-stu-id="8c343-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="8c343-105">Pour ce scénario, considérez que vous avez configuré un profil Traffic Manager pointant toosome de vos services hébergés de cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="8c343-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="8c343-106">Si le contrôle d’intégrité hello votre Traffic Manager affiche une **détérioré** état, état hello d’un ou plusieurs points de terminaison peut être **détérioré**:</span><span class="sxs-lookup"><span data-stu-id="8c343-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![statut du point de terminaison dégradé](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="8c343-108">Si le contrôle d’intégrité hello votre Traffic Manager affiche une **inactif** état, les deux points de terminaison peut être **désactivé**:</span><span class="sxs-lookup"><span data-stu-id="8c343-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Statut Traffic Manager inactif](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="8c343-110">Présentation des sondes de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8c343-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="8c343-111">Traffic Manager considère un toobe de point de terminaison en ligne uniquement lors de la sonde de hello reçoit une réponse HTTP 200 de nouveau chemin d’accès de la sonde hello.</span><span class="sxs-lookup"><span data-stu-id="8c343-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="8c343-112">Toute réponse autre que 200 traduite un échec.</span><span class="sxs-lookup"><span data-stu-id="8c343-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="8c343-113">Une redirection 30 x échoue, même si hello redirigée URL retourne une réponse 200.</span><span class="sxs-lookup"><span data-stu-id="8c343-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="8c343-114">Pour les sondes HTTPs, les erreurs de certificat sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="8c343-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="8c343-115">contenu du chemin d’accès de la sonde hello Hello peu, tant que 200 est retourné.</span><span class="sxs-lookup"><span data-stu-id="8c343-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="8c343-116">Détection d’un type de contenu statique toosome URL « / favicon.ico » est une technique courante.</span><span class="sxs-lookup"><span data-stu-id="8c343-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="8c343-117">Le contenu dynamique, comme les pages ASP hello, ne retourne pas toujours 200, même lorsque l’application hello est saine.</span><span class="sxs-lookup"><span data-stu-id="8c343-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="8c343-118">Une meilleure solution consiste à tooset hello sonde toosomething de chemin d’accès qui est suffisamment toodetermine logique qui hello site est vers le haut ou vers le bas.</span><span class="sxs-lookup"><span data-stu-id="8c343-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="8c343-119">Bonjour exemple précédent, en définissant hello too"/favicon.ico de chemin d’accès », vous pouvez uniquement tester ce w3wp.exe répond.</span><span class="sxs-lookup"><span data-stu-id="8c343-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="8c343-120">Cette sonde n’indique pas que votre application web est intègre.</span><span class="sxs-lookup"><span data-stu-id="8c343-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="8c343-121">Une meilleure option ressemblerait alors tooset un tooa de chemin d’accès tel que « / Probe.aspx » qui a une logique toodetermine hello d’intégrité du site de hello.</span><span class="sxs-lookup"><span data-stu-id="8c343-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="8c343-122">Par exemple, vous pouvez utiliser tooCPU l’utilisation des compteurs de performances ou un chiffre hello de mesure des demandes ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="8c343-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="8c343-123">Ou bien, vous risquez de ressources de base de données tooaccess ou toomake d’état session sûr que l’application web de hello fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8c343-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="8c343-124">Si le dégradé de tous les points de terminaison dans un profil, puis Traffic Manager traite tous les points de terminaison intègre et itinéraires du trafic tooall de points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8c343-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="8c343-125">Ce comportement garantit que des problèmes avec le mécanisme de sonde de hello n’entraînent pas une panne complète de votre service.</span><span class="sxs-lookup"><span data-stu-id="8c343-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8c343-126">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="8c343-126">Troubleshooting</span></span>

<span data-ttu-id="8c343-127">tootroubleshoot une défaillance de sonde, vous devez un outil qui affiche le code d’état HTTP hello retour à partir de l’URL de sonde hello.</span><span class="sxs-lookup"><span data-stu-id="8c343-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="8c343-128">Il existe de nombreux outils disponibles qui affichent vous hello brute réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c343-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="8c343-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="8c343-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="8c343-130">curl</span><span class="sxs-lookup"><span data-stu-id="8c343-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="8c343-131">wget</span><span class="sxs-lookup"><span data-stu-id="8c343-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="8c343-132">En outre, vous pouvez utiliser l’onglet réseau hello Hello des outils de débogage F12 dans Internet Explorer tooview hello des réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c343-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="8c343-133">Pour cet exemple, nous souhaitons réponse hello toosee nos URL de sonde : http://watestsdp2008r2.cloudapp.net:80/sonde.</span><span class="sxs-lookup"><span data-stu-id="8c343-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="8c343-134">Hello l’exemple PowerShell suivant illustre le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="8c343-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="8c343-135">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="8c343-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="8c343-136">Notez que nous avons reçu une réponse redirigée.</span><span class="sxs-lookup"><span data-stu-id="8c343-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="8c343-137">Comme indiqué précédemment, tout StatusCode autre que 200 est considéré comme un échec.</span><span class="sxs-lookup"><span data-stu-id="8c343-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="8c343-138">Modifications du Traffic Manager hello tooOffline d’état de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8c343-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="8c343-139">problème de hello tooresolve, cocher hello site Web configuration tooensure qui hello StatusCode approprié peut être retourné à partir du chemin d’accès de la sonde hello.</span><span class="sxs-lookup"><span data-stu-id="8c343-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="8c343-140">Reconfigurez hello Traffic Manager sonde toopoint tooa chemin d’accès qui renvoie une réponse 200.</span><span class="sxs-lookup"><span data-stu-id="8c343-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="8c343-141">Si votre analyse utilise hello le protocole HTTPS, vous devrez peut-être certificat toodisable rechercher des erreurs SSL/TLS tooavoid pendant votre test.</span><span class="sxs-lookup"><span data-stu-id="8c343-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="8c343-142">Hello instructions PowerShell suivantes désactiver la validation des certificats pour la session de PowerShell hello actuelle :</span><span class="sxs-lookup"><span data-stu-id="8c343-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8c343-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c343-143">Next Steps</span></span>

[<span data-ttu-id="8c343-144">À propos des méthodes de routage du trafic de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8c343-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="8c343-145">Qu’est-ce que Traffic Manager ?</span><span class="sxs-lookup"><span data-stu-id="8c343-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="8c343-146">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="8c343-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="8c343-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="8c343-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="8c343-148">Opérations sur Traffic Manager (Référence sur l’API REST)</span><span class="sxs-lookup"><span data-stu-id="8c343-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="8c343-149">[Applets de commande Azure Traffic Manager][1]</span><span class="sxs-lookup"><span data-stu-id="8c343-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
