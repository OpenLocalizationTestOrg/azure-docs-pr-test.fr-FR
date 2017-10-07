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
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Résolution des problèmes liés à l’état détérioré d’Azure Traffic Manager

Cet article décrit comment tootroubleshoot un profil Traffic Manager de Azure qui affiche un état détérioré. Pour ce scénario, considérez que vous avez configuré un profil Traffic Manager pointant toosome de vos services hébergés de cloudapp.net. Si le contrôle d’intégrité hello votre Traffic Manager affiche une **détérioré** état, état hello d’un ou plusieurs points de terminaison peut être **détérioré**:

![statut du point de terminaison dégradé](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Si le contrôle d’intégrité hello votre Traffic Manager affiche une **inactif** état, les deux points de terminaison peut être **désactivé**:

![Statut Traffic Manager inactif](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Présentation des sondes de Traffic Manager

* Traffic Manager considère un toobe de point de terminaison en ligne uniquement lors de la sonde de hello reçoit une réponse HTTP 200 de nouveau chemin d’accès de la sonde hello. Toute réponse autre que 200 traduite un échec.
* Une redirection 30 x échoue, même si hello redirigée URL retourne une réponse 200.
* Pour les sondes HTTPs, les erreurs de certificat sont ignorées.
* contenu du chemin d’accès de la sonde hello Hello peu, tant que 200 est retourné. Détection d’un type de contenu statique toosome URL « / favicon.ico » est une technique courante. Le contenu dynamique, comme les pages ASP hello, ne retourne pas toujours 200, même lorsque l’application hello est saine.
* Une meilleure solution consiste à tooset hello sonde toosomething de chemin d’accès qui est suffisamment toodetermine logique qui hello site est vers le haut ou vers le bas. Bonjour exemple précédent, en définissant hello too"/favicon.ico de chemin d’accès », vous pouvez uniquement tester ce w3wp.exe répond. Cette sonde n’indique pas que votre application web est intègre. Une meilleure option ressemblerait alors tooset un tooa de chemin d’accès tel que « / Probe.aspx » qui a une logique toodetermine hello d’intégrité du site de hello. Par exemple, vous pouvez utiliser tooCPU l’utilisation des compteurs de performances ou un chiffre hello de mesure des demandes ayant échoué. Ou bien, vous risquez de ressources de base de données tooaccess ou toomake d’état session sûr que l’application web de hello fonctionne.
* Si le dégradé de tous les points de terminaison dans un profil, puis Traffic Manager traite tous les points de terminaison intègre et itinéraires du trafic tooall de points de terminaison. Ce comportement garantit que des problèmes avec le mécanisme de sonde de hello n’entraînent pas une panne complète de votre service.

## <a name="troubleshooting"></a>Résolution des problèmes

tootroubleshoot une défaillance de sonde, vous devez un outil qui affiche le code d’état HTTP hello retour à partir de l’URL de sonde hello. Il existe de nombreux outils disponibles qui affichent vous hello brute réponse HTTP.

* [Fiddler](http://www.telerik.com/fiddler)
* [curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

En outre, vous pouvez utiliser l’onglet réseau hello Hello des outils de débogage F12 dans Internet Explorer tooview hello des réponses HTTP.

Pour cet exemple, nous souhaitons réponse hello toosee nos URL de sonde : http://watestsdp2008r2.cloudapp.net:80/sonde. Hello l’exemple PowerShell suivant illustre le problème de hello.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Exemple de sortie :

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

Notez que nous avons reçu une réponse redirigée. Comme indiqué précédemment, tout StatusCode autre que 200 est considéré comme un échec. Modifications du Traffic Manager hello tooOffline d’état de point de terminaison. problème de hello tooresolve, cocher hello site Web configuration tooensure qui hello StatusCode approprié peut être retourné à partir du chemin d’accès de la sonde hello. Reconfigurez hello Traffic Manager sonde toopoint tooa chemin d’accès qui renvoie une réponse 200.

Si votre analyse utilise hello le protocole HTTPS, vous devrez peut-être certificat toodisable rechercher des erreurs SSL/TLS tooavoid pendant votre test. Hello instructions PowerShell suivantes désactiver la validation des certificats pour la session de PowerShell hello actuelle :

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

## <a name="next-steps"></a>Étapes suivantes

[À propos des méthodes de routage du trafic de Traffic Manager](traffic-manager-routing-methods.md)

[Qu’est-ce que Traffic Manager ?](traffic-manager-overview.md)

[Cloud Services](http://go.microsoft.com/fwlink/?LinkId=314074)

[Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/)

[Opérations sur Traffic Manager (Référence sur l’API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Applets de commande Azure Traffic Manager][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
