# hello
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
      nodePort: 30001 
  type: NodePort   


apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: aymanhussain21/eeman:latest
          ports:
            - containerPort: 3000
  


# Use the official Node.js image as a base
FROM node:20


WORKDIR /app

COPY package*.json ./

# Install dependencies
RUN npm install
# If you use yarn:
# RUN yarn install

# Copy the rest of the application code
COPY . .

# Expose the port your app runs on
EXPOSE 3000

# Command to run your app
CMD ["node", "index.js"]
# If using Next.js:
# CMD ["npm", "run", "dev"]


Here’s the **simple and complete guide** to connect your **new laptop** to **GitHub** and start pushing code.

---

# ✅ **1. Install Git**

Check if Git is installed:

```bash
git --version
```

If not installed:

### **Ubuntu**

```bash
sudo apt update
sudo apt install git
```

### **Windows**

Install Git from: [https://git-scm.com/downloads](https://git-scm.com/downloads)

---

# ✅ **2. Configure Git (your identity)**

You only do this **once per laptop**:

```bash
git config --global user.name "Your Name"
git config --global user.email "your_github_email@example.com"
```

Make sure the email is the same as your GitHub account email.

---

# ✅ **3. Create SSH Key (Recommended Way)**

This lets you push code **without entering password every time**.

Run:

```bash
ssh-keygen -t ed25519 -C "your_github_email@example.com"
```

Press Enter for all prompts → default is fine.

---

# ✅ **4. Add SSH Key to SSH Agent**

Start ssh-agent:

```bash
eval "$(ssh-agent -s)"
```

Add your new key:

```bash
ssh-add ~/.ssh/id_ed25519
```

---

# ✅ **5. Add Key to GitHub**

Now copy the key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the whole output.

Go to:

**GitHub → Settings → SSH and GPG Keys → New SSH Key**

Paste the key → Save.

---

# ⭐ **6. Test the Connection**

Check if your laptop is authenticated with GitHub:

```bash
ssh -T git@github.com
```

If successful, you'll see:

```
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

---

# ✅ **7. Clone or Push Repository**

### **If you want to clone an existing repo:**

```bash
git clone git@github.com:your-username/your-repo.git
```

### **If you have a local project and want to push it to GitHub:**

Inside your project folder:

```bash
git init
git remote add origin git@github.com:your-username/your-repo.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

(If your repo uses `master`, use that instead of `main`.)

---

# 🎉 Done!

Now your laptop is fully connected to GitHub using SSH.
You can push, pull, clone without entering your password.

If you want, I can help you:
✔ create SSH key
✔ fix Git errors
✔ push a project step-by-step

Just tell me what step you're stuck on!

