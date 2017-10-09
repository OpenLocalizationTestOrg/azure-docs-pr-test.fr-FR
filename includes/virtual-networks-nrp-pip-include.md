## <a name="public-ip-address"></a><span data-ttu-id="4a582-101">Adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="4a582-101">Public IP address</span></span>
<span data-ttu-id="4a582-102">Une ressource d’adresse IP publique fournit une adresse IP réservée ou une adresse IP dynamique accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="4a582-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="4a582-103">Vous pouvez créer une adresse IP publique en tant qu’objet autonome, vous devez tooassociate il tooanother objet tooactually utiliser l’adresse de hello.</span><span class="sxs-lookup"><span data-stu-id="4a582-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="4a582-104">Vous pouvez associer un équilibreur de charge tooa d’adresse IP publique, passerelle d’application ou un réseau tooprovide Internet access toothose des ressources.</span><span class="sxs-lookup"><span data-stu-id="4a582-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="4a582-105">Propriété</span><span class="sxs-lookup"><span data-stu-id="4a582-105">Property</span></span> | <span data-ttu-id="4a582-106">Description</span><span class="sxs-lookup"><span data-stu-id="4a582-106">Description</span></span> | <span data-ttu-id="4a582-107">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="4a582-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a582-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="4a582-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="4a582-109">Définit si l’adresse IP de hello est *statique* ou *dynamique*.</span><span class="sxs-lookup"><span data-stu-id="4a582-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="4a582-110">static, dynamic</span><span class="sxs-lookup"><span data-stu-id="4a582-110">static, dynamic</span></span> |
| <span data-ttu-id="4a582-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="4a582-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="4a582-112">Définit hello inactif délai d’expiration, valeur par défaut est de 4 minutes.</span><span class="sxs-lookup"><span data-stu-id="4a582-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="4a582-113">Si aucun autre paquet pour une session donnée n’est reçue dans ce délai, hello est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="4a582-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="4a582-114">Toute valeur aléatoire comprise entre 4 et 30.</span><span class="sxs-lookup"><span data-stu-id="4a582-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="4a582-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="4a582-115">**ipAddress**</span></span> |<span data-ttu-id="4a582-116">Adresse IP affectée tooobject.</span><span class="sxs-lookup"><span data-stu-id="4a582-116">IP address assigned tooobject.</span></span> <span data-ttu-id="4a582-117">Il s’agit d’une propriété en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="4a582-117">This is a read-only property.</span></span> |<span data-ttu-id="4a582-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="4a582-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="4a582-119">Paramètres DNS</span><span class="sxs-lookup"><span data-stu-id="4a582-119">DNS settings</span></span>
<span data-ttu-id="4a582-120">Les adresses IP publiques ont un objet enfant nommé **dnsSettings** contenant hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4a582-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="4a582-121">Propriété</span><span class="sxs-lookup"><span data-stu-id="4a582-121">Property</span></span> | <span data-ttu-id="4a582-122">Description</span><span class="sxs-lookup"><span data-stu-id="4a582-122">Description</span></span> | <span data-ttu-id="4a582-123">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="4a582-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a582-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="4a582-124">**domainNameLabel**</span></span> |<span data-ttu-id="4a582-125">Ordinateur hôte nommé utilisé pour la résolution de nom.</span><span class="sxs-lookup"><span data-stu-id="4a582-125">Host named used for name resolution.</span></span> |<span data-ttu-id="4a582-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="4a582-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="4a582-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="4a582-127">**fqdn**</span></span> |<span data-ttu-id="4a582-128">Nom qualifié complet pour l’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="4a582-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="4a582-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="4a582-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="4a582-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="4a582-130">**reverseFqdn**</span></span> |<span data-ttu-id="4a582-131">Nom de domaine complet qui résout l’adresse IP de toohello et qui est enregistré dans DNS comme un enregistrement PTR.</span><span class="sxs-lookup"><span data-stu-id="4a582-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="4a582-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4a582-132">www.contoso.com.</span></span> |

<span data-ttu-id="4a582-133">Exemple d’adresse IP publique au format JSON :</span><span class="sxs-lookup"><span data-stu-id="4a582-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="4a582-134">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4a582-134">Additional resources</span></span>
* <span data-ttu-id="4a582-135">Obtenez davantage d’informations sur les [adresses IP publiques](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="4a582-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="4a582-136">En savoir plus sur les [adresses IP publiques de niveau d’instance](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="4a582-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="4a582-137">Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) des adresses pour l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="4a582-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

