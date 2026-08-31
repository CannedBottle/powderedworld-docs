# Save Order

> This page is mostly for me to reference, since once the save system is done there is little need to know what each binary sequence corresponds to.
> However, it doesnt hurt to keep this here, does it?

----

Each `.pwdr` file is saved in the same way. It represents the simulation as a binary file.  **Here is the order in which the binary is saved and what each number represents:**
> *When a bullet point is indented, it is instanced a variable number of times within that indentation level.*

- A PascalString that acts as a key and a header: "PWEngine {version number}"

- A 32-bit integer; the position to put the pointer when reading the file to find the offset dictionary.

- A 16-bit integer; Number of elements

    - A PascalString for every element's name

- An 8-bit integer; The number of cell-specific fields each cell is created with

- A 32-bit integer; the number of chunks saved

    - A 32-bit integer; the X-position of the current chunk

    - A 32-bit integer; the Y-position of the current chunk

    - A 32-bit integer; The number of <br> runs after the cells were compressed *(using RLE)*

        - A 32-bit integer; The length of the current run *(generated with RLE)*

        - A 16-bit integer; The element of the current cell, expressed as the index to the name in the lookup table generated above.

            - An 8-bit integer; one of the cell-specific fields the current cell has.

    <br>
    
- A 32-bit integer; The amount of chunks in the file offset dict

    -  A 32-bit integer; The X-position of the current chunk in this file offset dictionary

    - A 32-bit integer; The Y-position of the current chunk

    - A 32-bit integer; The file offset of the chunk.

