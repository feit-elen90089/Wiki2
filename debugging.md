# Debugging

## Contents

1. [File Sink and Source](#file-sink-and-source)

## File Sink and Source

GNU Radio flowgraphs are real-time signal processing applications that typically
operate on continuous streams of data. This can make it difficult to investigate
signal characteristics or debug unexpected behaviour. The GNU Radio *File Sink*
and *File Source* blocks are a handy way to allow offline investigation of the
signal at various points in your flowgraph using or MATLAB or Python.

<div align="center">

![File Sink](images/file_sink.png)
![File Source](images/file_source.png)

</div>

When included in your flowgraph, the *File Sink* block will save data samples
to a binary file that can then be loaded as an array in MATLAB or Python.
Similarly, a known test waveform can be generated in MATLAB or Python and then
fed into your flowgraph using the *File Source* block. The combination of sink
and source bloacks can also be used to save a waveform for latter playback.

You can load the binary file into MATLAB as follows.

```
f = fopen('filename', 'rb');
values = fread(f, Inf, 'float');
```

Note that you must choose the data type that matches the signal type you saved
in GNU Radio.

<div align="center">

| GNU Radio Type   | MATLAB Type |
| ---------------- | ----------- |
| Complex Float 32 |   'float'   |
| Float 32         |   'float'   |
| Integer 32       |   'int'     |
| Integer 16       |   'short'   |
| Integer 8        |   'char'    |

</div>

Complex samples are represented in GNU radio with interleaved I and Q
components, so after reading in an array of complex samples using 'float' you
will need to create a complex vector:
`iq = values(1:2:end) + 1j*values(2:2:end)`.

Use the Numpy package to load a binary file into Python.

```python
import numpy
f = numpy.fromfile(open("filename"), dtype=numpy.uint8)
```
Again, the Numpy data type selected must match the GNU Radio signal type.

<div align="center">

| GNU Radio Type   |     Numpy Type      |
| ---------------- | ------------------- |
| Complex Float 32 |   numpy.complex64   |
| Float 32         |   numpy.float32     |
| Integer 32       |   numpy.int32       |
| Integer 16       |   numpy.int16       |
| Integer 8        |   numpy.int8        |

</div>

See the following GNU Radio documentation pages to understand these blocks and
details on loading or creating binary waveforms files in MATLAB and Python.

- [GNU Radio File Sink](https://wiki.gnuradio.org/index.php/File_Sink)
- [GNU Radio File Source](https://wiki.gnuradio.org/index.php/File_Source)
