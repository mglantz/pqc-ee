# Post-Quantum Cryptography for an Ansible execution environment
This is an example of an RHEL 10 Post-Quantum Cryptography (PQC) Execution Environment.
For demo purposes, this EE only allows SSH using the PQC kex algorithm mlkem768x25519-sha256.

```
├── context
│   └── openssh.config # Only allowing mlkem768x25519-sha256. Remove if you don't like that.
├── execution-environment.yml # Execution environment
├── LICENSE
└── README.md
```

# How to build your own PQC execution environment
1. I'm using the Red Hat Universal Base Image for RHEL 10.1 to build the execution environment, that means you also need access to that.
[You get access for free](https://catalog.redhat.com/en/software/base-images), but need access to this image: registry.access.redhat.com/ubi10:10.1

2. Get ansible-builder. I used the upstream version of ansible-builder for Fedora 43, which is my own build rig.
```
$ pip install ansible-builder
```

3. Clone this repository
```
$ git clone https://github.com/mglantz/pqc-ee
```

4. IF you like it to also allow non-PQC kex algorithms, modify the execution-environment.yml file and remove the lines which adds the openssh.config file.

5. IF you like it to use Red Hat downstream supported ansible and ansible-runner, you need to get those from Red Hat repositories.

6. Build the image
```
$ ansible-builder build
```

7. Push the image to some registry you like or Private Automation Hub, etc, and use it.

8. IF you are using Ansible Automation Platform, configure a new execution environment which points at your registry of choice - where you put the execution environment.
