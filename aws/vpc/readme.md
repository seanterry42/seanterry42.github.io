# Virtual Private Cloud (VPC) Setup
Amazon Web Services (AWS) Series: Part 1

## Create your VPC
Do yourself some huge favors:
  * Leave your *default* VPC alone except for walking through other tutorials. Don't delete it, but don't use it in production either.
  * Minimize your dependence on public IPv4 addresses. Elastic IPs (a.k.a. static public IPv4 addresses) are currently limited to 5 per region, and all other public IPv4 addresses are _dynamic_. Exposing your public-facing services with dual-stack (IPv4+IPv6) support without requiring Elastic IPs is remarkably easy. You'll want to save those precious Elastic IPs for the following:
    * Your NAT Gateway.
    * Your VPN host.
    * Services that can't operate behind Elastic Load Balancers (ELBs) nor reverse proxies.
  * Choose your region carefully - some services are not offered in all regions.

Create your VPC in the following manner:
  1. Log into the AWS console.
  2. Select the region in which you want to set up your VPC.
  3. In the *Services* drop-down, search for and select *VPC*.
  4. Click *Start VPC Wizard*.
  5. *IPv4 CIDR block* represents the private IPv4 address space available in your VPC. Tips to save you some pain: 
    * Select the largest size possible (/16).
    * Don't overlap the block with any other network you might want to communicate with. Site-to-site VPNs or VPC peering will require both ends to have their own unique block of addresses, so plan accordingly.
  6. For *IPv6 CIDR block*, select *Amazon provided IPv6 CIDR block*. This will allow you to utilize IPv6.
  7. For *Public subnet's IPv4 CIDR*, use a /20 mask.
  8. For *Public subnet's IPv6 CIDR* select *Specify a Custom IPv6 CIDR* and start your numbering at *00*.
  9. Use the Availability Zone ending in *a* for your region.
  10. For the name of the subnet, I recommend prefixing the availability zone with whether the subnet is public or private. For the first subnet, this is public.

Here are the settings I am using in my demo:
![VPC Settings](vpc-settings.png)
