### <a name="app-service-plan"></a><span data-ttu-id="20ec9-101">Plan App Service</span><span class="sxs-lookup"><span data-stu-id="20ec9-101">App Service plan</span></span>
<span data-ttu-id="20ec9-102">Crée un plan de service hello pour l’hébergement de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="20ec9-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="20ec9-103">Vous fournissez le nom hello du plan hello via hello **hostingPlanName** paramètre.</span><span class="sxs-lookup"><span data-stu-id="20ec9-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="20ec9-104">emplacement Hello du plan de hello est hello même emplacement utilisé pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="20ec9-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="20ec9-105">taille de couche et de travail tarification Hello sont spécifiés dans hello **référence (SKU)** et **workerSize** paramètres</span><span class="sxs-lookup"><span data-stu-id="20ec9-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

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

