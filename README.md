# narray
A simple library to give (very minimal) functions of multidimensional
array compatible with C/Fortran



## Installation


1. Add the dependency to your `shard.yml`:

   ```yaml
   dependencies:
     narray:
       github: jmakino/narray
   ```

2. Run `shards install`


## Getting started
At your project directory (where you ran shards install), try

   crystal lib/narray/examples/narray_test.cr

should show some output.

  
## Usage

```
  require "narray"
```
provides the Narray class.
```
  Narray(T).new(nx : Int32,ny : Int32 = 1, nz : Int32 = 1)
```
creates the Narray of type T of up to three dimensions. For example,
```
  x = Narray(Float64).new(10)
```
makes one-dimensional array of size 10 of Float 64, and
```
  xy = Narray(Float64).new(10,20)
```
makes two-dimensional array of size 10  times 20 of Float 64.

The elements of x can be accessed and assigned using usual [], like

```
  pp! x[1]
  x[2]=5.0
```

and the elements of xy as
```
  pp! xy[1,2]
  x[2,3]=5.0
```


The storage order is in the C convention, not in the Fortran convention.

If you supply -Drange_check (or --define range_check) compiler option,
the code to check the range of indices is generated. This checking is
done through the use of Slice struct, and thus checks only if the
address is outside the range of the array. Thus, in the above example,
x[10,0] would be an error but x[0,20] would not

You can use Narray.range_check? class function to test if range check
is enabled or not.

You can use all member functions supported by Slice. For example, you
can sort the array by x.sort!

A special `each_index` method is available. 
```
   xyz = Narray(Float64).new(10,10,10)
   xyz.each_index{|i,j,k| xyz[i,j,k]= ...}
```
loops over all indices of xyz. For 1 and 2-dimentional arrays, you can
write
```
   x = Narray(Float64).new(10)
   x.each_index{|i| x[i]= ...}
   xy = Narray(Float64).new(10,10)
   xy.each_index{|i,j| xy[i,j]= ...}
```
The each_index(idim) function is also avaiable, which loops over the idim-th dimension.

