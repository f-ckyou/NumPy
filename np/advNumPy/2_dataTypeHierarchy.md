NumPy's data type hierarchy is a structured system that defines how data is represented and manipulated within ndarray objects. This hierarchy encompasses various data types, their characteristics, and how they interact with one another. Here’s a detailed overview of the NumPy data type hierarchy:

## Overview of NumPy Data Types

1. **Basic Data Types**:
   - NumPy provides a range of basic data types, each represented by a single character code. These types are used to define the kind of data that can be stored in an ndarray.
   - Common basic data types include:
     - **`i`**: Integer (e.g., `int32`, `int64`)
     - **`u`**: Unsigned integer (e.g., `uint32`, `uint64`)
     - **`f`**: Float (e.g., `float32`, `float64`)
     - **`c`**: Complex float (e.g., `complex64`, `complex128`)
     - **`b`**: Boolean
     - **`O`**: Object
     - **`S`**: String
     - **`U`**: Unicode string
     - **`V`**: Void (fixed chunk of memory for other types)

2. **Structured Data Types**:
   - NumPy allows the creation of structured data types, which enable the storage of heterogeneous data in a single ndarray. A structured dtype can contain multiple fields, each potentially having different data types.
   - Example of creating a structured dtype:
     ```python
     import numpy as np
     dt = np.dtype([('name', 'U16'), ('grades', 'f8', (2,))])  # 16-character string and an array of two floats
     ```
   - This allows for complex data structures, similar to records in databases.

3. **Sub-arrays**:
   - Sub-arrays can be defined within structured dtypes, allowing for multi-dimensional arrays as fields of a structured array.
   - For example, a field could be defined as a 2D array:
     ```python
     dt = np.dtype([('data', np.float64, (3, 4))])  # A field 'data' that is a 3x4 array of floats
     ```

## Data Type Properties

Each dtype object in NumPy has several important properties:

- **Type**: Indicates the type of the data (e.g., integer, float).
- **Size**: The number of bytes used to store each element.
- **Byte Order**: Specifies whether the data is stored in little-endian or big-endian format.
- **Itemsize**: The size in bytes of each element in the array.

### Example of Retrieving Properties

```python
import numpy as np

# Define an array with a specific dtype
arr = np.array([(1, 2.0), (3, 4.5)], dtype=[('x', 'i4'), ('y', 'f4')])

# Accessing dtype properties
print(arr.dtype)          # Output: [('x', '<i4'), ('y', '<f4')]
print(arr.dtype['x'])     # Output: (dtype('int32'))
print(arr.itemsize)       # Output: 8 (4 bytes for int + 4 bytes for float)
```

## Type Promotion

NumPy follows specific rules for type promotion when performing operations involving multiple dtypes:

1. If two different types are combined, NumPy promotes them to a common type that can accommodate all values without loss.
2. The promotion hierarchy typically follows this order:
   - Boolean < Integer < Float < Complex

### Example of Type Promotion

```python
a = np.array([1, 2, 3], dtype='i4')    # Integer array
b = np.array([1.0, 2.0], dtype='f8')    # Float array

result = a + b                           # Result will be promoted to float64
print(result.dtype)                      # Output: float64
```

## Type Checking Functions

NumPy provides several functions to check and manipulate dtypes:

- **`numpy.can_cast(from_, to)`**: Checks if one dtype can be safely cast to another.
- **`numpy.promote_types(type1, type2)`**: Returns the smallest dtype that can hold both input types.
- **`numpy.result_type(*arrays_and_dtypes)`**: Returns the resulting dtype from applying type promotion rules.

## Conclusion

The NumPy data type hierarchy is essential for efficient memory management and numerical computations in Python. By understanding the various basic and structured data types, their properties, and how they interact through promotion rules, users can effectively utilize NumPy's capabilities for handling diverse datasets in scientific computing and data analysis tasks.


---- 

Data types have superclasses, which can be used with the np.issubtype function:

``` python

ints = np.ones(10, dtype=np.uint16)
floats = np.ones(10, dtype=np.float32)

np.issubdtype(ints.dtype, np.integer) # True
np.issubdtype(floats.dtype, np.floating) # True

```

to see all of the parent classes of a specific data type by calling the type's mro method:
``` python

np.float64.mro()
# output
[numpy.float64,
numpy.floating,
numpy.inexact,
numpy.number,
numpy.generic,
float,
object]
# therefore
np.issubtype(ints.dtype, np.number) # True
```

# Hierarchy
![image](dtype-hierarchy.png)