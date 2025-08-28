# tetanus
Rust based pentesting tool. Will work as an implant generator, c2 server, c2 client, distrobox manager, engagement data management, and markdown note generator (and maybe editor?).

# Purpose
This will basically replace my existing pentest_tool project. It will do all the same things, but will use a client/server model and include a client that will run on Windows Victim machines in order to automate some of the victim stuff.

This is really meant to be used once you have initial access to a machine during a pentest.

Rust already seems to get around EDR/AV pretty easily, but I do also intend to add some evasion features later on.

# Design considerations
Clients and the server will be wirtten in rust. The core modules will all be written in rust. I intend to design a system that will allow custom modules to be written in dotnet, python, powershell, and rust.

The server will keep the states of all clients, projects, and notes. The clients will interact with the server. Each client will have it's own handler thread. I intend to manage the threads with either Tokio or some sort of agent system. MPSC channels will be utilized to talk to all threads. 

The network communication for all clients will be encrypted. Victim clients will use a beacon model to check if there are any commands to run. Attacker clients will just use a tcp connection that stays open.

Any important data should be either printed to the attacker client, or saved in markdown format to the notes. The markdown format will be configurable, with Obsidian being the default.

There will be both a CLI and a GUI for the Attacker clients. The server and victim clients will be CLI only.

The attacker clients should have an easy function to spin up a server on the same machine they're running on, or any server that the attacker has SSH access to.

I plan to document how to properly write the network communications so that users can create their own modules that talk to the server or extend functionality with other tools.

This repo will be empty for a bit while I get the initial client/server communications working.

# WIP
This is very much a work in progress. Nothing works yet. If you want the original tool, head over to my pyro pentest tool repository and clone the stable branch.
