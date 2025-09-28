# Digital-banking-infra
Load Balancer, Application Gateway, Bastion, HTTPS encryption, etc
digital-banking-infra/
│── README.md
│── main.tf
│── variables.tf
│── outputs.tf
│── bastion.tf
│── loadbalancer.tf
│── application_gateway.tf
│── security.tf

# 🚀 Secure & Scalable Digital Banking Infrastructure (Demo Project)

This repository showcases a **DevOps Project** inspired by my experience at **Unity Small Finance Bank**, where I worked on improving **Mobile & Net Banking applications** by making them more **secure, scalable, and highly available**.  

---

## 🔑 Features Implemented
- 🌐 **Application Gateway + Web Application Firewall (WAF)** for secure traffic management.  
- ⚖️ **Load Balancer** to ensure high availability and intelligent routing.  
- 🛡️ **Bastion Host** for controlled access to production servers.  
- 🔐 **HTTPS/TLS Encryption** for secure customer transactions.  
- 👥 **RBAC & Secure Authentication** with encrypted usernames and passwords.  
- ⚡ Automated deployment pipelines with **CI/CD**.  
- 📊 Monitoring using **Prometheus + Grafana**.  

---

## 📂 Repository Structure
- `main.tf` → Core infrastructure setup  
- `bastion.tf` → Bastion host config  
- `loadbalancer.tf` → Load balancer config  
- `application_gateway.tf` → WAF + Application Gateway  
- `security.tf` → HTTPS/TLS + firewall rules  
- `variables.tf` → Input variables  
- `outputs.tf` → Output values  

---


        Client
           |
           v
 Application Gateway (WAF)
           |
           v
     Load Balancer
           |
           v
     Web/App Servers
           |
           +--> Bastion Host (Admin Access)
           |
           +--> HTTPS/TLS Encryption


## 🚀 How to Use
1. Clone this repo  
   ```bash
   git clone https://github.com/<your-username>/digital-banking-infra.git
   cd digital-banking-infra

   Client ---> Application Gateway (WAF) ---> Load Balancer ---> Web/App Servers
                  |                                     
                  +---> Bastion Host (Admin Access)
                  +---> HTTPS/TLS Encryption


---

## ⚙️ Example Terraform Snippet (`loadbalancer.tf`)  

```hcl
resource "azurerm_lb" "banking_lb" {
  name                = "banking-lb"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
  sku                 = "Standard"

  frontend_ip_configuration {
    name                 = "PublicIPAddress"
    public_ip_address_id = azurerm_public_ip.lb_public_ip.id
  }
}

resource "azurerm_public_ip" "lb_public_ip" {
  name                = "lb-public-ip"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
  allocation_method   = "Static"
  sku                 = "Standard"
}

