<!-- 5.4 -->

If you are having trouble sending function keys to a managed device, there may be a problem with your terminal's emulation type, the function key's escape sequence, or the managed device itself.

# Escape Sequences

If the function key is between F5 and F12, then depending on your emulation type, it may contain a ~ character at the end of its escape sequence. Since the appliance uses ~ to escape menu commands, it may not correctly register the function key.

To test this, try hitting F8 while using the terminal command. If pressing ENTER immediately after F8 exits you from a terminal session, then the ~ in the escape sequence is being intercepted. A simple workaround for this limitation is to type an additional ~ after the function key. Pressing F8 + ~ should register the correct sequence.

# Emulation Types

The ability to send function keys (as well as other special keys like HOME and END) to a managed device can often depend on the SSH client used along with the keyboard emulation type selected.

For example, the F8 workaround mentioned above works with SecureCRT using Linux emulation, but not with XTerm emulation.

# Device Support

It is also possible that the managed device simply does not support function keys during regular operation or in special cases like BIOS load.

For example, it is possible to use functions keys in Emacs on an HP Linux Server if you connect to the Uplogix appliance via SecureCRT with Linux emulation. However, the BIOS of an HP server only supports function keys delivered via keyboard or through ILO. Any terminal connected to its serial port, including a straight connection from a laptop, will not be able to send function keys. Instead, try ESC + 8 for F8, ESC + 9 for F9, etc.