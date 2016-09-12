UNMAINTAINED - ufw
========

# No longer updated
Use [aspects_iptables](https://github.com/LaneCommunityCollege/aspects_iptables)

A simple role that manages the ufw firewall via ufw's app profile feature.


Role Variables
--------------

TODO: Refine this section.
Set the default ufw firewall policy. See the ufw module documentation for possible values.
aspects_aspects_ufw_default_policy:
  default:
    state: "enabled"
    policy: "deny"

Set the rules for existing ufw app profiles in /etc/ufw/applications.d
See ufw's man page and other ufw documentation for more information.
aspects_aspects_ufw_apps:
  OpenSSH:
    name: "OpenSSH"
    rule: "allow"
    enabled: true
  Apache:
    name: "Apache Full"
    rule: "allow"
    enabled: true

Create custom ufw app profiles. These are set in /etc/ufw/applications.d/ansible_aspects_ufw_custom_apps
If you wish to keep an app out of the file, then set enabled to false.
See https://wiki.archlinux.org/index.php/Uncomplicated_Firewall#Adding_other_applications for help on creating new apps.
aspects_ufw_custom_apps:
  david:
    enabled: true
    rule: "reject"
    name: "DAVID"
    description: "test description"
    ports: '22220:22240/tcp|44444/tcp'

Example Playbook
-------------------------


    - hosts: servers
      roles:
         - ufw
      vars:
        aspects_ufw_default_policy:
          default:
            state: "enabled"
            policy: "deny"
        aspects_ufw_apps:
          OpenSSH:
            name: "OpenSSH"
            rule: "allow"
            enabled: true
          Apache:
            name: "Apache Full"
            rule: "allow"
            enabled: true
        aspects_ufw_custom_apps:
          randomapp:
            enabled: true
            rule: "reject"
            name: "Random App"
            description: "A random app with very odd ports."
            ports: '22220:22240/tcp|44444/tcp|123456/udp'

License
-------

MIT
