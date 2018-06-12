# Genode & Fiasco Update

This section covers the updates for Genode and Fiasco.OC. 

## Agenda

<a href="https://github.com/malsami/foc/tree/r78"><img
		alt="foc r78"
		src="https://img.shields.io/badge/foc%20r78-done-brightgreen.svg?style=flat-square"></a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+
<a href="https://github.com/malsami/genode/tree/18.02_r78"><img
		alt="Genode 18.02"
		src="https://img.shields.io/badge/Genode%2018.02-done-brightgreen.svg?style=flat-square"></a>
<br>
<a href="https://github.com/malsami/foc/tree/focnados_r78"><img
		alt="focnados r78"
		src="https://img.shields.io/badge/focnados%20r78-done-brightgreen.svg?style=flat-square"></a> +
<a href="https://github.com/malsami/genode/tree/focnados_18.02_r78"><img
		alt="Genode Focnados 18.02"
		src="https://img.shields.io/badge/Genode%20Focnados%2018.02-done-brightgreen.svg?style=flat-square"></a>

<a href="https://github.com/argos-research/genode-CheckpointRestore-SharedMemory.git"><img
		alt="Genode Focnados 18.02 Checkpoint-Restore"
		src="https://img.shields.io/badge/Genode%2018.02%20Focnados%20r78%20Checkpoint%20Restore-incomplete%20/%20work%20in%20progress-orange.svg?style=flat-square"></a>

<img alt="Genode Focnados 18.02 seL4"
		src="https://img.shields.io/badge/Genode%2018.02%20seL4-future%20work-red.svg?style=flat-square"></a>


## Setup 
The default setup listed below is based on Genode 16.08 and foc r67.<br />
To use the new versions Genode 18.02 and foc r78 please take a look at "Structure of directories".

If you like to use a VM for this project,<br />
please follow the steps on the [ArgOS-research website](https://argos-research.github.io/documentation/install.html).

If you like to use your native machine,<br />
just clone https://github.com/argos-research/operating-system.git branch master<br />
and execute ./setup.sh .<br />
This will build the project "dom0-HW" on platform "focnados_panda" by default.<br />
Please adjust the MAKEFILE to your needs.

## Structure of directories
Genode 18.02 and foc r78:<br />
https://github.com/malsami/genode<br />
branch 18.02_r78

Genode 18.02 and focnados r78:<br />
https://github.com/malsami/genode<br />
branch focnados_18.02_r78

Checkpoint Restore for Genode 18.02 and focnados r78:<br />
https://github.com/argos-research/genode-CheckpointRestore-SharedMemory<br />
branch fixing_restore-AR-18.02
