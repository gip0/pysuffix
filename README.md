# pysuffix
Automatically exported from code.google.com/p/pysuffix

pysuffix : a python implementation for efficient augmented suffix array construction.
What does it do?
Usage
Pysuffix v2.1
Bench pysuffix please
Pysuffix v2.0
Pysuffix v1.0
See also
What does it do ?
Let's start with a string S = 'abcdabcd' You can represent S in that way :

a	b	c	d	a	b	c	d	$
0	1	2	3	4	5	6	7	8
, where '$' is the smallest letter in the alphabet used to write S.

Each offset can be seen as a suffix of the string S. For exemple, in S :

offset	suffix
0	abcdabcd$
1	bcdabcd$
2	cdabcd$
3	dabcd$
4	abcd$
5	bcd$
6	cd$
7	d$
8	$
Pysuffix computes for you the augmented suffix array as follow :

i	lcp	offset	suffix
0	0	8	$
1	4	4	abcd$
2	0	0	abcdabcd$
3	3	5	bcd$
4	0	1	bcdabcd$
5	2	6	cd$
6	0	2	cdabcd$
7	1	7	d$
8	0	3	dabcd$
suffix_array = (4, 0, 5, 1, 6, 2, 7, 3) lcp = (4, 0, 3, 0, 2, 0, 1, 0)

Usage
>user@machina tar -xzvf pysuffix.2.1.tar.gz
>user@machina python suffix_array.test.py
Pysuffix v2.1
Inside suffix_array.test.py
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import tools_karkkainen_sanders as tks

s = 'abab'
s_unicode = unicode(s,'utf-8','replace')
sa = simple_kark_sort(s_unicode)
lcp = tks.LCP(s,sa)
print sa
print lcp
print :

[2, 0, 3, 1, 0, 0, 0] #suffix_array
[2, 0, 1, 0] #longest common prefixes
lcp[i] : longest common prefix between sa[i] and sa[i+1]

You surely only be interested in sa[0:n], where n is the length of s :

[2, 0, 3, 1]
Bench pysuffix please
Tests are done with an Intel Atom N280 (benchmarking with mini-pc is so fun). The string used for the benchs is

str = 'a' * len
Runs with Python :

bench_pysuffix



Runs with Pypy :

bench_pysuffix

Pysuffix v2.0
Inside suffix_array.test.py
#!/usr/bin/env python
# -*- coding: utf-8 -*-

from tools_karkkainen_sanders import *

s = 'abcdabcd'
s_unicode = unicode(s,'utf-8','replace')
sa = simple_kark_sort(s_unicode)
print sa
print :

[4, 0, 5, 1, 6, 2, 7, 3, 0, 0, 0]
You surely only be interested in sa[0:n], where n is the length of s :

[4, 0, 5, 1, 6, 2, 7, 3]
Pysuffix v1.0
Inside suffix_array.test.py
Some imports

#!/usr/bin/env python
# -*- coding: utf-8 -*-

from string import *
from StringIO import StringIO
from tools import *
from suffix_array import Suffix_array
import sys
Prepare string in unicode

str = 'abcabc'
str_unicode = utf82unicode(str)
Create Suffix_array and feed it with unicode strings. Here, twice 'abcabc'.

sa1 = Suffix_array()
sa1._add_str(str_unicode)
sa1._add_str(str_unicode)
Run the Karkkaïnen and Sanders sort

sa1.karkkainen_sort()
Write the 5th letters of each suffix in a sorted order

sa1._write_su_n(5)
Or you can simply access to the sorted suffix array

sorted = sa1.suffix_array
See also
py-rstr-max : maximum repeats in strings detection for python users
And also
linsuffarr.py
