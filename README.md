# PPMS-FMR-Control-Software-via-Python
This a python implementation of controlling software that performs ferromagnetic resonance (FMR) in Quantum Design (QD) Physical Property Measurement System (PPMS).

## Run PPMS_FMR.py to start the control software

The sample should be mounted on a coplanar waveguide (CPW) or stripline and installed on a PPMS FMR probe (designed by QD). Electronics should be connected via GPIB-USB converter to the computer this program runs on, while the PPMS should be connected via LAN.

The electronics include an AC current source (Keithley 6221), microwave source (Agilent N5183) and a lock-in amplifier (Stanford SR830). The AC current source drives a small modulating magnetic field, and the lock-in amplifier catches the change of microwave absorption (dependent on magnetic field). The resultant spectrum is a derivative of the real peak lineshape.

![LSC441_YIG35_GGG_Etched_IP_300K_10p0GHz_0dBm_20p0mA](https://user-images.githubusercontent.com/46427095/203198455-b9890568-0f07-48fb-85f2-77bfb81d5cbd.png)

Enter folder name and path in "Sample ID" and "Folder" text boxes in order to specify where the data will be saved.

The PPMS and electronics must be connected before operation. Click "Connect GPIB Conn" button on the left to connect. The addresses of the three electronics can be edited. Successful connection will change the status tags below.

![PPMS_FMR_ScreenShot](https://user-images.githubusercontent.com/46427095/203198503-eca35083-3de7-4aa6-83c3-2deef0f694b0.png)

Upon successful connection, labels on the right will update real-time status, such as temperature/field/lock-in reading. You can use text boxes and buttons to set key parameters of the PPMS, electronics.

## This program allows series of measurements at different frequencies and temperatures.

"Freq(GHz):Field(G) pairs(Seperate with ',')" text box reads in pairs of driving microwave frequency and resonance field positions. For example, "10: 2400, 20: 6000" will do an FMR scan centered at 2400G with 10GHz microwave and another FMR scan centered at 6000G with 20GHz microwave".

"Initial linewidth(G)" text box is your estimate of the linewidth at 2400G and 10GHz; "Final linewidth(G)" text box is your estimate of the linewidth at 6000G and 20GHz. Scan ranges will be 7x the estimated linewidth. "10: 2400, 15: 4500, 20: 6000", 10G Initial linewidth and 20G Final linewidth will yield scans of 2365-2435G at 10GHz, 4447.5-4552.5G at 15GHz (assuming linear frequency dependence of linewidth) and 5930-6070G at 20GHz.

"Temps(K):Shift(G) (Seperate with ',')" text box reads in pairs of measurement temperature and field shift. For example, "150: 0, 300: 15" will do two series of FMR scans. The first series will be done at 150K, with the scans being "10GHz: 2400G, 20GHz: 6000G". The second series will then be done at 300K, with scans being "10GHz: 2400G+15G, 20GHz: 6000G+15G".

6221 Setup.txt and CommandsforInstruments.docx are manuals for how to set up AC current source 6221 and common GPIB commands for the instruments.

QDInstrument.dll holds all necessary functions to interface with the PPMS.
