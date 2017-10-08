### <a name="app-service-plan"></a>Plan App Service
Crée un plan de service hello pour l’hébergement de l’application web hello. Vous fournissez le nom hello du plan hello via hello **hostingPlanName** paramètre. emplacement Hello du plan de hello est hello même emplacement utilisé pour le groupe de ressources hello. taille de couche et de travail tarification Hello sont spécifiés dans hello **référence (SKU)** et **workerSize** paramètres

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

