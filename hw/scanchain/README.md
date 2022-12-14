# hw-scanchain

This is a simple, parameterized scanchain interface which can be used to 
interact with targets from a host machine over UART. This was designed for
SCUM-V and the Arty-A7 100T but can trivially ported to other FPGAs and SoCs.

By default, this project uses a scan clock of 100KHz. This can be changed in
`a7top.v`. To use this, attach `SCAN_CLK`, `SCAN_EN`, `SCAN_IN`, and 
`SCAN_RESET` to the target. Next, press the reset switch on the FPGA to start
the UART interface. The target SoC does not need to be configured directly; a
remote reset can be triggered via the scan chain over UART. 

This project uses the following binary wire format for UART:

    Scan chain write request:  {2'b0, 1'b_reset, 169'b_payload, 12'b_addr}.
    Scan chain write response: {7'b0, 1'b_success}

