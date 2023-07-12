import requests
import urllib3
import csv

from vmware.vapi.vsphere.client import create_vsphere_client
session = requests.session()

# Disable cert verification for demo purpose. 
# This is not recommended in a production environment.
session.verify = False

# Disable the secure connection warning for demo purpose.
# This is not recommended in a production environment.
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

# Connect to a vCenter Server using username and password
  vsphere_client = create_vsphere_client(server='VC_IP', username='Account_Username', password='credentials', session=session)

# List all VMs inside the vCenter Server

# Get a list of VMs
vm_list = vsphere_client.vcenter.VM.list()
#print(vm_list)
vm_details = []
# Write the VM list to a CSV file
for vm in vm_list:
    # Retrieve the full set of properties for the VM
    vm_details.append(vsphere_client.vcenter.VM.get(vm))
print(vm_details)
      with open('file.csv', mode='w', newline='') as file:
    writer = csv.writer(file)
    writer.writerow(['Name', 'Power State', 'Memory', 'CPU', 'Guest OS'])
    for vm in vm_details:
        name = vm.name
        power_state = vm.power_state
        memory = vm.memory_size_mib
        cpu = vm.cpu_count
        guest_os = vm.guest.guest_family + ' ' + vm.guest.guest_full_name
        writer.writerow([name, power_state, memory, cpu, guest_os])
