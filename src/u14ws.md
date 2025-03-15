<!-- u14ws.md -->

<div class="flex-container">
        <img src="https://github.com/ProfessionalLinuxUsersGroup/img/blob/main/Assets/Logos/ProLUG_Round_Transparent_LOGO.png?raw=true" width="64" height="64"></img>
    <p>
        <h1>Unit 14 Worksheet: Ansible Automation</h1>
    </p>
</div>

## Introduction

This **Unit 14 Worksheet** is designed to help you engage with the topics presented in our Ansible Automation discussions and materials. You’ll reflect on inventory management, ad-hoc commands, playbooks, and more.

---

## Unit 14 Recording

<iframe
    style="width: 100%; height: 100%; border: none;
    aspect-ratio: 16/9; border-radius: 1rem; background:black"
    src="https://www.youtube.com/embed/-tk73llgt3E?list=PLyuZ_vuAWmprPIqsG11yoUG49Z5dE5TDu&index=14"
    title="Unit 14: Ansible Automation"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    referrerpolicy="strict-origin-when-cross-origin"
    allowfullscreen>
</iframe>

*(If the embedded video does not display, please use this direct link: [Unit 14 Recording](https://www.youtube.com/watch?v=-tk73llgt3E&list=PLyuZ_vuAWmprPIqsG11yoUG49Z5dE5TDu&index=14))*

---

## Discussion Questions

### Unit 14 Discussion Post 1

Refer back to your previous environmental scans (like in Unit 5) and consider how Ansible can be used to maintain consistent configurations.

1. Make an **inventory** of your servers, grouped any way you like.
2. What **inventory format** did you choose (INI, YAML, etc.)? Why?
3. What additional information might you add to your inventory in the future?

**Relevant Reading**:  
[Ansible Inventory Guide](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)

---

### Unit 14 Discussion Post 2

You are noticing configuration drift on servers, and you want a way to validate configurations daily. Research ways Ansible can help by generating daily reports on your environment.

1. Share at least one method or module you would use.
2. How would you schedule or automate these checks (e.g., cronjob, Jenkins, AWX, etc.)?
3. Post relevant code snippets or references.

**Tip**: [KillerCoda’s Ansible Labs](https://killercoda.com/het-tanis/course/Ansible-Labs)  
**Optional Webhook**: [Discord Webhook Example](https://discord.com/api/webhooks/1317659221604433951/uyKpuq8fNNNSEyCra4n33PakIBk-XtTn1WrwTpHs9BcgkIu7URPV_Gd5HJCRX0_EJVUT)

---

### Unit 14 Discussion Post 3

Using the Ansible **git** module, pull down the HPC_Deploy repo from GitHub:

- [https://github.com/het-tanis/HPC_Deploy.git](https://github.com/het-tanis/HPC_Deploy.git)

Discuss:

1. How is the repository structured?
2. What **roles** are available, and how do they differ from basic tasks?
3. How does the repository organize playbooks and roles?

---

## Terminology

- **Automation**: The technique of making an apparatus, process, or system operate automatically.
- **Consistency**: Ensuring that all managed nodes share uniform configurations and policies.
- **Dev/Ops**: A collaborative approach between Development and Operations teams focused on automation and integration.
- **Timeliness**: The capability of completing configuration tasks or deployments quickly.
- **Git**: A version control system for tracking changes in files and coordinating work.
- **Repository**: A central location where data is stored and maintained.
- **Ad-hoc Commands**: One-off Ansible commands run without a formal playbook, often used for quick checks.
- **Playbook**: A YAML file of Ansible tasks describing desired configurations or operations.
- **Task**: A single action executed by Ansible, typically calling a module.
- **Role**: A modular way to group tasks, variables, and other resources to streamline reusability.
- **SSH**: Secure Shell; the protocol typically used by Ansible to communicate with remote hosts.
- **WinRM**: Windows Remote Management; a protocol for managing Windows environments.

---

## Notes During Lecture/Class

Use this section to jot down personal notes, key insights, or additional resources:

