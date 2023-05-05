# Kerberos_ssh
This project is about kerberos authentiication using ssh

First we will type the command `hostname -I`  to get the IP adress
![Screenshot from 2023-05-03 20-41-44](https://user-images.githubusercontent.com/94203047/236062619-f717eaf6-9ccd-498f-9c8f-6b9244b5fe6f.png)

 We add that IP adress and we declare it as a kdc 
![Screenshot from 2023-05-03 20-43-41](https://user-images.githubusercontent.com/94203047/236064538-6fbbaaaa-e0fa-4640-8b24-ece4372107c2.png)

BY closing and ropening the termilnal 
![Screenshot from 2023-05-03 20-46-30](https://user-images.githubusercontent.com/94203047/236066365-1746b7f6-6295-4622-b72c-5ec508e7adb8.png)

## Kerberos installation 
After typing this command 
`sudo apt install krb5-kdc krb5-admin-server krb5-config`
![Screenshot from 2023-05-03 20-54-58](https://user-images.githubusercontent.com/94203047/236565134-9f2d63a1-04cd-4ee1-9370-5c8a953278a5.png)
We net up realm name , Kerberos server name and admin server name

After the set up , this will appear 
![Screenshot from 2023-05-03 20-56-17](https://user-images.githubusercontent.com/94203047/236565802-0c2621a4-1b87-4523-98f0-b8112cd8a27e.png)

 ## Kerberos configuration
 ### Initialising base realm 
 `krb5_newrealm`
![Screenshot from 2023-05-03 21-49-34](https://user-images.githubusercontent.com/94203047/236566216-3be955e3-2c18-40f2-bb06-9c2464299b69.png)
![Screenshot from 2023-05-03 21-51-40](https://user-images.githubusercontent.com/94203047/236566777-14d482ae-a877-4cf4-9e16-2612dd556d00.png)

### Change kadm5.acl
`sudo nano /etc/krb5kdc/kadm5.acl`
![Screenshot from 2023-05-03 21-52-00](https://user-images.githubusercontent.com/94203047/236566854-9b0c956e-0702-4a0b-b63f-3d31cd64e838.png)

### Open kadmin local 
`kadm.local`
![Screenshot from 2023-05-03 21-53-36](https://user-images.githubusercontent.com/94203047/236567507-cbcd01d5-4a46-4e39-b18e-3683980377c6.png)

### Add principals
`addprinc {name of principal}`
![Screenshot from 2023-05-03 21-57-43](https://user-images.githubusercontent.com/94203047/236567862-9085298c-a9dd-4a20-95a4-ecdfc17b9cb0.png)

### Add kadmin/admin and kadmin/changepw to keytab
`ktadd -k /etc/krb5kdc/kadm5.keytab kadmin/admin`
![Screenshot from 2023-05-03 22-10-38](https://user-images.githubusercontent.com/94203047/236568769-573698aa-4244-414a-8ae6-ba75ad382939.png)

### Add host principal
`addprinc -randkey host/kdc`
### Add keytab to host pricipal 
`ktadd host/kdc`
![Screenshot from 2023-05-03 22-11-27](https://user-images.githubusercontent.com/94203047/236569335-411760ee-8981-4ad2-97cc-6d08057d39dc.png)

After finishing the kerberos configuration we will tap this command to restart the server 
`sudo systemctl restart krb5-admin-server`

## Configuration open ssh

### Now we are going to change sshd_config to allow GSSAPI
`sudo nano /etc/ssh/sshd_config`
you need to make sure that GSSAPIAuthentication and GSSAPICleanupCredentials are enabled
![Screenshot from 2023-05-03 22-14-59](https://user-images.githubusercontent.com/94203047/236571402-6b99de36-2f1c-4df0-a2c8-4721311c334c.png)

### We will do the same for ssh_config 
![Screenshot from 2023-05-03 22-16-46](https://user-images.githubusercontent.com/94203047/236571902-0518b427-65a4-45ba-8a52-1f4fee0bd4c4.png)

Then we restart open ssh service 
`sudo systemctl restart ssh`

## Test
![Screenshot from 2023-05-03 22-40-35](https://user-images.githubusercontent.com/94203047/236572319-ef59d5a0-0f64-4901-b7e6-03d637fcd86e.png)


