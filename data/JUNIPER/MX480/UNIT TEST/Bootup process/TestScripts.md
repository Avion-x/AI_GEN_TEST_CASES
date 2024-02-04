 Here are sample Python unit test scripts for testing the bootup process on the Juniper Networks MX480 router, saved as separate files and output in Markdown format:

## test_bootup.py

```python
import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.is_powered_on())
    
    def test_load_bios(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.bios_loaded())
        
    def test_boot_loader(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.bootloader_loaded())

    def test_kernel_load(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.kernel_loaded())

    def test_init_process(self):
        router = MX480()
        router.power_on() 
        self.assertTrue(router.init_complete())

if __name__ == '__main__':
    unittest.main()
```

## test_interfaces.py

```python
import unittest
from router import MX480

class TestInterfaces(unittest.TestCase):

    def test_check_interfaces(self):
        router = MX480()
        router.power_on()
        interfaces = router.get_interfaces()
        self.assertGreater(len(interfaces), 0)

    def test_interface_status(self):
        router = MX480()
        router.power_on()
        for intf in router.get_interfaces():
            self.assertEqual(intf.get_status(), 'up')

if __name__ == '__main__':
   unittest.main()
```

## test_routing.py

```python
import unittest
from router import MX480

class TestRouting(unittest.TestCase):

    def test_routing_table(self):
        router = MX480()
        router.power_on()
        routes = router.get_routing_table()
        self.assertGreater(len(routes), 0)
    
    def test_static_routes(self):
        router = MX480()
        router.power_on()
        static_routes = router.get_static_routes()
        self.assertGreater(len(static_routes), 0)

    def test_ospf_neighbors(self):
        router = MX480()
        router.power_on()
        ospf_neighbors = router.get_ospf_neighbors()
        self.assertGreater(len(ospf_neighbors), 0)

if __name__ == '__main__':
    unittest.main()
```

This provides sample unit tests for the bootup process, interfaces, and routing on an MX480 router. The tests could be expanded to cover additional cases. Here is the Python script with unit tests for the bootup process of an MX480 router in separate files for each test case, formatted in Markdown:

## test_bootup.py

```python
import unittest
from router import MX480

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        self.router = MX480()

    def test_power_on(self):
        self.router.power_on()
        self.assertTrue(self.router.is_powered_on())

    def test_load_bios(self):
        self.router.power_on()
        self.router.load_bios()
        self.assertTrue(self.router.bios_is_loaded())

    def test_boot_loader(self):
        self.router.power_on()
        self.router.load_bios()
        self.router.start_boot_loader()
        self.assertTrue(self.router.boot_loader_started())

    def test_load_junos(self):
        self.router.power_on()
        self.router.load_bios()
        self.router.start_boot_loader()
        self.router.load_junos()
        self.assertTrue(self.router.junos_is_loaded())

    def test_boot_complete(self):
        self.router.power_on()
        self.router.load_bios()
        self.router.start_boot_loader()
        self.router.load_junos()
        self.router.complete_boot()
        self.assertTrue(self.router.is_fully_booted())

    def tearDown(self):
        self.router.power_off()

if __name__ == '__main__':
    unittest.main()
```

This script contains test cases for each step of the MX480 bootup process:

- Power on 
- Load BIOS
- Start boot loader
- Load Junos OS
- Complete bootup

Each test case sets up the router, executes the step being tested, verifies the expected state, and then tears down the router after all tests complete. The tests can be run by invoking `unittest.main()`.

## test_power_on.py

```python 
import unittest
from router import MX480

class TestMX480PowerOn(unittest.TestCase):

    def test_power_on(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.is_powered_on())

if __name__ == '__main__':
    unittest.main()
```

Focused unit test for just the power on functionality.

## test_load_bios.py

```python
import unittest 
from router import MX480

class TestMX480LoadBIOS(unittest.TestCase):
    
    def test_load_bios(self):
        router = MX480()
        router.power_on()
        router.load_bios()
        self.assertTrue(router.bios_is_loaded())
        
if __name__ == '__main__':
    unittest.main()
```

Focused unit test for just the BIOS loading functionality.

And so on for each step... Here is a Python script with unit tests for the bootup process of the Juniper MX480 router:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):

    def test_power_on(self):
        """Test powering on the router"""
        # Simulate turning on power 
        print("Power on test: PASS")
        self.assertTrue(True)

    def test_boot_loader(self):
        """Test loading boot loader"""
        # Simulate loading boot loader
        print("Boot loader test: PASS") 
        self.assertTrue(True)

    def test_kernel_load(self):
        """Test loading kernel"""
        # Simulate loading kernel
        print("Kernel load test: PASS")
        self.assertTrue(True)

    def test_init_process(self):
        """Test initializing processes""" 
        # Simulate initializing processes
        print("Init process test: PASS")
        self.assertTrue(True)

    def test_daemons_start(self):
        """Test starting daemons"""
        # Simulate starting daemons
        print("Daemons start test: PASS")
        self.assertTrue(True)

    def test_network_interfaces(self):
        """Test initializing network interfaces"""
        # Simulate initializing network interfaces
        print("Network interfaces test: PASS")
        self.assertTrue(True)

    def test_routing_protocols(self):
        """Test starting routing protocols"""
        # Simulate starting routing protocols
        print("Routing protocols test: PASS")
        self.assertTrue(True)

if __name__ == '__main__':
    unittest.main()
```

This script defines a TestMX480Bootup class with unit tests for each major step in the bootup process. The tests simply print a "PASS" message and return True to simulate a passing test. In practice, each test would validate the expected state after that boot step. This can be run with `python test_mx480_bootup.py` which will execute the tests and print the results. Here is a python script that could be used for unit testing the bootup process on an MX480 router. It checks the bootup logs, verifies the startup configuration, and validates key routing information. The script is split into separate test functions for each aspect of the bootup validation. The output is formatted in Markdown.

```python
import re
import json
from junos import Device

def test_bootup_logs():
    """Check bootup logs for errors"""

    logs = get_bootup_logs()
    
    # Search logs for errors
    errors = re.search("error", logs, re.I)
    
    if errors:
        print("## Bootup Logs Test: FAIL")
        print("Errors found in bootup logs:") 
        print(errors.group())
    else: 
        print("## Bootup Logs Test: PASS")
        print("No errors found in bootup logs")

def test_startup_config():
    """Verify startup configuration"""
    
    dev = Device('mx480')
    dev.open()
    config = dev.cli('show configuration')
    dev.close()

    # Check for expected config lines
    if re.search('interfaces ge-0/0/0', config):
        print("## Startup Config Test: PASS")
        print("Startup config contains expected interfaces")
    else:
        print("## Startup Config Test: FAIL")
        print("Expected interfaces missing from startup config")

def test_routing_table():
    """Validate routing table"""

    dev = Device('mx480')
    dev.open()
    routes = json.loads(dev.cli('show route json'))
    dev.close()

    # Check for presence of default route
    has_default = False
    for route in routes['routing-table']:
        if route['rt-destination'] == '0.0.0.0/0':
            has_default = True
            break

    if has_default:
        print("## Routing Table Test: PASS")
        print("Routing table has default route")
    else:
        print("## Routing Table Test: FAIL")
        print("Default route not found in routing table")

test_bootup_logs()
test_startup_config() 
test_routing_table()
```

This provides a basic structure for unit testing the bootup process on the MX480 and verifying the configuration. Additional tests could be added to validate other aspects of the bootup as needed.