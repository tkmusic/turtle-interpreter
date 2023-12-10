# Turtle Interpreter Documentation

## Overview

The Turtle Interpreter is an open-source project designed to interpret and execute programs written in the Turtle programming language. This documentation provides an overview of the key components and modules of the Turtle Interpreter, along with explanations of their functionality and purpose.

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

9. **value.c**: Source file implementing functions for managing a dynamic array of `Value` types.

10. **value.h**: Header file declaring functions and structures related to managing `Value` types.

## Code Chunks (`chunk.c`, `chunk.h`)

The Turtle Interpreter uses code chunks to represent the bytecode of Turtle programs. A code chunk (`Chunk`) consists of an array of bytes (`code`), a count of the number of bytes used (`count`), and the capacity of the array (`capacity`). Additionally, code chunks now include a `ValueArray` named `constants` to store constant values. The main operations related to code chunks are:

- `void initChunk(Chunk* chunk)`: Initializes a code chunk by setting the count and capacity to zero, allocating memory for the code array, and initializing the constants array.

- `void freeChunk(Chunk* chunk)`: Frees the memory allocated for the code array and constants array within a code chunk and resets the chunk to its initial state.

- `void writeChunk(Chunk* chunk, uint8_t byte)`: Writes a byte to the code chunk. If the capacity is exceeded, it dynamically resizes the code array to accommodate more bytes.

- `int addConstant(Chunk* chunk, Value value)`: Appends a constant value to the constants array and returns its index.

## Debugging Functionality (`debug.c`, `debug.h`)

The debugging functionality has been updated to handle the new `OP_CONSTANT` instruction. The following functions have been added:

- `void disassembleChunk(Chunk* chunk, const char* name)`: Prints the disassembled bytecode of a given code chunk, identified by the provided name.

- `int constantInstruction(const char* name, Chunk* chunk, int offset)`: Disassembles an `OP_CONSTANT` instruction at the specified offset within a code chunk, printing detailed information about the constant value.

## Value Management (`value.c`, `value.h`)

The `value.c` and `value.h` files introduce functions for managing a dynamic array of `Value` types. The `ValueArray` structure includes fields for capacity, count, and an array of values. Functions include:

- `void initValueArray(ValueArray* array)`: Initializes a `ValueArray` by setting the values array to `NULL` and the capacity and count to zero.

- `void writeValueArray(ValueArray* array, Value value)`: Appends a `Value` to the values array. If the capacity is exceeded, it dynamically resizes the array.

- `void freeValueArray(ValueArray* array)`: Frees the memory allocated for the values array within a `ValueArray` and resets the array to its initial state.

- `void printValue(Value value)`: Prints a `Value` to the console.

## Build and Execution (`main.c`)

The `main.c` file now includes additional functionality to demonstrate the new `OP_CONSTANT` instruction and constant handling. It creates a chunk with an `OP_CONSTANT` instruction and a constant value, followed by an `OP_RETURN` instruction. The chunk is then disassembled and printed using `disassembleChunk`.
