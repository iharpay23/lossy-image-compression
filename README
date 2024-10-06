# README

Date: 10/24/23

## PROGRAMMERS: 
Ayah Harper and Nana Adjekum

## PROGRAM PURPOSE:
Arith is a lossy image compression and decompression program. It takes a PPM image file as input for compression and outputs a compressed binary file. For decompression, it accepts the compressed binary file and reconstructs a PPM image, which may have slight quality loss compared to the original. The compression process involves reading and converting RGB values, transforming to chroma-averaged values, packing into codewords, and writing compressed data; decompression performs these steps in reverse order to reconstruct the image.

## FILE ARCHITECTURE:
The program is structured into several components, each handling specific aspects of the compression and decompression process. Here's an overview of the file structure and their purposes:

### Main Function Files:
- **40image.c**: 
  - Main entry point for the program.
  - Handles client prompts and validates input.
  - Calls `compress40` with appropriate arguments for compression or decompression.

- **compress40.c**: 
  - Implements the main steps for both compression and decompression.
  - Orchestrates the calling of individual steps based on user input.

### Compression Files:
- **readandconvert.c** (interface: readandconvert.h):
  - Handles the first 3 steps of compression:
    1. Reads the input pixmap.
    2. Converts pixel values from unsigned to floats.
    3. Converts float values to component video colorspace.
  - Utilizes UArray2b for efficient storage and processing.

- **transform.c** (interface: transform.h):
  - Performs the next 2 steps of compression:
    1. Compresses the 2D blocked array into a regular 2D array.
    2. Converts component video values into codewords for bitpacking.
  - Uses UArray2b, UArray2, and standard arrays for data manipulation.

- **writecodewords.c** (interface: writecodewords.h):
  - Executes the final steps of compression:
    1. Takes codewords and packs them into 32-bit words.
    2. Uses the custom bitpack implementation for efficient packing.
  - Stores compressed data in a UArray2 structure.

### Decompression Files:
- **readcodewords.c** (interface: readcodewords.h):
  - Initiates the decompression process:
    1. Reads 32-bit codewords from the compressed PPM.
    2. Extracts individual fields (a, b, c, d, pb, pr) using bitpack.
  - Stores extracted values in a UArray2.

- **detransform.c** (interface: detransform.h):
  - Handles the next 2 steps of decompression:
    1. Converts codewords back into component video values.
    2. Populates a UArray2b with the resulting float values.

- **convertandwrite.c** (interface: convertandwrite.h):
  - Completes the decompression process:
    1. Converts component video floats back to RGB values.
    2. Writes the decompressed pixel data to a new PPM file.
  - Utilizes UArray2b for data handling and PNM interface for file output.

### Bitpacking:
- **bitpack.c**:
  - Implements the bitpack.h interface.
  - Provides functions for width-testing, field-extraction, and field-update on 64-bit integers.

### Other:
- **structs.c**:
  - Contains declarations for common structures used in both compression and decompression processes.

This architecture allows for a modular approach to image compression and decompression, with each component handling a specific part of the process.
