# Lab 07 Challenge: Environment Audit and Ping Block

## Job 1: Environment Audit

**Commands used:**

```bash
printenv | grep '^PATH='
printenv | grep '^LANG='
printenv | grep '^PWD='
```

**Results:**
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/shehzadimantasha
LANG=en_US.UTF-8
PWD=/home/shehzadimantasha/lab07-env-ssh-firewall


## Job 2: Temporary Student Variables

**Commands used:**

```bash
export STUDENT_NAME="Your Name"
export STUDENT_ROLL_NUMBER="Your Roll Number"
export STUDENT_SEMESTER="5th Semester"

printenv | grep '^STUDENT_'
```

**Result:**

All three student variables were displayed successfully.

After logging out and connecting again, I used:

```bash
echo "$STUDENT_NAME"
printenv | grep '^STUDENT_'
```

The variables were no longer available because they were temporary and were not saved in a configuration file.

## Job 3: Permanent Student Variables

**File edited:** ~/.bashrc

**Commands used:**

```bash
vim ~/.bashrc
source ~/.bashrc
printenv | grep '^STUDENT_'
```

The following variables were added to `.bashrc`:

```bash
export STUDENT_NAME="Mantasha Shehzadi"
export STUDENT_ROLL_NUMBER="FA24B1-SE-033"
export STUDENT_SEMESTER="5th Semester"
```

After logging out and logging in again, all three variables were displayed successfully.

This confirmed that the variables were permanent.

## Job 4: Block and Allow Ping

**Backup command:**

```bash
sudo cp /etc/ufw/before.rules ~/before.rules.backup
```

**File edited:**

```bash
sudo vim /etc/ufw/before.rules
```

The incoming echo-request rule was changed from ACCEPT to DROP.

**Firewall reload command:**

```bash
sudo ufw reload
```

**Command used to verify blocked ping:**

```bash
sudo iptables -S ufw-before-input | grep "icmp-type 8"
```

Result: The rule ended with -j DROP, confirming that incoming ping requests were blocked.

**Restoration:**

The rule was changed back from DROP to ACCEPT.

```bash
sudo ufw reload
sudo iptables -S ufw-before-input | grep "icmp-type 8"
```

Result: The rule ended with -j ACCEPT, confirming that ping was allowed again.

**Conclusion:**

All four challenge tasks were completed successfully. Environment variables were created and made permanent, and the firewall was configured to block and then allow incoming ping requests.
