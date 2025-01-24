## **Allowing GitHub and GitLab Webhooks with UFW** for Jenkins port or 8080

Webhooks allow GitHub and GitLab to notify your server about events like code pushes. To let them through the firewall, you need to allow their specific IP ranges on the port your server is listening to (e.g., `8080`).

### **Commands to Allow GitHub Webhooks**

Run these commands to allow GitHub's webhook IP ranges:


```bash

sudo ufw allow from 192.30.252.0/22 to any port 8080 proto tcp
sudo ufw allow from 185.199.108.0/22 to any port 8080 proto tcp
sudo ufw allow from 140.82.112.0/20 to any port 8080 proto tcp
sudo ufw allow from 143.55.64.0/20 to any port 8080 proto tcp`
```

### **Commands to Allow GitLab Webhooks**

Run these commands to allow GitLab's webhook IP ranges:


```bash

sudo ufw allow from 34.74.90.64/28 to any port 8080 proto tcp 
sudo ufw allow from 34.74.226.0/24 to any port 8080 proto tcp`
```

### **Final Steps**

1. **Enable UFW (if not already enabled):**
    
```bash
sudo ufw enable
```
    
2. **Verify the Rules:**  
    Check the active rules with:

```bash
sudo ufw status   
```
---

Now, your server is ready to receive webhook traffic securely from GitHub and GitLab!