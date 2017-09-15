### <a name="app-service-plan"></a><span data-ttu-id="097bb-101">Plan App Service</span><span class="sxs-lookup"><span data-stu-id="097bb-101">App Service plan</span></span>
<span data-ttu-id="097bb-102">Crée le plan de service pour l'hébergement de l'application web.</span><span class="sxs-lookup"><span data-stu-id="097bb-102">Creates the service plan for hosting the web app.</span></span> <span data-ttu-id="097bb-103">Vous fournissez le nom du plan à l'aide du paramètre **hostingPlanName** .</span><span class="sxs-lookup"><span data-stu-id="097bb-103">You provide the name of the plan through the **hostingPlanName** parameter.</span></span> <span data-ttu-id="097bb-104">L’emplacement du plan est identique à celui utilisé pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="097bb-104">The location of the plan is the same location used for the resource group.</span></span> <span data-ttu-id="097bb-105">Le niveau tarifaire et la taille de worker sont spécifiés dans les paramètres **sku** et **workerSize**.</span><span class="sxs-lookup"><span data-stu-id="097bb-105">The pricing tier and worker size are specified in the **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

