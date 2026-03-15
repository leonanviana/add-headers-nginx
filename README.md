# add-headers-nginx

> 🇧🇷 [Português](#português) | 🇺🇸 [English](#english)

![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-000000?style=for-the-badge&logo=ansible&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Security](https://img.shields.io/badge/DevSecOps-000000?style=for-the-badge&logo=hackthebox&logoColor=white)

---

## Português

Playbooks Ansible para adição e remoção de security headers no Nginx de forma automatizada e idempotente.

### Por que security headers?

Security headers protegem aplicações web contra ataques como XSS, clickjacking e MIME sniffing. São exigidos em auditorias de segurança e compliance (OWASP, PCI-DSS).

### Estrutura

```
add-headers-nginx/
├── nginx.conf                      # Exemplo de configuração Nginx
└── playbooks/
    ├── headers_nginx.txt           # Headers a serem inseridos
    ├── add_headers_nginx.yml       # Playbook para adicionar headers
    └── remove_headers_nginx.yml    # Playbook para remover headers
```

### Pré-requisitos

- Ansible instalado
- Acesso sudo ao host alvo
- Nginx instalado

### Como usar

**1. Configure os paths no playbook conforme seu ambiente:**

```yaml
vars:
  PATH_ADD_HEADERS_TXT: /seu/path/playbooks/headers_nginx.txt
  PATH_NGINX_CONF: /etc/nginx/nginx.conf
```

**2. Adicionar headers:**

```bash
ansible-playbook playbooks/add_headers_nginx.yml
```

**3. Remover headers:**

```bash
ansible-playbook playbooks/remove_headers_nginx.yml
```

### O que o playbook faz

1. Faz backup do `nginx.conf` (duas cópias de segurança)
2. Remove headers existentes para evitar duplicação
3. Injeta os novos headers após a diretiva `gzip_vary on`
4. Mantém o arquivo limpo (sem linhas em branco desnecessárias)

> **Nota:** O restart do Nginx está comentado no playbook. Descomente a task `Restart Nginx` para aplicar as mudanças automaticamente.

---

## English

Ansible playbooks for automated and idempotent addition and removal of security headers in Nginx.

### Why security headers?

Security headers protect web applications against attacks like XSS, clickjacking and MIME sniffing. They are required in security and compliance audits (OWASP, PCI-DSS).

### Structure

```
add-headers-nginx/
├── nginx.conf                      # Nginx configuration example
└── playbooks/
    ├── headers_nginx.txt           # Headers to be inserted
    ├── add_headers_nginx.yml       # Playbook to add headers
    └── remove_headers_nginx.yml    # Playbook to remove headers
```

### Prerequisites

- Ansible installed
- Sudo access on target host
- Nginx installed

### Usage

**1. Configure paths in the playbook for your environment:**

```yaml
vars:
  PATH_ADD_HEADERS_TXT: /your/path/playbooks/headers_nginx.txt
  PATH_NGINX_CONF: /etc/nginx/nginx.conf
```

**2. Add headers:**

```bash
ansible-playbook playbooks/add_headers_nginx.yml
```

**3. Remove headers:**

```bash
ansible-playbook playbooks/remove_headers_nginx.yml
```

### What the playbook does

1. Backs up `nginx.conf` (two backup copies)
2. Removes existing headers to prevent duplication
3. Injects new headers after the `gzip_vary on` directive
4. Keeps the file clean (no unnecessary blank lines)

> **Note:** The Nginx restart is commented out in the playbook. Uncomment the `Restart Nginx` task to apply changes automatically.
