# Genode & Fiasco Update

This section covers the updates for Genode and Fiasco.OC. 

## Agenda

<a href="https://github.com/malsami/foc/tree/r78"><img
		alt="foc r78"
		src="https://img.shields.io/badge/foc%20r78-done-brightgreen.svg?style=flat-square"></img></a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+
<a href="https://github.com/malsami/genode/tree/18.02_r78"><img
		alt="Genode 18.02"
		src="https://img.shields.io/badge/Genode%2018.02-done-brightgreen.svg?style=flat-square"></img></a>
<br>
<a href="https://github.com/malsami/foc/tree/focnados_r78"><img
		alt="focnados r78"
		src="https://img.shields.io/badge/focnados%20r78-done-brightgreen.svg?style=flat-square"></img></a> +
<a href="https://github.com/malsami/genode/tree/focnados_18.02_r78"><img
		alt="Genode Focnados 18.02"
		src="https://img.shields.io/badge/Genode%20Focnados%2018.02-done-brightgreen.svg?style=flat-square"></img></a>
<br>
<img alt="Genode Focnados 18.02 Taskloader"
		src="https://img.shields.io/badge/Genode%20Focnados%2018.02%20Taskloader-done-brightgreen.svg?style=flat-square"></img>

<a href="https://github.com/argos-research/genode-CheckpointRestore-SharedMemory/tree/fixing_restore-AR-18.02"><img
		alt="Genode Focnados 18.02 Checkpoint-Restore"
		src="https://img.shields.io/badge/Genode%2018.02%20Focnados%20r78%20Checkpoint%20Restore-incomplete%20/%20work%20in%20progress-orange.svg?style=flat-square"></img></a>

<img alt="Genode Focnados 18.02 seL4"
		src="https://img.shields.io/badge/Genode%2018.02%20seL4-future%20work-red.svg?style=flat-square"></img>


## Setup 
The default setup listed below is based on Genode 16.08 and foc r67.
To use the new versions Genode 18.02 and foc r78 please take a look at "Structure of directories".

If you like to use a VM for this project,
please follow the steps on the [ArgOS-research website](https://argos-research.github.io/documentation/install.html).

If you like to use your native machine,
just `git clone https://github.com/argos-research/operating-system.git`
and execute `./setup.sh` .
This will build the project "dom0-HW" on platform "focnados_panda" by default.
Please adjust the MAKEFILE to your needs.

## Structure of directories

Genode 18.02 and foc r78:  
[Malsami Genode/branch_18.02_r78](https://github.com/malsami/genode/tree/18.02_r78)

Genode 18.02 and focnados r78:  
[Malsami Genode/branch focnados_18.02_r78](https://github.com/malsami/genode/tree/focnados_18.02_r78)

Checkpoint Restore and Taskloader for Genode 18.02 and focnados r78:  
[Malsami Genode/branch 18.02](https://github.com/argos-research/operating-system/tree/18.02)
