---
layout: post
title:  "Write a dictionary in Fortran using hash table"
date:   2020-03-02
categories: Coding Tips
---
Previously, we calculated mass and rounded them into integer in our mass spectrum calculation. Nowadays, the accurate mass calculation becomes more important, but at the same time the method use array index to save mass as integer won't be appropriate. Under this condition, I decide to use hash table to work as dictionary to save mass and intensity as key-value pair.

I found an example on [website](https://github.com/pdebuyl/fortran_hash_table). Here are several problems I encountered:

## Make
GNU make utility is a tool to compile and then build program by the rules you give to it. To use it, you need to write a makefile first.
In ifort complier, `-c` option means to compile to object (.o) only, and do not link.
In this case we have a module and a main function, the right compling sequence should be:
<pre><code>
ifort -c dictionary_m.f90
ifort -c example_from_readme.f90
ifort example_from_readme.o dictionary_m.o
</code></pre>

## Fortran
### allocatable array:
<pre><code>
!correct way:
character(len=16), allocatable :: key_list(:)
! ":" here is a placeholder, need to be declare when allocate()
allocate(key_list(2))

!wrong way:
character(len=(:)), allocatable :: key_list(:)
allocate(key_list(2))
!to correct:
allocate(character(16) :: key_list(2))
</code></pre>
### intrinsic function:
We can't use intrinsic function name as parameter name: `size = SIZE(array)`

