# narray
A simple library to give (very minimal) functions of multidimensional
array compatible with C/Fortran



## Installation


1. Add the dependency to your `shard.yml`:

   ```yaml
   dependencies:
     narray-crystal:
       github: jmakino/narray-crystal
   ```

2. Run `shards install`


## Getting started
At your project directory (where you ran shards install), try

   crystal lib/narray-crystal/examples/narray_test.cr

should show some output.

  
## Usage

```
  require "narray"
```
provides a Narray class.
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

The elements of x can be accessed and assigned using usial [], like

```
  pp! x[1]
  x[2]=5.0
```

and the elements of xy as
```
  pp! xy[1,2]
  x[2,3]=5.0
```


The storage order is in C convention, not in the Fortran convention.

If you supply -Drange_check (or --define range_check) compiler option,
the code to check the range of indices is generated. This checking is
done through the use of Slice struct, and thus checks only if the
address is outside the range of the array. Thus, in the above example,
x[10,0] would be an error but x[0,20] would not

You can use Nrray.range_check? class function to test if range check
is active or not.

You can use all member functions supported by Slice. For example, you
can sort the array by x.sort!
