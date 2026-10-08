# Linux Security Basics – Veda Technology Internship (Day 19)

## Objective
Understand basic Linux security controls: users, groups, permissions and ownership.

## Tools Used
- Linux (Kali Linux)
- Terminal

## 1. Users and Groups

| Command | Purpose |
|---|---|
| `whoami` | Show the current user |
| `id` | Show UID, GID and group memberships |
| `cat /etc/passwd` | List user accounts |
| `cat /etc/group` | List groups |
| `sudo adduser testuser` | Create a new user |
| `sudo groupadd devteam` | Create a new group |
| `sudo usermod -aG devteam testuser` | Add a user to a group |

## 2. File Permissions (read, write, execute)

Running `ls -l` shows output like:

```
-rwxr-xr-- 1 ritu devteam 1024 Oct 08 notes.sh
```

| Part | Meaning |
|---|---|
| `-` | File type (`d` = directory) |
| `rwx` | Owner permissions |
| `r-x` | Group permissions |
| `r--` | Others' permissions |

| Permission | Letter | Number | On a file | On a directory |
|---|---|---|---|---|
| Read | r | 4 | View contents | List contents |
| Write | w | 2 | Modify contents | Create/delete files |
| Execute | x | 1 | Run as program | Enter (cd) |

## 3. chmod – Changing Permissions

```bash
chmod 755 script.sh      # rwxr-xr-x
chmod 644 notes.txt      # rw-r--r--
chmod 600 secret.txt     # rw------- (owner only)
chmod u+x script.sh      # add execute for owner
chmod go-w notes.txt     # remove write for group and others
```

## 4. Ownership – chown and chgrp

```bash
sudo chown testuser file.txt            # change owner
sudo chown testuser:devteam file.txt    # change owner and group
sudo chgrp devteam file.txt             # change group only
```

## 5. Practical Exercise

```bash
mkdir lab && cd lab
echo "confidential" > secret.txt
ls -l secret.txt                 # check default permissions
chmod 600 secret.txt             # restrict to owner only
ls -l secret.txt                 # verify
sudo chown testuser secret.txt   # change ownership
su testuser -c "cat secret.txt"  # test access as the new owner
```

### Screenshots


![ls -l](screenshots/ls-l.png)




![chmod](screenshots/chmod.png)




![chown](screenshots/chown.png)



## 6. Interview Questions

**What is chmod?**
A command that changes the read, write and execute permissions of files and directories, using symbolic (`u+x`) or numeric (`755`) modes.

**What is file ownership?**
Every file has an owner (user) and a group. Permissions are applied separately to the owner, the group and everyone else. `chown` and `chgrp` change them.

**What is least privilege?**
A security principle: give users and processes only the minimum permissions they need to do their job, which limits the damage from mistakes or compromise.

## 7. Security Best Practices
- Avoid `chmod 777`; it gives everyone full access.
- Keep sensitive files (keys, passwords) at `600`.
- Use `sudo` only when needed; avoid working as root.
- Regularly review users and groups.
- Remove unused accounts.

## Conclusion
Linux controls access through users, groups, ownership and permissions. Using `chmod` and `chown` correctly, along with the principle of least privilege, is a basic and important part of system hardening.

## Author
Ritu Raj – Cyber Security Intern, Veda Technology
