# RING BUFFER

Welcome to the Ring Buffer implementation! This ring buffer is designed for use in embedded projects based on microcontrollers.

## Features

- **Custom Element Size**: You can create a ring buffer for any custom data type.
- **Efficient Memory Usage**: The buffer efficiently manages memory, allowing for continuous data processing.

**Warning!** This implementation is **not thread-safe**. Use with caution in multi-threaded environments.

## Usage

### Defining a Custom Data Type

Here’s an example of how to define a custom data type for use with the ring buffer:

```c
typedef struct test_struct {
    uint16_t a;
    char b;
} test_struct_st;
```

### Initializing the Ring Buffer

To create a ring buffer with *BUFF_SIZE* length and *sizeof(test_struct_st)* element size, use the following:

```c
ring_buffer_st *test_ring_buffer = ringBufferInit(sizeof(test_struct_st), BUFF_SIZE);
```

### Writing Data to the Buffer

To write a single element of your custom data type:

```c
test_struct_st test_data = { .a = 1137, .b = 'm' };
ringBufferPutSymbol(test_ring_buffer, (void*)&test_data);
```

To write multiple elements at once:

```c
test_struct_st test_data_2[20] = { /* initialize with values */ };
ringBufferPutData(test_ring_buffer, (void*)test_data_2, 20);
```

### Reading Data from the Buffer

To get the number of available symbols in the buffer:

```c
uint16_t available_symbols = ringBufferGetAvail(test_ring_buffer);
```

To retrieve a single element from the buffer:

```c
test_struct_st test_data = {0};
ringBufferGetSymbol(test_ring_buffer, (void*)&test_data);
```

To retrieve multiple elements:

```c
test_struct_st test_data_2[20] = {0};
ringBufferGetData(test_ring_buffer, (void*)test_data_2, 20);
```

### Clearing and Deinitializing the Buffer

To clear the buffer and reset its indices:

```c
ringBufferClear(test_ring_buffer);
```

To deinitialize and free the buffer's memory:

```c
ringBufferDeinit(test_ring_buffer);
```

## Error Handling

The ring buffer functions return error codes defined in `ring_buff_err_t`. Here are some common error codes:

- `ERR_RING_BUFF_NULL`: The buffer is NULL.
- `ERR_RING_BUFF_EMPTY`: The buffer is empty when trying to get data.
- `ERR_RING_BUFF_FULL`: The buffer is full when trying to put data.
- `RING_BUFF_OK`: Operation was successful.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

---

Feel free to modify or add any specific details according to your preferences or requirements!