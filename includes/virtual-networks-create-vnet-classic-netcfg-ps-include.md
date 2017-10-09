## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>Comment toocreate un réseau virtuel à l’aide d’une configuration de réseau de fichiers à partir de PowerShell
Azure utilise une toodefine de fichier xml abonnement de tooa disponibles tous les réseaux virtuels. Vous pouvez télécharger ce fichier, toomodify le modifier ou supprimer des réseaux virtuels existants et créer de nouveaux réseaux virtuels. Dans ce didacticiel, vous apprendrez comment toodownload ce fichier, appelée tooas fichier de configuration (ou netcfg) du réseau et le modifier toocreate un réseau virtuel. toolearn en savoir plus sur le fichier de configuration de réseau hello, consultez hello [schéma de configuration de réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate un réseau virtuel avec un fichier netcfg à l’aide de PowerShell, hello complète comme suit :

1. Si vous n’avez jamais utilisé Azure PowerShell, hello terminé les étapes Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) de l’article, puis connectez-vous à tooAzure et sélectionnez votre abonnement.
2. À partir de la console Azure PowerShell hello, utilisez hello **Get-AzureVnetConfig** applet de commande toodownload hello configuration tooa répertoire de fichiers réseau sur votre ordinateur en exécutant hello de commande suivante : 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Sortie attendue :
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Ouvrir le fichier hello enregistré à l’étape 2 à l’aide de n’importe quelle application de l’éditeur XML ou texte et recherchez hello  **<VirtualNetworkSites>**  élément. Si vous avez déjà créé des réseaux, chacun est affiché comme son propre élément **<VirtualNetworkSite>**.
4. réseau virtuel de toocreate hello décrite dans ce scénario, ajoutez hello XML suivant juste sous hello  **<VirtualNetworkSites>**  élément :

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. Enregistrez le fichier de configuration de réseau hello.
6. À partir de la console Azure PowerShell hello, utilisez hello **Set-AzureVnetConfig** fichier de configuration de réseau applet de commande tooupload hello en exécutant hello de commande suivante : 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Sortie retournée :
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Si **OperationStatus** n’est pas *Succeeded* Bonjour retourné de sortie, vérifiez à nouveau fichier xml de hello pour les erreurs et l’étape 6.

7. À partir de la console Azure PowerShell hello, utilisez hello **Get-AzureVnetSite** tooverify d’applet de commande qui hello nouveau réseau a été ajouté en exécutant hello de commande suivante : 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Hello retourné sortie (abrégé) inclut hello suivant du texte :
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
