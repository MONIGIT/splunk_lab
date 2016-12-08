# splunk_lab
repo for all my splunk lab works (vagrant, ansible).

Note:
I am happy to receive feedback, comment and improvement ideas :-)

I shall shortly start committing a mix of vagrantfile ansible playbook (+roles) to build the following;

(all based on splunk enterprise 6.5.x [evaluation/trial editions])
centos 7.2 minimal (most linux distros will work)
vagrant
virtualbox (about to test vmware esxi as an endpoint)
1x cpu
512mb mem

1x index cluster master (including license master and search head deployer roles)
3x index cluster peers
3x search head cluster members
2x heavy forwarders (using indexer discovery)
