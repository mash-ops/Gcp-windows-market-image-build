# Gcp-windows-market-image-build
#Build VM from GCP Market place, Apply OS hardening, App, ceriticates, latest updates and sysprep the VM and capture Image
# pyenv versions
  system
* 3.8.10 (set by ~deployer/.pyenv/version)

## ansible --version

ansible [core 2.11.1]

config file = None

configured module search path = ['~deployer/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']

ansible python module location = ~deployer/.pyenv/versions/3.8.10/lib/python3.8/site-packages/ansible

ansible collection location = ~deployer/.ansible/collections:/usr/share/ansible/collections

executable location = ~deployer/.pyenv/versions/3.8.10/bin/ansible

python version = 3.8.10 (default, Jun  3 2021, 18:00:45) [GCC 4.8.5]

jinja version = 3.0.1

libyaml = True

-------------
Since winrm is restricted from dcXX to control host, build has to be split between control host and DC54 rundeck
1) run on image build : ansible-playbook -e "vm_name=w16dc-gcpbld-v1" gcp_mkt_vm_create.yml -vvv
2) run below on dcXXrundeck as deployer user
	#### ansible-playbook -i Rundeck_IP, ~user/gcp/marketBuild/win_copy.yml -vvv
	#### ansible-playbook -i Rundeck_IP, ~user/gcp/marketBuild/win_harden.yml -vvvv
	#### ansible-playbook -i Rundeck_IP, ~user/gcp/marketBuild/win_App_inst_cleanup.yml -vvvv
