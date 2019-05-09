# Ansible Playbook to provision an Aura Staking Node on a DigitalOcean droplet

This is a playbook to provision an Aura Staking Node on DigitalOcean with Ansible. 

Based off the [sample digital ocean playbook](https://github.com/jasonheecs/ansible-digitalocean-sample-playbook) 


This playbook does the following:
- Spins up a DigitalOcean droplet
- Adds the droplet's IP address to the [ansible inventory file](hosts)
- Setup the swap file
- Installs and setup fail2ban
- Setup Uncomplicated firewall
- Setup the timezone
- Adds a new user account with sudo access
- Adds a public ssh key for the new user account
- Disables password authentication to the droplet
- Deny root login to the droplet
- Installs the UnattendedUpgrades package for automatic security updates
- Installs Docker
- Installs the Aura cli

## Prerequisites

Ansible >= 2.4.0.0
Python >= 3.6

## Usage

1) Clone this repo:
```
git clone https://github.com/eodgooch/aura-staking-node-ansible-playbook
cd aura-staking-node-digital-ocean
```

2) Rename the `group_vars/all/secret.yml.example` file to `group_vars/all/secret.yml` and change the secret variables to your appropriate values.

3) Modify the values in `group_vars/all/main.yml` with your desired values.

4) Run the following:
```
ansible-galaxy install -r requirements.yml
ansible-playbook -i hosts main.yml
```

5) Set up Aura Staking Node

You may want to review the [Medium post video](https://medium.com/idex/idex-launches-aura-staking-learn-how-to-earn-platform-trading-fees-or-increased-trading-rewards-2babf29244a8) 
and review the [staking documentation](https://github.com/AuroraDAO/aurad/blob/master/README.md)

There are manual steps required with this playbook:

- Ensure you have 10000 Aura in a wallet (preferably a cold wallet) for 7 days!
- SSH into Digital Ocean droplet
- run `aura config`
- sign the challenge transaction
- run `aura start`
- wait for your staking node to pull blockchain data
- run `aura logs` to check status of node

## TODOS

- set up an http server that reports current state of the Aura Staker
- automate aura config setup 
- auto-restart on aura staker offline

## License

MIT

