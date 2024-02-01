 Here are sample Python unit test scripts for bootup process test cases for the Juniper Networks MX480 router, split into separate Python files and with markdown formatted output:

## test_bootup_power_on.py

```python
import unittest

class TestBootupPowerOn(unittest.TestCase):

    def test_power_on(self):
        """Test powering on the device"""

        # Test steps to power on device
        self.assertTrue(power_on_device())

        # Assert device is powered on
        self.assertEqual(get_device_power_status(), 'ON')

```

## test_bootup_load_bios.py  

```python
import unittest

class TestBootupLoadBIOS(unittest.TestCase):

    def test_load_bios(self):
        """Test BIOS loading during bootup"""

        # Assume device is already powered on

        # Allow some time for BIOS to load
        wait_for_bios_load()
        
        # Check BIOS version
        bios_version = get_bios_version()
        self.assertEqual(bios_version, 'EXPECTED_VERSION')

```

## test_bootup_load_os.py

```python  
import unittest

class TestBootupLoadOS(unittest.TestCase):

    def test_load_os(self):
        """Test OS loading during bootup"""
        
        # Assume device is powered on and BIOS is loaded
        
        # Initiate bootup 
        start_device_boot()

        # Wait for OS to finish loading
        wait_for_os_load()

        # Check OS version
        os_version = get_os_version()
        self.assertEqual(os_version, 'EXPECTED_VERSION')
        
```

This provides sample unit tests for power on, BIOS load and OS load stages of the bootup process for the MX480 router. The tests are split into separate Python files and output in Markdown format. Here is a sample python script with unit tests for the bootup process of the MX480 router, with test cases for the main steps:

```python
import unittest
from junos import Device

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        self.dev = Device(host='mx480', user='testuser', password='test123')
        self.dev.open()
    
    def test_power_on(self):
        print('## Test: Power on device')
        # Steps to power on device
        # Verify device boots to loader prompt
    
    def test_load_image(self):
        print('## Test: Load system image')  
        # Commands to load system image
        # Verify image is loaded successfully

    def test_boot_image(self):
        print('## Test: Boot into loaded image')
        # Command to boot into loaded image
        # Verify device boots into image

    def test_verify_bootup(self):
        print('## Test: Verify successful bootup')
        # Commands to verify successful boot 
        # e.g. show version
        # Verify expected output  

    def tearDown(self):
        self.dev.close()
        
if __name__ == '__main__':
    unittest.main()
```

The script contains setup and teardown methods to initialize and close the device connection. 

Each test case prints the test name, contains steps to execute the test, and verification steps to validate the results. 

The tests cover:

- Powering on the device 
- Loading the system image
- Booting into the loaded image
- Verifying successful bootup

This provides a template to build upon for complete bootup testing. The steps and verification can be expanded with real commands, expected output, assertions, etc. Here is a Python script to unit test the bootup process of an MX480 router in markdown format:

## Unit Test Script for MX480 Bootup Process

```python
import unittest
from router import MX480

class TestMX480Bootup(unittest.TestCase):

    def test_power_on_self_test(self):
        """Test power on self test"""
        router = MX480()
        router.power_on()
        self.assertEqual(router.status, "Running power on self test")

    def test_load_bios(self):
        """Test BIOS loading"""
        router = MX480()
        router.power_on()
        router.post() 
        self.assertEqual(router.status, "BIOS loaded successfully")

    def test_load_bootloader(self):
        """Test bootloader loading"""
        router = MX480()
        router.power_on()
        router.post()
        router.load_bootloader()
        self.assertEqual(router.status, "Bootloader loaded successfully")

    def test_load_junos(self):
        """Test Junos OS loading"""
        router = MX480()
        router.power_on()
        router.post()
        router.load_bootloader()
        router.load_junos()
        self.assertEqual(router.status, "Junos OS loaded successfully")

    def test_verify_interfaces(self):
        """Test interface initialization""" 
        router = MX480()
        router.power_on()
        router.post()
        router.load_bootloader()
        router.load_junos()
        interfaces = router.get_interfaces()
        self.assertGreater(len(interfaces), 0)

if __name__ == '__main__':
    unittest.main()
```

This script imports the `unittest` module and creates a `TestMX480Bootup` class that inherits from `unittest.TestCase`. 

It defines test methods to validate each stage of the bootup process:

- Power on self test
- BIOS loading
- Bootloader loading  
- Junos OS loading
- Interface initialization

Each test initializes an MX480 router instance, performs the relevant bootup steps, and validates the expected status after each step.

The `main` block runs the test suite if the script is executed directly. Here is a python script that runs unit tests for the bootup process on the MX480 router to verify configuration. The tests are separated into individual files for each test case:

```python
# test_bootup.py

import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def setUp(self):
        self.router = MX480()

    def test_boot_sequence(self):
        self.router.power_on()
        self.assertEqual(self.router.get_state(), 'loading_boot_config')
        
        self.router.load_boot_config()
        self.assertEqual(self.router.get_state(), 'applying_boot_config')
        
        self.router.apply_boot_config()
        self.assertEqual(self.router.get_state(), 'ready')

    def test_saved_config(self):
        self.assertEqual(self.router.get_config(), 'saved_config.txt')

if __name__ == '__main__':
    unittest.main()
```

```python
# test_interfaces.py 

import unittest
from router import MX480

class TestInterfaces(unittest.TestCase):

    def setUp(self):
        self.router = MX480()

    def test_interface_count(self):
        num_interfaces = len(self.router.get_interfaces())
        self.assertEqual(num_interfaces, 48)

    def test_interface_status(self):
        for intf in self.router.get_interfaces():
            self.assertEqual(intf.get_status(), 'up')

if __name__ == '__main__':
   unittest.main()
```

```python
# test_routing.py

import unittest 
from router import MX480

class TestRouting(unittest.TestCase):

    def setUp(self):
        self.router = MX480()

    def test_routing_table(self):
        routing_table = self.router.get_routing_table()
        self.assertIn('10.0.0.0/24', routing_table)
        self.assertIn('192.168.1.0/24', routing_table)
    
    def test_static_routes(self):
        static_routes = self.router.get_static_routes()
        self.assertIn('172.16.0.0/16', static_routes)
        self.assertIn('10.20.30.0/24', static_routes)

if __name__ == '__main__':
    unittest.main()
```

This provides three test files (test_bootup.py, test_interfaces.py, test_routing.py) that each focus on testing a specific area of the bootup process and configuration. The tests can be run independently or together to provide full test coverage.