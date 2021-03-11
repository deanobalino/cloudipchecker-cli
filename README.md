# cloudipchecker-cli

A CLI utility for to the [Azure Cloud IP Checker](https://github.com/deanobalino/cloudipchecker)

Given an IP address, find out if the IP address resides in Azure, and if so, also get the Azure Service, Region and Address Prefix that IP belongs to. 

```
▶ cloudipchecker get --ip 13.72.105.31
```

## Installation

cloudipchecker-cli has no runtime dependencies. You can just [download a binary for Linux, Mac or Windows and run it](https://github.com/deanobalino/cloudipchecker-cli/releases).
Put the binary in your `$PATH` (e.g. in `/usr/local/bin`) to make it easy to use:
```
▶ tar xzf cloudipchecker_0.1.0_Linux_arm64.tar.gz
▶ sudo mv cloudipchecker /usr/local/bin/
```

Or if you're a Go user you can use `go get` (if you're using Go 1.7 or newer):

```
▶ go get -u github.com/deanobalino/cloudipchecker-cli
```


## Usage

Get details of an IP Address:

```
▶ cloudipchecker get --ip 13.72.105.31
Performing ip lookup for: 13.72.105.31 using data source: webjson
{
    "Status": 200,
    "Values": [
        {
            "Region": "",
            "Service": "AzureAdvancedThreatProtection",
            "AddressPrefix": "13.72.105.31/32"
        },
        {
            "Region": "eastus",
            "Service": "",
            "AddressPrefix": "13.72.64.0/18"
        },
        {
            "Region": "",
            "Service": "",
            "AddressPrefix": "13.72.64.0/18"
        }
    ]
}

```

Specify the data source (Azure Service Tag API or JSON Download):

>Note: The Azure Service Tag API is in preview and therefore may have limited results. The utility defaults to 'webjson'

```
▶ cloudipchecker get --ip 13.72.105.31 --source api
Performing ip lookup for: 13.72.105.31 using data source: api
{
    "Status": 200,
    "Values": [
        {
            "Region": "",
            "Service": "AzureAdvancedThreatProtection",
            "AddressPrefix": "13.72.105.31/32"
        },
        {
            "Region": "",
            "Service": "",
            "AddressPrefix": "13.72.64.0/18"
        },
        {
            "Region": "eastus",
            "Service": "",
            "AddressPrefix": "13.72.64.0/18"
        }
    ]
}
```

