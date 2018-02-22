

In this class, we will use the GENI testbed to run networking experiments. This assigment teaches you how to use GENI to set up and access a basic topology of two hosts connected by a router.

After completing this assignment, you should:

* Be able to log in and create a slice using GENI Portal and Jacks.
* Know how to use GENI to design a simple network, generate an RSpec, and reserve resources.
* Understand GENI terms.



## Join our GENI project (one-time setup)

To use GENI, you must create a GENI account and join a project. This involves a one-time account setup.

First, go to [https://portal.geni.net/](https://portal.geni.net/) and click on "Use GENI".

On the next screen, you will be prompted to choose an Identity Provider. Choose "New York University" and press "Continue". Log in with your NYU NetID.

Review the policies on the next page, check both boxes, and click "Activate" to log in to the portal.

GENI users are organized into projects (read more [here](http://groups.geni.net/geni/wiki/GENIConcepts#Project).) Anyone can create an account on GENI, but unless you are part of a project (supervised by a responsible Project Lead), you won't be able to access any GENI resources. For this course, we will work in the EL9383-NYU-S18 project. I am the Project Lead for this project; the students in our class will be Project Members.

In the portal, [join the project](https://portal.geni.net/secure/join-project.php) named EL9383-NYU-S18 - i.e. type "EL9383-NYU-S18" into the box where it says "Enter a Project Name", click "Join", and proceed to send the join request. Requests to join a project are pending until they are approved by the project lead (me); understand that it may take up to a day for your request to be approved, so plan accordingly.



## Generate and upload an SSH key pair (one-time setup)

(Note: if you have already used GENI before and still have access to the keys you used, you don't need to create new keys - you can skip this section.)

GENI users access resources using public key authentication. Using SSH public-key authentication to connect to a remote system is a more secure alternative to logging in with an account password.

SSH public-key authentication uses a pair of separate keys (i.e., a key pair): one "private" key, which you keep a secret, and the other "public". A key pair has a special property: any message that is encrypted with your private key can only be decrypted with your public key, and any message that is encrypted with your public key can only be decrypted with your private key.

This property can be exploited for authenticating login to a remote machine. First, you upload the public key to a special location on the remote machine. Then, when you want to log in to the machine:

1. You use a special argument with your SSH command to let your SSH application know that you are going to use a key, and the location of your private key. If the private key is protected by a passphrase, you may be prompted to enter the passphrase (this is not a password for the remote machine, though.)
2. The machine you are logging in to will ask your SSH client to "prove" that it owns the (secret) private key that matches an authorized public key. To do this, the machine will send a random message to you.
3. Your SSH client will encrypt the random message with the private key and send it back to the remote machine.
4. The remote machine will decrypt the message with your public key. If the decrypted message matches the message it sent you, it has "proof" that you are in possession of the private key for that key pair, and will grant you access (without using an account password on the remote machine.)

Of course, this relies on you keeping your private key a secret. Never share your private key with anyone else, and never post it online.

On your laptop, you're going to generate a key pair and upload the public key to the GENI portal. Then, you'll use that key from now on to log in to GENI resources.

If you are using Windows, download and install [Git Bash](https://git-scm.com/downloads) and use its terminal. If you are using a Mac or Linux-based laptop, open a terminal.

Generate a key with:

```
ssh-keygen -t rsa
```

and follow the prompts to generate and save the key pair. The output should look something like this:

```
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/users/ffund01/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /users/ffund01/.ssh/id_rsa.
Your public key has been saved in /users/ffund01/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:z1W/psy05g1kyOTL37HzYimECvOtzYdtZcK+8jEGirA ffund01@example.com
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|                 |
|           .  .  |
|          + .. . |
|    .   S .*.o  .|
|     oo. +ooB o .|
|    E .+.ooB+* = |
|        oo+.@+@.o|
|        ..o==@ =+|
+----[SHA256]-----+
```

In a safe place, make a note of:

* The passphrase you used,
* The full path to your private key (`/users/ffund01/.ssh/id_rsa in` the example above) - copy and paste this from your terminal output,
* The full path to your public key (`/users/ffund01/.ssh/id_rsa.pub` in the example above) - copy and paste this from your terminal output.

If you forget these, you won't be able to access resources on GENI - so hold on to this information!

Next, upload your public key to the [SSH Keys](https://portal.geni.net/secure/profile.php#ssh) section of your profile on the GENI portal.

---

Note: If you are having trouble uploading your public key to the portal because you aren't able to find it in the file browser, you can copy it to a more convenient location and upload it from there. To do this:

* Open a terminal (a Git Bash terminal on Windows, or your operating system's native terminal application on Linux or Windows)
* Run `cp /path/to/key.pub /path/to/new/location` - substituting the path to your key and the path to a more convenient location (e.g. your Desktop) for the two arguments.
* Upload the public key from the new location.

---


Once your key is in the portal, every time you reserve GENI resources, your key will automatically be placed in the "authorized keys" list so that you can access the resource. Note that this only applies to resources you reserved after uploading a key. If you lose access to your key and have to generate and upload a new key, you will lose the ability to log on to resources you have reserved in the past.

In general, a common mistake students make is to delete or replace their keys if they are having trouble logging in to a resource. This is usually not helpful, and in most cases makes things worse. Deleting a key is like forgetting a password - don't do it!



## Create a slice

To do anything on GENI, you need to create a slice. A slice is a "container" for the resources that will be used in an experiment (read more [here](http://groups.geni.net/geni/wiki/GENIConcepts#Slice)).

Create a slice by clicking New Slice in the portal. All slices in a project must have a unique name. To make your slices easy to distinguish from your classmates', please include your net ID in your slice name. For example, for this assignment, I might call my slice "lab0-ff524."

Slices expire. Pay special attention to your slice expiration date! When your slice expires, you will lose access to all of the resources in your slice. Individual resources have their own expiration date, which may be different than, but not later than, the slice expiration date. 

Once you have created your slice, you will be presented with a blank canvas that allows you to manage resources in your slice. You can click on "Add resources" to add resources to your slice.

## Add resources

The GENI Portal includes a web-based tool called Jacks. Jacks is a graphical tool for creating a resource specification document (RSpec) and submitting a request for the resources described in the RSpec.

After you click on "Add Resources" inside your slice page, Jacks will be open in Edit mode, which looks something like this:


![](../images/jacks-add-resources.png)


Click on the black "VM" icon and drag it onto the white canvas. This icon represents a generic default virtual machine, suitable for general-purpose tasks. Repeat the above step two more times. You should now see three VM boxes on the canvas.

To edit the hostname of the VM, click the VM box. In the "Name" field at the top, replace "node-0" with "client" (use all lowercase for hostnames, by convention.) Name the other nodes "router" and "server".

Now click near the "client" VM box on the canvas, then click and drag towards the "router" VM. Release when you reach the "router" VM. You should now see a line and a box representing a link connecting the two VMs. Repeat this step to connect the "router" to the "server". Your canvas should now look like this:

![](../images/jacks-topology.png)

You can customize the details of your topology further in Jacks - e.g. you can set the characteristics (capacity, for example) of each of the network links, or change the hardware resources (CPU cores, disk space, memory), software resources (disk image, operating system), or network configuration (IP address, netmask) of the VMs. All of these customizations will also be reflected in the RSpec. For today's experiment, we won't need many customizations. We will, however, use the "Auto IP" tool to automatically assign appropriate IPs to all of the VMs in our topology, to allow them to communicate with one another.

The configuration of VMs and links is typically referred to as a "topology". Behind the scenes, Jacks is creating an RSpec that completely describes the topology you have drawn. To see the RSpec that you have just generated, click on "View RSpec."

![](../images/jacks-rspec.png)

An RSpec is a very useful document, because once you have an RSpec for a particular toplogy, you can use it to reserve the same topology many times (or share a topology) without having to go through the trouble of specifying the topology and configuration details by hand in the portal. Try this out for yourself: use the "Download RSpec" button below the canvas to save your RSpec to a file. Then, use the "X" button in the Jacks editor to return to the canvas view. Then use the "Delete All" button in the Jacks editor to clear your canvas. Now, we'll reload it from the file. Below the canvas, you'll see a "Choose RSpec" section with a few choices (portal, file, URL, text box) that allows you to provide an RSpec document in several ways. Choose the file option and choose the file that you've just saved your RSpec to. You should see your three-node topology displayed on the canvas.

At this point, your RSpec is still unbound. This means that it is a "generic" document that doesn't specify which aggregate your topology will be on. (An aggregate is a server with a set of resources that may be available by request to GENI users.) Before you can reserve your topology, you need to bind your RSpec to a particular aggregate. To do this, click on the "Site 1" box on the canvas and choose an aggregate from the dropdown list, according to the instructions in the box below.

---

### Choosing an aggregate

There are several things to consider when choosing an aggregate:

* **Aggregate type**: GENI aggregates come in several flavors (e.g. ExoGENI, InstaGENI.) For the lab assignments in the first half of this course, we will use only InstaGENI aggregates.
* **Current status**: Aggregates sometimes go offline or are otherwise unavailable. Check the [AM Status](https://portal.geni.net/amstatus.php) page to see the status of aggregates at any given time, and avoid those that are listed as "Down." You may also check the [calendar](http://tick.globalnoc.iu.edu/public_tools/cals/public/gmoc/www/month.php?cal[]=Unscheduled
) of scheduled maintenance events and unscheduled maintenance events and avoid those which are undergoing maintenance of some kind during the time that you'll need to use them.
* **Current load**: Each aggregate has a limited number of VMs, CPU cores, memory, and network capacity, and will refuse requests that it cannot satisfy based on its current load. This page shows you the current load of all InstaGENI aggregates. Choose an aggregate that appears to be less loaded with respect to the number of VMs currently in use vs the number of available VMs.
* **Load balancing**: To avoid overwhelming any single GENI aggregate, educators using GENI are asked to assign different students to different GENI aggregates. To facilitate this, please choose an aggregate whose name starts with a letter that is no more than 5 letters away from the first letter of your last name. (For example, my name is Fund, so I will choose from Case Western, CENIC, Clemson, ... , Kentucky, Kettering.)
* **Failure**: If your resource request fails, or your VMs fail to come up, try again on a different aggregate (after deleting any remaining VMs in your slice).

---


Once your resource request is bound to a particular aggregate, you will be able to reserve your resources; scroll down to the bottom of the page and click on "Reserve Resources." This will submit your RSpec to the aggregate you've selected, which will attempt to satisfy your request. If the aggregate believes it is able to give you the resources you've requested, then you'll see that your reservation has finished:


![](../images/jacks-status.png)


If your request fails, try again with a different aggregate.

Even if your request is succesful, it will take some time before your VMs are ready for you to log in. 

To see when they're ready, click on the name of your slice (at the top, where it says "Home -> Project -> Slice") to go back to the slice page. On your slice page, the canvas will automatically refresh to show you the status of your VMs - each VM will turn green as it becomes available for log in:


![](../images/jacks-some-resources-ready.png)


This may take some time. If the aggregate is unable to bring up the VMs you requested (even if the request "finishes"), you may get an email telling you that your VMs failed to boot. If this happens, delete the resources (use the "Delete" button at the bottom of the canvas) and try again with a different aggregate.

## Log in to your resources

When all your VMs are green, you are ready to log in to your resources. 

To get login details (SSH hostname and port number), click on "Details" at the bottom of the canvas. This will take you to a page that lists login details for each VM.

Once you have the hostname and port number for each node in your topology, you can log in to them. When you log in, you will need to specify the location of your private key. Open a terminal, and run

```
ssh USERNAME@HOSTNAME -p PORT -i /PATH/TO/id_rsa
```

where USERNAME is your GENI username, HOSTNAME is the hostname of the VM you are logging in to, PORT is the port number specified in the portal for that VM, and /PATH/TO/id_rsa is the full path to the private half of your key pair. (The default location is ~/.ssh/id_rsa if you generated your key with ssh-keygen and didn't specify a different location.)

If you have specified your key path and other details correctly, it won't ask you for a password when you log in to the node. (It may ask for the passphrase for your private key if you've set one.)


## What to submit

Use

```
ifconfig
```

to examine the network interfaces on each host in your topology. It should show that each VM has multiple network interfaces (e.g. `eth0`, `eth1`, etc.).

In your report, show the output of `ifconfig` and answer the following questions:

1. For each VM, can you find out what network interface is used to communicate between VMs ("data interface" or "experiment interface")? 
2. What network interface do you use when you log in to the VMs over the public Internet ("control interface" or "management interface")?
3. The experiment interface is connected to a private network, with the only traffic on this network coming from the VMs in your topology. If you listen on the "experiment interface" of one host (e.g. with a tool like `tcpdump`), can you "hear" traffic from other hosts that are not in your topology? Explain (using the `tcpdump` output).


## Delete your resources

Part of being a good GENI citizen is releasing resources when you're not using them anymore. When you have finished all parts of this assignment, use the "Delete" button at the bottom of the canvas in the GENI portal to delete your resources.

You don't have to delete your slice; it will be deleted automatically when it expires.

In general, your resources will not persist forever if you don't delete them. Resources are reserved with an expiration date, at which time you will lose access to them. 
