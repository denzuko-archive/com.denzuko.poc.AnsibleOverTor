Ansible tor hidden node deployment
=================================

(C)2015 Dwight A. Spencer

Intro
=====

As part of a research project into distributed computing, I needed a way to 
manage the grid no matter if it was deployed to AWS, OpenStack, COTS PC, Pi 
Cluster, or any other system.

Since I plan on deploying this within the spirit of Beowulf clustering and a few
AWS free tier tiny instances. I chose to use ansible to manage nodes and 
distribute the batch processes. However given that both mDNS and DNS would not 
always available the choice of using Tor hidden nodes as a way of accessing
the grid proved to be invaluable.

Thus, this project is born to document the process to set up a cluster of hidden
nodes and manage them via ansible.

Goals
=====

  - Create a small computational grid accessable only via ssh with pubkeys
  - Allow only darknet access to nodes
  - Administrate and distribute batch jobs in parallel across the grid
  - Administrate and distribute batch jobs in serial across individual nodes
  - Must be simple enough that this can run on any Virtualized Hosting, COTS PC,
    and/or a cluster of Raspberry Pi machines.

Installation
============

Installation is very easy from the controlling node and the end
nodes. Trystack was choisen for the test but can just as easily been done
thorough EC2. The process of launching instances is documented else where
and in future revisions may include both the cli and gui versions of starting
for both EC2 and OpenStack.

First to start with is ansible. From a command line execute:

  easy_install pip && pip install ansible

Once this step has completed execute:

  git clone https://github.com/denzuko/ansible-tor && cd ansible-tor
  ansible-playbook main.yml -i hosts stack

Configuration
=============

Be sure to list the IP addresses of each node to install tor on. From there use
torify/torsocks with ansible-playbook to administrate and interact with nodes via
their hidden service name.
