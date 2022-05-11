# romcard
A periferal card for Apple //

This is a project I created in 1995 - ROMcard, based on 8 x 27C512 EPROM chips. A photo of the original is posted.
The ROMs are organized in 256 banks of 2kB each, numbered #00 to #FF
Banks are selected by writing a byte (#00 - #FF) into $C0Nx, where N = 8 + [slot number]
When writing to $C0Nx at the same time the ROM chip is also enabled
When a bank is selected, its content are seen in the address space $C800-$CFFF
To de-enable the ROM chips a write must be performed to address $CFFF or reset executed
If a user program is accessing the card, it is important that at the end a write is performed to $CFFF so that the card is deactivated and does not conflict with other hardware, which is using the same address space.
The 256-byte bootloader is programmed in 2 separate 256x4 bit PROM chips 82S129.
The boot loader is available at addresses $CM00-$CMFF, where M = [slot number]
Each program must be recorded in the ROM as follows:
4 markers – #AA #D5 #55 #2A, always starting at an address $xxx00 – multiple of #100 
16 bytes with the name of the program
2 bytes indicating the start address of the program
2 bytes with the length of the program
The actual binary code of the program
Recommended installation is on Slot 7.
The boot loader has functionality that it captures the boot sequence of the computer and executes the first program recorded onto the ROM – usually DOS.
If ”\” is pressed while performing a cold reset – the boot sequence will override the ROMcard2 boot so floppy disk can boot.
Programs are called with “&” followed by the number of the program
&2 calls the program which returns a list of programs recorded onto ROMcard2.
10 Apr 2022 edit: added new firmware for ProDOS. Functions as a standard block device.
www.clintech.net/romcard

Copyright (c) 2021 Ralle Palaveev
All rights reserved.

Redistribution and use in source, binary, and manufactued forms, with or without
modification, are permitted provided that the following conditions are met:
1. Redistributions of source code and design files must retain the above copyright
   notice, this list of conditions and the following disclaimer.
2. Redistributions in binary or manufactured form must reproduce the above copyright
   notice, this list of conditions and the following disclaimer in the
   documentation and/or other materials provided with the distribution.
3. All advertising materials mentioning features or use of this software
   or hardware must display the following acknowledgement:
   This product includes software and hardware developed by Ralle Palaveev.
4. Neither the name of Ralle Palaveev nor the
   names of its contributors may be used to endorse or promote products
   derived from this software or hardware without specific prior written permission.

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
