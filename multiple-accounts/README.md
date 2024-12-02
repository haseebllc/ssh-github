# **Setup SSH Keys for Multiple GitHub Accounts**

## **Step 1: Generate Separate SSH Keys for Each Account**

It's important to generate a separate SSH key for each GitHub account.

### **1. Generate the First Key:**

open git-bash if you havn't download and install git

```bash
cd ~/.ssh
ssh-keygen -t ed25519 -C "first-email@example.com"
```

- When prompted:

  ```
  Enter file in which to save the key (~/.ssh/id_ed25519):
  ```

  Provide a custom file name to keep the keys separate:

  ```bash
  ~/.ssh/github1
  ```

- **Passphrase**: You can set a passphrase or leave it blank by pressing **Enter**.

---

### **2. Generate the Second Key:**

```bash
ssh-keygen -t ed25519 -C "second-email@example.com"
```

- When prompted:
  ```bash
  Enter file in which to save the key (~/.ssh/id_ed25519):
  ```
  Provide a different custom file name:
  ```bash
  ~/.ssh/github2
  ```

---

## **Step 2: Start the SSH Agent and Add the Keys**

### **1. Start the SSH Agent:**

```bash
eval "$(ssh-agent -s)"
```

The output will look like:

```
Agent pid 12345
```

---

### **2. Add the First Key:**

```bash
ssh-add ~/.ssh/github1
```

Output:

```
Identity added: ~/.ssh/github1
```

---

### **3. Add the Second Key:**

```bash
ssh-add ~/.ssh/github2
```

Output:

```
Identity added: ~/.ssh/github2
```

---

## **Step 3: Add Public Keys to GitHub Accounts**

### **1. Copy the First Key:**

```bash
cat ~/.ssh/github1.pub
```

- The output will look like:

  ```
  ssh-ed25519 AAAAC3Nza... first-email@example.com
  ```

- **Copy** the entire key.

#### **Add the First Key to GitHub Account 1:**

1. Open **GitHub** > **Settings** > **SSH and GPG keys**.
2. Click **New SSH Key**.
3. Enter a **Title** (e.g., "Personal Laptop Key").
4. Paste the copied key into the **Key** box.
5. Click **Add SSH Key**.

---

### **2. Copy the Second Key:**

```bash
cat ~/.ssh/github2.pub
```

- The output will look like:

  ```
  ssh-ed25519 AAAAC3Nza... second-email@example.com
  ```

- **Copy** the entire key.

#### **Add the Second Key to GitHub Account 2:**

1. Open the **second GitHub account** > **Settings** > **SSH and GPG keys**.
2. Click **New SSH Key**.
3. Enter a **Title** (e.g., "Work Laptop Key").
4. Paste the copied key into the **Key** box.
5. Click **Add SSH Key**.

---

## **Step 4: Manage Multiple Keys Using the SSH Config File**

We need to create a **config** file that tells SSH which key to use for which account.

### **Create the SSH Config File:**

```bash
nano ~/.ssh/config
```

recursivly : If the file doesn’t exist, this command will create a new one.

---

### **Content for the Config File:**

```bash
# First GitHub Account
Host github1
  HostName github.com
  User git
  IdentityFile ~/.ssh/github1

# Second GitHub Account
Host github2
  HostName github.com
  User git
  IdentityFile ~/.ssh/github2
```

#### **Explanation:**

- **`Host github1`** and **`Host github2`**: These are aliases. You can use any name you like.
- **`IdentityFile`**: This specifies which SSH key to use.

To save the file:

- Press **CTRL + O** to save.
- Press **CTRL + X** to exit.

---

## **Step 5: Use the Correct Key for Git Repositories**

### **1. For github1 acc Repository:**

If you want to set up a repository for your github1 GitHub account:

```bash
git remote set-url origin git@github1:username/repo1.git
```

---

### **2. For github2 acc Repository:**

If you want to set up a repository for your github2 account:

```bash
git remote set-url origin git@github2:username/repo2.git
```

---

## **Step 6: Test the SSH Connection**

### **1. Test for github1:**

```bash
ssh -T git@github1
```

If everything is set up correctly, you should see this message:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```
