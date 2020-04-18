# List Existing VNets

```bash
az network vnet list --output table
```

```
Name    ResourceGroup    Location      NumSubnets    Prefixes     DnsServers    DDOSProtection    VMProtection
------  ---------------  ------------  ------------  -----------  ------------  ----------------  --------------
vnet    playground-rg    koreacentral  2             10.0.0.0/16                False             False
```

# Create subnet: 
```
az network vnet subnet create -g playground-rg --vnet-name vnet -n subnet --address-prefix 10.0.1.0/24
```

```json
{
  "addressPrefix": "10.0.1.0/24",
  "addressPrefixes": null,
  "delegations": [],
  "etag": "W/\"84bd61ff-fe5d-4dd9-afdf-a80f3050e7b6\"",
  "id": "/subscriptions/ec70b9b8-46a0-4a8c-b2bf-992c3ba4d810/resourceGroups/playground-rg/providers/Microsoft.Network/virtualNetworks/vnet/subnets/subnet",
  "ipConfigurationProfiles": null,
  "ipConfigurations": null,
  "name": "subnet",
  "natGateway": null,
  "networkSecurityGroup": null,
  "privateEndpointNetworkPolicies": "Enabled",
  "privateEndpoints": null,
  "privateLinkServiceNetworkPolicies": "Enabled",
  "provisioningState": "Succeeded",
  "purpose": null,
  "resourceGroup": "playground-rg",
  "resourceNavigationLinks": null,
  "routeTable": null,
  "serviceAssociationLinks": null,
  "serviceEndpointPolicies": null,
  "serviceEndpoints": null,
  "type": "Microsoft.Network/virtualNetworks/subnets"
}
```

# Create a NIC: 
```
az network nic create -g playground-rg --vnet-name vnet --subnet subnet -n nic
```

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "51z0whmfsvke1n2fgn2yrallvd.syx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"72f71008-9fed-44a9-9ffa-036f8eefe45e\"",
    "hostedWorkloads": [],
    "id": "/subscriptions/ec70b9b8-46a0-4a8c-b2bf-992c3ba4d810/resourceGroups/playground-rg/providers/Microsoft.Network/networkInterfaces/nic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "applicationSecurityGroups": null,
        "etag": "W/\"72f71008-9fed-44a9-9ffa-036f8eefe45e\"",
        "id": "/subscriptions/ec70b9b8-46a0-4a8c-b2bf-992c3ba4d810/resourceGroups/playground-rg/providers/Microsoft.Network/networkInterfaces/nic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "10.0.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "privateLinkConnectionProperties": null,
        "provisioningState": "Succeeded",
        "publicIpAddress": null,
        "resourceGroup": "playground-rg",
        "subnet": {
          "addressPrefix": null,
          "addressPrefixes": null,
          "delegations": null,
          "etag": null,
          "id": "/subscriptions/ec70b9b8-46a0-4a8c-b2bf-992c3ba4d810/resourceGroups/playground-rg/providers/Microsoft.Network/virtualNetworks/vnet/subnets/subnet",
          "ipConfigurationProfiles": null,
          "ipConfigurations": null,
          "name": null,
          "natGateway": null,
          "networkSecurityGroup": null,
          "privateEndpointNetworkPolicies": null,
          "privateEndpoints": null,
          "privateLinkServiceNetworkPolicies": null,
          "provisioningState": null,
          "purpose": null,
          "resourceGroup": "playground-rg",
          "resourceNavigationLinks": null,
          "routeTable": null,
          "serviceAssociationLinks": null,
          "serviceEndpointPolicies": null,
          "serviceEndpoints": null
        },
        "type": "Microsoft.Network/networkInterfaces/ipConfigurations",
        "virtualNetworkTaps": null
      }
    ],
    "location": "koreacentral",
    "macAddress": null,
    "name": "nic",
    "networkSecurityGroup": null,
    "primary": null,
    "privateEndpoint": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "playground-rg",
    "resourceGuid": "ca321750-fafc-40f8-957f-e2986189c1c1",
    "tags": null,
    "tapConfigurations": [],
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```