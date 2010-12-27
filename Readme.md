This is beanstalkd, a fast, general-purpose work queue.

See http://xph.us/software/beanstalkd/ for general info.

To build beanstalkd, type "./configure" then "make". (You might need to type
"gmake"; our build requires GNU make.)

Requires libevent 1.4.1 or later. You can find libevent at
http://www.monkey.org/~provos/libevent/.

To install, copy the file "beanstalkd" anywhere you like.

See doc/protocol.txt for details of the on-the-wire protocol.

## Running Tests

To run unit tests, type "make check".

These unit tests use a slightly modified bundled version of CUT, originally
from http://sourceforge.net/projects/cut/.

## Writing Tests

There are two kinds of tests here: unit tests and shell tests.

### Unit Tests

These go in `tests/test_*.c`. See the CUT documentation for more info.

http://sourceforge.net/projects/cut/

## Shell Tests

Shell tests go in the sh-tests directory and are to be written in pairs:

 - `my_test.commands`
 - `my_test.expected`

Each .commands file will be nc'd to beanstalkd, and the response diff'd
with the appropriate .expected file.  If the response is not identical to the
.expected file, the test fails.  At the moment, the test harness bails upon the
first failure, but it could easily be extended to finish the tests and print
full results.

IMPORTANT: Since beanstalkd expects \r\n line endings, you must be sure to
include those in your files.  You can tell vim to do this with

    :set ff=dos
