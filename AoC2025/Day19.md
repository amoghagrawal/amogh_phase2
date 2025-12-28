# Day 19: ICS/Modbus - Claus for Concern

> You're called into the command centre, where screens flicker with delivery statistics. Everything looks normal on the surface—1,000 presents in stock, 98% success rate, and all systems are operational. But the phones won't stop ringing with confused citizens asking why they're receiving chocolate eggs instead of the toys and gifts they ordered. <br>
> The logistics manager pulls up a delivery manifest. "Look at this", she says, pointing at the screen."The system indicates that we delivered a teddy bear to the Miller family, but they received a chocolate bunny instead. It's the same weight, exact dimensions, but completely different items."

## Solution

- SCADA consists of monitoring systems, PLCs and sensors to manage critical functions
- SCADA generally communicates using TCP port 502
- By simply running the restoration script which writes values to coils and holding registers
- It then reads the flag from the registers to get the flag as `THM{eGgMas0V3r}`

## Objectives

### What port is commonly used by Modbus TCP?
> 502

### What's the flag?
> THM{eGgMas0V3r}

## Concepts learnt:

- How SCADA (Supervisory Control and Data Acquisition) systems monitor industrial processes
- What PLCs (Programmable Logic Controllers) do in automation
- How the Modbus protocol enables communication between industrial devices