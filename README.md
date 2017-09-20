# vRealize
Terraform vRealize provider

## Introduction
This provider uses the https://github.com/sky-uk/govrealize client library to implement creation, reading and deletion vRealize machines.

## Usage
Build the provider
```bash
go build -o terraform-provider-vrealize github.com/sky-uk/terraform-provider-vrealize && cp terraform-provider-vrealize /usr/local/terraform/
```
Configure vRealize provider in a .tf file
```golang
provider "vrealize" {
	username = "xxxxxxxx"
	password = "xxxxxxxx"
	tenant =   "vsphere"
	server = "server.com"
}
```
Define resource
```golang
resource "vrealize_machine" "test" {
    catalog_item_ref_id = "xxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxx"
    tenant_ref = "vsphere.local"
    sub_tenant_ref = "xxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxx"
		request_data = {
			key = "provider-provisioningGroupId"
			value = "xxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxx"
		}
		request_data = {
			key = "provider-VirtualMachine.CPU.Count"
			value = 1
		}
		request_data = {
			key = "provider-VirtualMachine.Memory.Size"
			value = 1024
		}
		request_data = {
			key = "provider-Cafe.Shim.VirtualMachine.Description"
			value = "Test API request"
		}
		request_data = {
			key = "reasons"
			value = "Test reason"
		}
}
```
Execute provisioners
```golang
connection {
  user     = "user"
  password = "password"
}

provisioner "file" {
  source      = "test.sh"
  destination = "/tmp/terraform.sh"
}

provisioner "remote-exec" {
  inline = [
    "chmod +x /tmp/terraform.sh",
    "/tmp/terraform.sh",
  ]
}
```
