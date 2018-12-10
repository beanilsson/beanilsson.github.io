# How to install and run Boost 1.67.0 libraries for C++
... on Ubuntu 18.10
## Download and Unpack
`cd` to the directory where you want to install Boost. I put my installation in `/usr/local`. Then issue this command which will download a compressed `.tar` version of the library: 

`wget https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.bz2` and wait.
 
 Then issue this command to uncompress the file: 
 
 `tar --bzip2 -xf /path/to/boost_1_67_0.tar.bz2` and wait.
## Test program using Boost
Now it's time to test if you were successful with the steps above! Create a `.cpp` file with any name, I chose `example.cpp` (how original). And paste the following code into the file:
```
#include <boost/lambda/lambda.hpp>
#include <iostream>
#include <iterator>
#include <algorithm>

int main()
{
    using namespace boost::lambda;
    typedef std::istream_iterator<int> in;

    std::for_each(
        in(std::cin), in(), std::cout << (_1 * 3) << " " );
}
```
Then build your program with:

`c++ -I path/to/boost_1_67_0 example.cpp -o example`

If no errors occur, test and run the program using:

`echo 1 2 3 | ./example`

Which should print `3 6 9`.


[Source](https://www.boost.org/doc/libs/1_68_0/more/getting_started/unix-variants.html)
