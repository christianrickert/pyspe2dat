# pyspe2dat
Simple file format conversion tool for Magnettech machines

## Software requirements
The minimum software requirement for pyspe2dat is a current version of:
* `Python 3`

## Converting files

Put your recording files in spe2dat's subfolder and execute pyspe2dat.py - all `.spe` files will be converted to ASCII files with the file extension `.dat`. Furthermore, all recording parameters as well as the time of modification from the original binary file are preserved.

## Start parameters

Use pyspe2dat's start parameters to adjust the ASCII file output:

* Parameter:	`--mscope n`
```
Values:		 1.0, former MiniScopeControl model using unsigned integers for data storage
		 2.0, recent MiniScopeControl model using signed integers for data storage
Default:	 1.0
```
* Parameter:	`--pool n`
```
Values:		 1.0-8.0, output 4096-512 data points by merging consecutive values
		-1.0, use the 'Steps' value set in the MiniScopeControl
Default:	-1.0
```
* Parameter:	`--rescale n`
```
Values:		 1.0-x, rescale the spectra with a fixed divisor
		-1.0, rescale using the 'Gain' value set in the MiniScopeControl
Default:	-1.0
```
* Parameter:	`--shift n`
```
Values:		 0.0-x, shift the spectra vertically adding a fixed offset value
Default:	-16384.0
```

## FAQ

1. Can I combine several of the start parameters?
   - Yes. Please see below for more detailed examples.

2. How do I use the start parameters with Windows?
   - Create a shortuct to the `pyspe2dat.py` file and edit the `Target` field:
   
		`"C:\Software\pyspe2dat\pyspe2dat.py" --pool 4.0`

3. Why are my spectra segmented exhibiting alternating offset steps after conversion?
   - Probably you're using the recent version of MiniScopeControl, so you need to force pyspe2dat to accept the newer data file format (with singed integers):

     `"C:\Software\pyspe2dat\pyspe2dat.py" --mscope 2.0 --shift 0.0`
    
4. How do I use the start parameters with Linux?
   - Create an executable shell script with two lines of code:
   
     ```
     cd /home/user/software/pyspe2dat
     python3 ./pyspe2dat.py --mscope 1.0 --pool 1.0 --rescale 1.0
     ```
