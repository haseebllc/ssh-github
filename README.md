# **Setup SSH Key with GitHub Account**

### **Step 1: SSH Key Generation**

```bash
cd ~/.ssh
ssh-keygen -t ed25519 -C "your-email@example.com"
```

If your system doesn't support `ed25519`, you can use `rsa` as an alternative.

```bash
cd ~/.ssh
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

#### **Breakdown:**

- **`ssh-keygen`**: the keygen key generator command.
- **`-t ed25519`** or **`-t rsa`**: specifies the type of key. If your system does not support `ed25519`, use `rsa` with `-b 4096` for a more secure key.
- **`-C "your_email@example.com"`**: adds a comment (usually your email) to help identify the key.

#### **Output Example:**

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (~/.ssh/id_ed25519):
```

1. **For File path:**  
   Press **Enter** to use the default location, or specify a custom path if desired.

2. **Passphrase:**  
   Press **Enter** for no passphrase, or enter a passphrase of your choice.

---

### **Step 2: Start SSH Agent**

The SSH agent is a background process that manages your keys.

```bash
eval "$(ssh-agent -s)"
```

#### **Explanation:**

- **`eval`**: runs the output of the command.
- **`ssh-agent -s`**: starts the SSH agent.

#### **Output Example:**

```
Agent pid 12345
```

---

### **Step 3: Add SSH Key to Agent**

Now, add your SSH key to the agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

If you used `rsa`, replace `id_ed25519` with `id_rsa` in the command.

#### **Output Example:**

```
Identity added: ~/.ssh/id_ed25519
```

---

### **Step 4: Copy Public Key**

To copy your public key, run the following command:

```bash
cat ~/.ssh/id_ed25519.pub
```

If you used `rsa`, replace `id_ed25519.pub` with `id_rsa.pub`.

#### **Output Example:**

```
ssh-ed25519 AAAAC3Nza... your-email@example.com
```

**Copy** the entire key.

---

### **Step 5: Add SSH Key to GitHub**

1. Go to **GitHub** > **Settings** > **SSH and GPG keys**.
2. Click **New SSH Key**.
3. Enter a **Title** (e.g., `my-pc-key`).
4. Paste the copied key into the **Key** box.
5. Click **Add SSH Key**.

---

### **Step 6: Test SSH Connection**

Test if your SSH connection is working correctly by running:

```bash
ssh -T git@github.com
```

#### **Output Example:**

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

### **Step 7: Git Repository Setup**

1. **Initialize a Repository:**

   ```bash
   git init
   ```

2. **Add Remote Repository:**

   ```bash
   git remote add origin git@github.com:username/repo-name.git
   ```

3. **Push Code to GitHub:**

   ```bash
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```
