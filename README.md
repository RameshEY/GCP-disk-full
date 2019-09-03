## Fix GCP Disk full issue - 

### Assumptions 

VM master disk is full 

VM slave is working file 


### Steps 

1. Log in to GCP console

2. Shut down master node 

3. Click on master VM 

4. Click edit on top 

5. Scroll to the boot disk section 

6. Change "When deleting instance" to "Keep Disk" 

7. Click on x next to Keep Disk to detach disk

8. On the Bottom click Save 

9. Go back to GCP compute engine console 

10. click on slave VM

11. Click Edit

12. Search for Additional Disks 

13. Click - Add existing Disks 

14. In the Disk dropdown select the master disk

15. Click Done

16. At bottom of the page click save 

17. Login to slave VM in terminal 

18. Log in as root - `sudo -i` 

19. Execute - `lsblk` 

20. You should now see a new disk - `sdb` 

```
loop0     7:0    0 88.7M  1 loop /snap/core/7396
loop1     7:1    0 60.5M  1 loop /snap/google-cloud-sdk/94
sda       8:0    0   30G  0 disk 
├─sda1    8:1    0 29.9G  0 part /
├─sda14   8:14   0    4M  0 part 
└─sda15   8:15   0  106M  0 part /boot/efi
sdb       8:16   0   30G  0 disk 
├─sdb1    8:17   0 29.9G  0 part 
├─sdb14   8:30   0    4M  0 part 
└─sdb15   8:31   0  106M  0 part 

```

21. `mkdir /hdd`

22. `vi /etc/fstab` 

23. Add the below line at the end - 

```
/dev/sdb1    /hdd    ext4    defaults    0    1
```

24. Save the file 

25. `mount /hdd`

26. `cd /hdd`

27. `cd var/log/jenkins/`

19. `rm *.log` 

20. `cd` 

21. `umount /hdd` 

22. Go back to GCP compute engine console

23. Click on slave VM 

24. Click edit 

25. Search for Additional Disks button 

26. Hover on Existing Disk section 

27. You will get a delete icon 

28. Click on the delete icon 

29. Click Save at the bottom of the page 

30. Go back to compute engine dashboard

31. Click on master VM

32. Click edit on top 

33. Search for Boot Disk section 

34. Add item -> Name - master 

35. Change Device Name from **Custom** to **Based on disk name(default)** in the **Device Name** dropdown

36. Click save

37. Boot VM















