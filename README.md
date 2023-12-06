# Turtle Interpreter Documentation

## Overview

The Turtle Interpreter is an open-source project designed to interpret and execute programs written in the Turtle programming language. This documentation provides an overview of the key components and modules of the Turtle Interpreter, along with explanations of their functionality and purpose.

The Core of the Interpreter is made using the incredible book [Crafting Interpreters](https://craftinginterpreters.com) from Robert Nystrom.

## Project Structure

The Turtle Interpreter project is organized into several files, each serving a specific purpose:

1. **main.c**: Entry point of the Turtle Interpreter. The `main` function initializes the interpreter and handles command-line arguments.

2. **common.h**: Header file containing common definitions and includes necessary for the entire project. It includes standard libraries such as `stdbool.h`, `stddef.h`, and `stdint.h`.

3. **chunk.c**: Source file implementing operations related to code chunks. Code chunks store the bytecode representation of Turtle programs.

4. **chunk.h**: Header file defining the `Chunk` struct and function prototypes related to code chunk management.

5. **memory.c**: Source file implementing memory management functions such as reallocation. It includes a function for dynamically resizing arrays.

6. **memory.h**: Header file defining memory-related macros and function prototypes for dynamic memory allocation and deallocation.

7. **debug.c**: Source file introducing debugging functionality. It includes functions `disassembleChunk` and `disassembleInstruction` for disassembling bytecode. The disassembly output is designed to aid in debugging Turtle programs.

8. **debug.h**: Header file declaring functions related to debugging. It includes prototypes for `disassembleChunk` and `disassembleInstruction`.

## Code Chunks (`chunk.c`, `chunk.h`)

The Turtle Interpreter uses code chunks to represent the bytecode of Turtle programs. A code chunk (`Chunk`) consists of an array of bytes (`code`), a count of the number of bytes used (`count`), and the capacity of the array (`capacity`). The main operations related to code chunks are:

- `void initChunk(Chunk* chunk)`: Initializes a code chunk by setting the count and capacity to zero and allocating memory for the code array.

- `void freeChunk(Chunk* chunk)`: Frees the memory allocated for the code array within a code chunk and resets the chunk to its initial state.

- `void writeChunk(Chunk* chunk, uint8_t byte)`: Writes a byte to the code chunk. If the capacity is exceeded, it dynamically resizes the code array to accommodate more bytes.

## Memory Management (`memory.c`, `memory.h`)

The memory management module provides functions for dynamic memory allocation and deallocation. Key macros include:

- `GROW_CAPACITY(capacity)`: Expands the capacity of a dynamic array. If the current capacity is less than 8, it sets the new capacity to 8; otherwise, it doubles the current capacity.

- `GROW_ARRAY(type, pointer, oldCount, newCount)`: Dynamically resizes an array of a specified type. It is used to resize the code array within a code chunk.

- `FREE_ARRAY(type, pointer, oldCount, newCount)`: Frees the memory allocated for an array. It is used to free the memory of the code array within a code chunk.

- `void* reallocate(void* pointer, size_t oldSize, size_t newSize)`: Reallocates memory for a block of memory, handling resizing and freeing.

## Debugging Functionality (`debug.c`, `debug.h`)

The debugging functionality has been introduced to aid developers in understanding the execution flow and bytecode representation. The following functions have been added:

- `void disassembleChunk(Chunk* chunk, const char* name)`: Prints the disassembled bytecode of a given code chunk, identified by the provided name.

- `int disassembleInstruction(Chunk* chunk, int offset)`: Disassembles an individual instruction at the specified offset within a code chunk.

## Build and Execution (`main.c`)

The `main.c` file serves as the entry point for the Turtle Interpreter. It now includes additional functionality to test the debugging features. Specifically, it creates a simple code chunk containing an `OP_RETURN` instruction, disassembles the chunk using `disassembleChunk`, and then frees the allocated memory.


