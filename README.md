# ballade

Current version: 0.95.3

Ballade is a light weight http proxy based on tornado and an upstream proxy switcher using [SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega) rules 

Ballade means ballade tempo, not that fast ~

This project is originally based on [tornado-proxy-server](https://github.com/thinxer/tornado-proxy-server) project

Support for python 3.4 and above, python 3.0 to 3.3 are not tested

Because of os.fork() issue, ballade use only one process when runing on windows

# Features and improvements

+ IPv6 over HTTP proxy support, especially for **CERNET IPv6** users
+ HTTP, SOCKS5 upstream proxy support
+ TLS and HTTP protocols support
+ Switch rules include virtual profile support
+ Multiprocess support
+ Some bugs fixed

## Usages

Install from pypi by pip3:

    pip3 install ballade # If you are a linux user, you may need to run as root to add  this program to /usr/local/bin/
    
Or install from source:

    git clone https://github.com/holyshawn/ballade
    cd ballade
    python3 setup.py install
    
After install, just run

    ballade # Start with the default config directory -> $HOME($HOMEPATH)/.config/ballade
    ballade -c /home/xxx/.config/ballade # Use your own config directory

###  Configuration Syntax

Configuration file is "config.yaml":

```yaml
bind:
  address: '0.0.0.0'
  port: 8080
# Keys and values must match the omega rule
proxy:
  profile:
    first: 'http://127.0.0.1:12345'
    second: 'socks5://127.0.0.1:23456'
    direct: 'direct://'
  # Virtual profile as alias
  virtual:
    speed: "first"
omega_file: 'omega.conf'
# Use to test IPv6 connection
ipv6_test:
  host: 'www.yahoo.com'
  port: 443
```

Rules file "omega.conf":

The rules file should be imported from SwitchyOmega

You can also make your own conf

```
[SwitchyOmega Conditions]
@with result

*.cloudflare.com +first
*.t.co +second

* +direct
```

## To Do

+ Authentication

## Acknowledgements

+ @thinxer: the author of the original project

## License

This project is under the MIT License. See the [LICENSE](https://github.com/holyshawn/ballade/blob/master/LICENSE) file for the full license text
