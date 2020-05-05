# Documentation and Usage
See the project's [wiki](https://github.com/scottgoetz/ansible/wiki) for documentation and usage examples


# Current Playbooks
#### secureSetup.yml
  * Initial firewall rules
  * Locks down SSH
  * Implements SSH Keys
  * Create unprivileged users
  * Updates OS and packages
#### offensiveTools.yml
  * Installs various tools, most from source
  * Nessus, Metasploit, GoPhish, CobaltStrike, Impacket, CrackMapExec, Responder, EyeWitness
  * Additional firewall rules
#### webRedirector.yml 
  * Installs Apache
  * Generates LetsEncrypt SSL certs
  * Configures Apache mod_rewrite
  * Additional firewall rules
#### mailServer.yml
  * Installs and configures Postfix
  * Removes mail client IOCs from mail Headers
  * SendGrid/Mailgun variants
  * Additional firewall rules
#### goPhish.yml
  * Builds from source
  * Changes default ports
  * Additional firewall rules
#### ghostPhish.yml
  * IOCs removed from source code (ghostPhish.yml)
  * Same as goPhish.yml
