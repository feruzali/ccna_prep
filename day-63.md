---
description: Ansible, Puppet, & Chef
---

# Day 63

**Configuration drift** is when individual changes made over time cause a device's configuration to deviate from the standard/correct configurations as defined by the company. Although each device has a unique part of the configuration (IP addresses, hostname, etc.), most of a device's configuration is usually defined in standard templates by the network engineers of the company. As individual engineers make changes to devices, the configuration of a device can drift away from the standard. Records of these individual changes and their reasons aren't kept. This leads to issues in future. Even without automation tools, it is best to have standard configuration management practices.

**Configuration provisioning** is how configuration changes are applied to devices. This includes configuring new devices too. Configuration management tools like Ansible, Puppet, and Chef allow us to make changes to devices on a mass scale with a fraction of the time/effort. Two essential components are **templates** and **variables**.

<figure><img src=".gitbook/assets/image (173).png" alt="templates and variables demo" width="563"><figcaption></figcaption></figure>

**Configuration management tools** are network automation tools that facilitate the centralized control of large numbers of network devices. They can be used to generate configurations for new devices on a large scale, perform configuration changes on devices, check device configurations for compliance with defined standards, and compare configurations between devices/different versions of configurations on the same device.

### Ansible

Ansible is a configuration management tool owned by Red Hat and written in Python. Ansible is agentless - it doesn't require any special software to run on the managed devices. It uses SSH to connect to devices, make configuration changes, extract information, etc. Ansible uses a **push** model - the Ansible server (Control node) uses SSH to connect to managed devices and push configuration changes to them. After installing Ansible itself, several text files must be created:

* **Playbooks** - blueprints of automation tasks. They outline the logic and actions of the tasks that Ansible should do. Written in YAML.
* **Inventory** - list of the managed devices and their characteristics. Written in INI, YAML, or other formats.
* **Templates** - device's configuration files but specific values for variables aren't provided. Written in Jinja2 format.
* **Variables** - list of variables and values. These values are substituted into the templates to create complete configuration files. Written in YAML.&#x20;

<figure><img src=".gitbook/assets/image (174).png" alt="ansible demo" width="563"><figcaption></figcaption></figure>

### Puppet

Puppet is written in Ruby. Puppet is typically agent-based. Specific software must be installed on the managed devices but not all Cisco devices support a Puppet agent. It can be run agentless, in which a proxy agent runs on an eternal host and uses SSH to connect to the managed devices and communicate with them. The Puppet server is called the **Puppet master**. It uses a **pull** model - clients pull configurations from the Puppet master. Clients use TCP port 8140 for communication. Instead of YAML, Puppet uses proprietary language for files. **Manifest** text file which defines the desired configuration state of a network device and **template** files are required on the Puppet master.

<figure><img src=".gitbook/assets/image (175).png" alt="Puppet demo" width="563"><figcaption></figcaption></figure>

### Chef

Chef is written in Ruby. It is agent-based and not all Cisco devices support it. Chef uses a **pull** model. The server uses TCP port 10002 to send configurations to clients. Files use a **DSL** (Domain-Specific Language) based on Ruby. Text files used by Chef:

* **Resources** - configuration objects managed by Chef.
* **Recipes** - outline the logic and actions of the tasks performed on the resources.
* **Cookbooks** - a set of related recipes grouped.
* **Run-list** - an ordered list of recipes that are run to bring a device to the desired configuration state.&#x20;

<figure><img src=".gitbook/assets/image (176).png" alt="Chef demo" width="563"><figcaption></figcaption></figure>

Here is the chart comparing the three configuration management tools:

<figure><img src=".gitbook/assets/image (177).png" alt="summary" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 63 Flashcards - Ansible, Puppet, Chef.apkg" %}
