 Here are sample unit test scripts for testing the bootup process on the Juniper Networks MX480 router, separated into individual .py files and output formatted in Markdown:

### test_power_on.py

```python
import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        router = MX480()
        self.assertFalse(router.is_powered_on()) 
        router.power_on()
        self.assertTrue(router.is_powered_on())
```

### test_load_bios.py 

```python
import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_load_bios(self):
        router = MX480()
        router.power_on()
        self.assertFalse(router.bios_loaded())
        router.load_bios()
        self.assertTrue(router.bios_loaded()) 
```

### test_boot_loader.py

```python
import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_boot_loader(self):
        router = MX480()
        router.power_on()
        router.load_bios()
        self.assertFalse(router.boot_loader_running())
        router.start_boot_loader()
        self.assertTrue(router.boot_loader_running())
```

### test_load_junos.py

```python 
import unittest
from router import MX480

class TestBootup(unittest.TestCase):
    
    def test_load_junos(self):
        router = MX480()
        router.power_on()
        router.load_bios()
        router.start_boot_loader()
        self.assertFalse(router.junos_loaded())
        router.load_junos()
        self.assertTrue(router.junos_loaded())
```

This provides sample unit tests to validate each stage of the bootup process for the Juniper MX480 router. The tests could be expanded to include additional validation as needed. Here is a python script with unit tests for the bootup process of an MX480 router, with each test case including setup, execution, verification, and teardown steps:

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        self.device = {
            'device_type': 'juniper',
            'host': 'mx480.example.com',
            'username': 'netconf',
            'password': 'juniper!123',
        }
        
    def tearDown(self):
        print("Test completed\n")
                
    def test_power_on(self):
        print("\nTest case: Power on device") 
        net_connect = ConnectHandler(**self.device)
        net_connect.send_command("request system power-off")
        net_connect.send_command("request system power-on")
        output = net_connect.send_command("show chassis environment")
        self.assertIn("Temp", output)
        print("Verified - Device powered on successfully")
        
    def test_login(self):
        print("\nTest case: Login to device")
        net_connect = ConnectHandler(**self.device)
        output = net_connect.send_command("show version")
        self.assertIn("Juniper Networks", output)
        print("Verified - Able to login successfully")

    def test_routing_engine_status(self):
        print("\nTest case: Verify routing engine status")
        net_connect = ConnectHandler(**self.device)
        output = net_connect.send_command("show chassis routing-engine")
        self.assertIn("Current state", output) 
        self.assertIn("Master", output)
        print("Verified - Routing engines in master state")
        
if __name__ == '__main__':
    unittest.main()
```

This provides three test cases:

1. Power on the device
2. Login to the device 
3. Verify routing engine status

Each test has a setup and teardown steps, executes a command, validates the output, and prints a verification message. The tests can be executed by running `python test_mx480.py`. Here is a Python script for unit testing the bootup process of the MX480 router in separate files with Markdown formatted output:

## test_bootup.py

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        """Test powering on the device"""
        print("## Power On")        
        print(" - Power on the device")
        self.assertTrue(power_on())

    def test_bios_post(self):
        """Test BIOS POST"""
        print("## BIOS POST")        
        print(" - Verify BIOS POST completes successfully")
        self.assertTrue(bios_post_success())

    def test_loader_boot(self):
        """Test loader booting correctly"""
        print("## Loader Boot")
        print(" - Verify loader boots properly")
        self.assertTrue(loader_boot_success())

    def test_kernel_boot(self):
        """Test kernel booting correctly"""
        print("## Kernel Boot")
        print(" - Verify kernel boots properly")
        self.assertTrue(kernel_boot_success())

    def test_routing_engine_online(self):
        """Test routing engine coming online""" 
        print("## Routing Engine Online")
        print(" - Verify routing engine comes online")
        self.assertTrue(routing_engine_online())

    def test_protocol_daemons(self):
        """Test protocol daemons start correctly"""
        print("## Protocol Daemons")
        print(" - Verify key protocol daemons start properly")
        self.assertTrue(protocol_daemons_start())

if __name__ == '__main__':
    unittest.main()
```

This script contains test cases for each major step in the bootup process. The tests print Markdown headers and text to provide formatted output. The assertions use mock functions that would need to be implemented to actually validate the bootup steps. Here are sample Python unit test scripts in separate files to test the bootup process and verify configuration on an MX480 router. The scripts use pytest and provide sample test cases and assertions.

```python
# test_bootup.py

import pytest
from router import MX480

@pytest.fixture
def router():
    return MX480()

def test_bootup(router):
    assert router.boot_status == "Ready"
    assert router.interfaces["ge-0/0/0"].is_up()

def test_config(router):  
    assert router.has_config("system host-name mx480")
    assert router.has_config("interfaces ge-0/0/0 unit 0")
```

```python  
# test_interfaces.py

from router import MX480

def test_interface_status(router):
    assert router.interfaces["ge-0/0/0"].is_up()
    assert not router.interfaces["ge-0/0/1"].is_up() 

def test_interface_config(router):
    assert router.interfaces["ge-0/0/0"].has_config("unit 0 family inet address 1.1.1.1/24")
```

The output in Markdown format:

# Unit Tests

## test_bootup.py

- `test_bootup` - Checks boot status and interface status
- `test_config` - Checks hostname and interface configuration

## test_interfaces.py  

- `test_interface_status` - Checks interface up/down status
- `test_interface_config` - Checks interface configuration