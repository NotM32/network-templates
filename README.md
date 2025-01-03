This repository contains configuration templates that are intended to be consumed and populated by [Netbox](https://github.com/netbox-community/netbox)

## About
While somewhat biased to my use cases practices, I'm publishing these with the intent that they can serve as a starting point for other users who couldn't find good examples.

For network hardware, most of the generic vendor operating system specific configuration bits should be easy to reuse. For more intricate parts of the configuration, like BGP and other routing protocols, you'll probably have to extend/modify/replace what I've provided.

For each vendor, there are also quite a few security related configuration options that I've added, which may need to be changed to fit your organization's policy.

## Supported network vendor OSes
I run a mixed vendor network, with mostly Arista core gear. We have Juniper switches for our office network, and older Cisco switches supporting some legacy business segments in the datacenter.

For our internet facing routers, I use FRR which I've compiled to support DPDK/eXpress Data Path. I configure that without the help of Netbox templates for the time being, and as such it is not seen in this repository yet either 

That said, I support and target the following vendor specifix operating systems
- Arista eOS
- Juniper JunOS
- Cisco iOS
- Cisco NXOS (not included, as we just use the iOS config. There are no specialties we've encountered with our use-case)

### Other use cases
We have a Harvester cluster that gets scaled up/down ocassionaly, with the underlying machines often being repurposed. It's handy to be able to automate installs for this cluster, and as such I've found that providing the intiial setup/network configuration of a node to the iPXE boot script is handy. There is a configuration template for use with harvester boot here.

This process is middlemanned by a server I've written to handle getting the negotiation between the netboot environment and netbox's endpoint. I have some other utilities in that server for resetting the IPMI BMC address and access credentials of machines from various vendors as well. If anyone reading is interested in that, I'd be happy to sanitize that repo and publicize it.

## Verify before you apply!
It goes without saying, but you should definitely triple check the configuration that these repository generates for your device before applying it. I haven't perfected this repository, and there are some hardcoded ip access lists and options that could lock you out of your control plane.

## Roles of templates
Netbox and it's configuration template feature is well abstracted and is able to fill a variety of use cases. While primarily used for network automation, there are many creative use cases that can extend beyond the network.

Some other ideas for template use cases (contributions welcome!):
- Cloudinit YAML files
- NixOS Node Configuration Snippets (presumably for network/hostname setting)
- SNMP OID R/W value setting for devices that are hard to configure otherwise?
- Generating templates that can be consumed by tools that validate hardware inventory against netbox state for security stuff
