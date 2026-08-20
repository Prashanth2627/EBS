# EBS
## NAME: Prashanth K
## REG NO: 212223230152

## Aim

To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

---

## Algorithm / Steps

1. Create a new Amazon EBS volume with a size of 1 GiB.
2. Select the same Availability Zone as the EC2 instance.
3. Attach the EBS volume to the EC2 instance using `/dev/sdb`.
4. Connect to the EC2 instance using AWS Systems Manager Session Manager.
5. Check the available storage using `df -h`.
6. Create an `ext3` file system on the EBS volume.
7. Create the `/mnt/data-store` directory.
8. Mount the EBS volume to `/mnt/data-store`.
9. Configure `/etc/fstab` for automatic mounting.
10. Verify that the EBS volume is successfully mounted.
11. Create `file.txt` inside the mounted EBS volume.
12. Verify the contents of the created file.
13. Create an EBS snapshot named `My Snapshot`.
14. Delete `file.txt` from the original EBS volume.
15. Create a new EBS volume from the snapshot.
16. Attach the restored volume to the EC2 instance using `/dev/sdc`.
17. Create the `/mnt/data-store2` directory.
18. Mount the restored volume to `/mnt/data-store2`.
19. Verify that `file.txt` has been successfully restored.

---

## Program

### 1. Check Available Storage

```bash
df -h
```

### 2. Create an ext3 File System

```bash
sudo mkfs -t ext3 /dev/sdb
```

### 3. Create a Mount Directory

```bash
sudo mkdir /mnt/data-store
```

### 4. Mount the EBS Volume

```bash
sudo mount /dev/sdb /mnt/data-store
```

### 5. Configure Automatic Mounting

```bash
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

### 6. View the File System Configuration

```bash
cat /etc/fstab
```

### 7. Verify the Mounted Volume

```bash
df -h
```

### 8. Create a File in the EBS Volume

```bash
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
```

### 9. Read the File

```bash
cat /mnt/data-store/file.txt
```

### 10. Delete the File

```bash
sudo rm /mnt/data-store/file.txt
```

### 11. Verify File Deletion

```bash
ls /mnt/data-store/
```

### 12. Create a Mount Directory for the Restored Volume

```bash
sudo mkdir /mnt/data-store2
```

### 13. Mount the Restored EBS Volume

```bash
sudo mount /dev/sdc /mnt/data-store2
```

### 14. Verify Snapshot Restoration

```bash
ls /mnt/data-store2/
```

Expected output:

```text
file.txt
```

---

## Outputs
<img width="1905" height="972" alt="Screenshot 2026-07-28 083310" src="https://github.com/user-attachments/assets/ed7a4b4e-06cc-4704-86ca-1320a22ac8e4" />
<img width="1911" height="860" alt="Screenshot 2026-07-28 090922" src="https://github.com/user-attachments/assets/51435ce6-62c8-4623-9b48-6008f093e7d3" />

<img width="946" height="302" alt="image" src="https://github.com/user-attachments/assets/b7f38a97-364c-4658-a06f-8c000644ac13" />

<img width="947" height="352" alt="image" src="https://github.com/user-attachments/assets/c6f1a20f-e64e-4fec-9999-74c98faae254" />

<img width="942" height="293" alt="image" src="https://github.com/user-attachments/assets/4501e55a-b46d-4c48-8807-78edade77df5" />

<img width="1911" height="860" alt="Screenshot 2026-07-28 090922" src="https://github.com/user-attachments/assets/b6cba444-4cc2-49d1-bd08-d7fe44b1749a" />

<img width="1917" height="862" alt="Screenshot 2026-07-28 090934" src="https://github.com/user-attachments/assets/448d56ee-ece4-4ff9-9a54-2b89a5fdf49b" />

<img width="1917" height="880" alt="Screenshot 2026-07-28 091108" src="https://github.com/user-attachments/assets/e593968f-74b3-44a0-8f7c-717a817d5716" />

<img width="1537" height="545" alt="Screenshot 2026-07-28 093332" src="https://github.com/user-attachments/assets/fe237408-45ec-4b56-8455-cd836a9847ff" />









## Result
Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an ext3 file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted file.txt was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.

