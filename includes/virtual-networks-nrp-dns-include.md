## <a name="azure-dns"></a><span data-ttu-id="bb54e-101">DNS Azure</span><span class="sxs-lookup"><span data-stu-id="bb54e-101">Azure DNS</span></span>
<span data-ttu-id="bb54e-102">Azure DNS est un service d'hébergement pour les domaines DNS et qui offre une résolution de noms à l'aide de l'infrastructure Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bb54e-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="bb54e-103">Propriété</span><span class="sxs-lookup"><span data-stu-id="bb54e-103">Property</span></span> | <span data-ttu-id="bb54e-104">Description</span><span class="sxs-lookup"><span data-stu-id="bb54e-104">Description</span></span> | <span data-ttu-id="bb54e-105">Exemple de valeur</span><span class="sxs-lookup"><span data-stu-id="bb54e-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb54e-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="bb54e-106">**DNSzones**</span></span> |<span data-ttu-id="bb54e-107">Enregistrements DNS toohost des informations de zone de domaine d’un domaine particulier</span><span class="sxs-lookup"><span data-stu-id="bb54e-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="bb54e-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="bb54e-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="bb54e-109">Jeux d'enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="bb54e-109">DNS record sets</span></span>
<span data-ttu-id="bb54e-110">Les zones DNS ont un objet enfant appelé jeu d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="bb54e-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="bb54e-111">Les jeux d'enregistrements sont un ensemble d'enregistrements hôtes par type pour une zone DNS.</span><span class="sxs-lookup"><span data-stu-id="bb54e-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="bb54e-112">Les types d'enregistrements sont A, AAAA, CNAME, MX, NS, SOA,SRV et TXT.</span><span class="sxs-lookup"><span data-stu-id="bb54e-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="bb54e-113">Propriété</span><span class="sxs-lookup"><span data-stu-id="bb54e-113">Property</span></span> | <span data-ttu-id="bb54e-114">Description</span><span class="sxs-lookup"><span data-stu-id="bb54e-114">Description</span></span> | <span data-ttu-id="bb54e-115">Exemple de valeur</span><span class="sxs-lookup"><span data-stu-id="bb54e-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb54e-116">Une</span><span class="sxs-lookup"><span data-stu-id="bb54e-116">A</span></span> |<span data-ttu-id="bb54e-117">Type d'enregistrement IPv4</span><span class="sxs-lookup"><span data-stu-id="bb54e-117">IPv4 record type</span></span> |<span data-ttu-id="bb54e-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="bb54e-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="bb54e-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="bb54e-119">AAAA</span></span> |<span data-ttu-id="bb54e-120">Type d'enregistrement IPv6</span><span class="sxs-lookup"><span data-stu-id="bb54e-120">IPv6 record type</span></span> |<span data-ttu-id="bb54e-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="bb54e-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="bb54e-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="bb54e-122">CNAME</span></span> |<span data-ttu-id="bb54e-123">type d'enregistrement nom canonique <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="bb54e-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="bb54e-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="bb54e-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="bb54e-125">MX</span><span class="sxs-lookup"><span data-stu-id="bb54e-125">MX</span></span> |<span data-ttu-id="bb54e-126">type d'enregistrement messagerie</span><span class="sxs-lookup"><span data-stu-id="bb54e-126">mail record type</span></span> |<span data-ttu-id="bb54e-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="bb54e-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="bb54e-128">NS</span><span class="sxs-lookup"><span data-stu-id="bb54e-128">NS</span></span> |<span data-ttu-id="bb54e-129">type d'enregistrement serveur nom</span><span class="sxs-lookup"><span data-stu-id="bb54e-129">name server record type</span></span> |<span data-ttu-id="bb54e-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="bb54e-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="bb54e-131">SOA</span><span class="sxs-lookup"><span data-stu-id="bb54e-131">SOA</span></span> |<span data-ttu-id="bb54e-132">Type d'enregistrement « SOA » (Start of Authority) <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="bb54e-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="bb54e-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="bb54e-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="bb54e-134">SRV</span><span class="sxs-lookup"><span data-stu-id="bb54e-134">SRV</span></span> |<span data-ttu-id="bb54e-135">type d'enregistrement service</span><span class="sxs-lookup"><span data-stu-id="bb54e-135">service record type</span></span> |<span data-ttu-id="bb54e-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="bb54e-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="bb54e-137"><sup>1</sup> autorise uniquement une valeur par jeu d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="bb54e-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="bb54e-138"><sup>2</sup> autorise uniquement un type d'enregistrement SOA par zone DNS.</span><span class="sxs-lookup"><span data-stu-id="bb54e-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="bb54e-139">Exemple de zone DNS au format Json :</span><span class="sxs-lookup"><span data-stu-id="bb54e-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="bb54e-140">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bb54e-140">Additional resources</span></span>
<span data-ttu-id="bb54e-141">Hello de lecture [documentation API REST pour les zones DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="bb54e-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="bb54e-142">Hello de lecture [documentation API REST pour les jeux d’enregistrements DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="bb54e-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

