<!-- u14intro.md -->

<div class="flex-container">
        <img src="https://github.com/ProfessionalLinuxUsersGroup/img/blob/main/Assets/Logos/ProLUG_Round_Transparent_LOGO.png?raw=true" width="64" height="64"></img>
    <p>
        <h1>Unit 14 Intro: Ansible Automation</h1>
    </p>
</div>

## Introduction

Welcome to **Unit 14** of the *Professional Linux Users Group System Administration for the Enterprise* course. In this chapter, we dive into **Ansible Automation**, exploring how to leverage Ansible to configure, manage, and deploy changes across multiple Linux systems quickly and consistently.

### What is Ansible?

Ansible is an open-source IT automation engine that automates tasks such as software provisioning, configuration management, and application deployment. It uses a simple, human-readable language (YAML) and SSH (or WinRM on Windows) to manage and configure nodes without needing a dedicated client or agent.

### Goals and Outcomes

- Understand basic Ansible concepts (inventory, modules, playbooks, tasks, roles).
- Implement automation for routine administrative tasks.
- Use Ansible ad-hoc commands for quick checks or single tasks.
- Develop playbooks to enforce configurations systematically.

### Key Terms

- **Playbook**: A structured file (in YAML) that describes the tasks to run on hosts.
- **Inventory**: A list of hosts or groups of hosts, typically stored in a file.
- **Module**: A reusable script that Ansible runs on the target system to perform a task.
- **Task**: A call to a module in a playbook, specifying what to do on a target system.
- **Role**: A way to group related tasks, variables, templates, and files in a standardized format.

---

## Resources / Important Links

- [Ansible Official Documentation](https://docs.ansible.com/)
- [KillerCoda’s Ansible Labs](https://killercoda.com/het-tanis/course/Ansible-Labs)
- [GitHub HPC_Deploy Repository](https://github.com/het-tanis/HPC_Deploy.git)
- [ProLUG Discord Community](https://discord.gg/k3nSeJKtqN) *(example link – use your own if preferred)*

---

## Why Ansible?

1. **Agentless Operation**: No extra daemons or agents are needed on remote hosts.
2. **Simple Language**: YAML-based playbooks are easy to read and write.
3. **Idempotency**: Running the same playbook multiple times leads to the same result.
4. **Scalability**: Manage any number of systems from small labs to large-scale enterprise environments.

---

## Next Steps

Proceed to the [Worksheet](./u14ws.md) to solidify your understanding with guided questions and discussions. Then, explore the hands-on [Lab](./u14lab.md) for practical experience. Finally, check out the [Bonus Material](./u14bonus.md) for more advanced tips and extended learning opportunities.
