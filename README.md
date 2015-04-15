Container::INI
=====

Container::INI -  Construct deeply nested perl data structures in INI format
* multiline values
* dot notation
* array detection

Quick Start
=====
* Headers are embedded between brackets []
* Nested hash keys included in headers are delimited by ::
* Like traditional INI files, keys and values are delimited by the equality operator =
* Unlike traditional INI parsers, dot notation can be used in key values to nest hash keys
* Comma separated values are detected as arrays
* Multiline values are permitted, lines must terminate with a backslash \


```
# config
[header::example::1]
address.street=1 Individual Way
address.city=Your Town
address.state=Your State
address.zip=Your Zip
name.first=Rajendra
name.last=Prashad
os.unix.linux=Debian, Centos, Gentoo, Mint
os.unix.bsd=FreeBSD, NetBSD, OpenBSD

# code
use Container::INI;
use Data::Dumper;

my $ini = new Container::INI("example1.ini");
print Dumper $ini->get_config;

# output

$VAR1 = {
          'header' => {
                        'example' => {
                                       '1' => {
                                                'name' => {
                                                            'first' => 'Rajendra',
                                                            'last' => 'Prashad'
                                                          },
                                                'address' => {
                                                               'zip' => 'Your Zip',
                                                               'city' => 'Your Town',
                                                               'street' => '1 Individual Way',
                                                               'state' => 'Your State'
                                                             },
                                                'os' => {
                                                          'unix' => {
                                                                      'bsd' => [
                                                                                 'FreeBSD',
                                                                                 'NetBSD',
                                                                                 'OpenBSD'
                                                                               ],
                                                                      'linux' => [
                                                                                   'Debian',
                                                                                   'Centos',
                                                                                   'Gentoo',
                                                                                   'Mint'
                                                                                 ]
                                                                    }
                                                        }
                                              }
                                     }
                      }
        };
```
