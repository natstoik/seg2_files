# seg2_files
## Simple file reading tools

seg2_files is a basic tool for reading binary SEG2 format seismic and ground-penetrating radar data files. It improves on other implementations by having few non-standard library dependencies (only _numpy_) and being able to read file headers containing any field supported by the SEG2 standard. 

### Using this library
First, import the function "seg2_load" from the _seg2load_ module in the library:
```py
from seg2_files.seg2load import seg2_load
```
Next, load the trace data as a numpy array with traces as columns, and header as a dictionary from a SEG2 file:
```py
traces, header = seg2load('example_file.seg2')
```

The header is a nested dictionary, with the following structure:

header
* Key:'tr' Value: dictionary of trace headers
    * Key: trace header field e.g. 'SAMPLE_INTERVAL' for trace timestep (more are detailed in SEG2             specification), Value: List of values of the key field for each trace in the file in order
* Key: 'rec' Value: Dictionary with field names as keys (found in SEG2 standard) containing information                     about the entire recording (file)

As an example, to get the timestep (_dt_) between samples of the 3rd trace in a file, you can use:
```py
seis_data, seis_header = seg2_load('example_file.seg2')
dt = seis_header['tr']['SAMPLE_INTERVAL'][2]
```

And that's all there is to it! This library is simple but hopefully should cover most basic use cases. Don't hesitate to contact me if you have an additional feature idea that you think would be useful or if I missed part of the standard implementation. 

Note that this is library is supposed to be pretty bare-bones - it reads SEG2 files (maybe SEGY in the future) and turns them into Python data types. That's it. Processing, plotting, etc. are up to other libraries or you.
