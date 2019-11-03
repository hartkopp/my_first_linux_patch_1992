# my_first_linux_patch_1992
Just for documentation if all my harddiscs die at the same day :-)

----8<----

Return-Path: <torvalds@cc.helsinki.fi>
Date: Thu, 16 Jul 92 15:53:23 +0300
From: torvalds@cc.helsinki.fi (Linus Torvalds)
To: hartkopp@ibr.cs.tu-bs.de (Oliver Hartkopp)
Subject: Re: bug in linux/kermel/irq.c

Oliver Hartkopp: "bug in linux/kermel/irq.c" (Jul 16, 12:23):
>
> I have 4 serial lines in my AT (COM3 @ IRQ5, COM4 @ IRQ9) and was very
> happy having them all running. In patch1 for 0.96c there is a tiny bug
> so that IRQ9 is not running:
> 164c164
> <       set_trap_gate(0x29,IRQ9_interrupt);
> ---
> >       set_trap_gate(0x29,IRQ10_interrupt);
> 
> That's all.

Yes.  I noticed this bug myself, and it's corrected in my version. 
Thanks for the effort, though.  Patch2 will (again) be out Saturday, and
correct this and some other problems. 

> ps. Is there any possibility setting the IRQ's for the COM3+4 than
> patching the default values in 'linux/kernel/chr_drv/serial.c' ?

Yes, you can use the TIOCGSERIAL ioctl to [G]et the serial line status
(the argument is a pointer to a "struct serial_stuct", and the
TIOCSSERIAL ioctl to change the IRQ nr and port number for the serial
line (again, the argument is a pointer to a "struct serial_struct", but
only the irq and port values are used). 

Again, there was a very minor bug introduced in patch1 that means they
won't actually work: they did work in 0.96c, but only on a limited nr of
IRQ's.  Patch2 has this corrected as well, so wait for it. 

                Linus

