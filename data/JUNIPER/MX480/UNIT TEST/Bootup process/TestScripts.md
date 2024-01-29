 Here are sample Python unit test scripts for testing the bootup process on a Juniper Networks MX480 router, separated into individual files:

```python
# test_bootup_poweron.py

import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        router = MX480()
        self.assertFalse(router.is_powered_on()) 
        router.power_on()
        self.assertTrue(router.is_powered_on())

if __name__ == '__main__':
    unittest.main()
```

```python
# test_bootup_bios.py  

import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_bios_post(self):
        router = MX480()
        router.power_on()
        self.assertFalse(router.bios_is_post())
        router.bios_post()
        self.assertTrue(router.bios_is_post())

if __name__ == '__main__':
    unittest.main()
```

```python
# test_bootup_loader.py

import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_loader(self):
        router = MX480()
        router.power_on()
        router.bios_post()
        
        self.assertFalse(router.loader_is_running())
        router.load_loader()
        self.assertTrue(router.loader_is_running())

if __name__ == '__main__':
    unittest.main() 
```

```python
# test_bootup_kernel.py

import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_kernel(self):
        router = MX480()
        router.power_on()
        router.bios_post()
        router.load_loader()
        
        self.assertFalse(router.kernel_is_running())
        router.load_kernel()
        self.assertTrue(router.kernel_is_running())
        
if __name__ == '__main__':
    unittest.main()
```

This provides sample unit tests for power on, BIOS POST, loader, and kernel boot stages. The tests could be expanded with additional assertions and checks as needed. Here is a markdown formatted python script with unit tests for the bootup process of an MX480 router:

```python
# test_mx480_bootup.py

import unittest
from router import MX480

class TestMX480BootUp(unittest.TestCase):

    def setUp(self):
        self.router = MX480()

    def test_power_on(self):
        # Power on 
        self.router.power_on()

        # Verify power LED is lit
        self.assertTrue(self.router.power_led)

    def test_post(self):
        # Power on 
        self.router.power_on()

        # Verify POST completes successfully 
        self.assertTrue(self.router.post_complete)

    def test_load_junos(self):
        # Power on
        self.router.power_on()

        # Verify Junos boots successfully
        self.assertTrue(self.router.junos_booted)

    def test_load_config(self):
        # Power on
        self.router.power_on()

        # Load configuration
        self.router.load_config("config.txt")

        # Verify configuration loaded successfully
        self.assertTrue(self.router.config_loaded)

    def tearDown(self):
        # Power off router after each test
        self.router.power_off() 

if __name__ == '__main__':
    unittest.main()
```

This script contains setup code to instantiate the MX480 router object, individual test cases for power on, POST, Junos boot, and configuration load, teardown to power off the router after each test, and a main block to run the unit tests. The test cases use assertions to verify the expected behavior at each step of the bootup process. Here is a Python script with unit tests for the bootup process of the Juniper MX480 router, output in Markdown format:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):

    def test_power_on(self):
        """Test powering on the device"""
        print("### Power On")
        # Test steps to power on device
        self.assertEqual(power_status, "on")

    def test_bootloader(self):
        """Test loading bootloader""" 
        print("### Load Bootloader")
        # Test steps to load bootloader
        self.assertEqual(bootloader_status, "loaded")

    def test_kernel_load(self):
        """Test loading kernel"""
        print("### Load Kernel")
        # Test steps to load kernel
        self.assertEqual(kernel_status, "loaded") 

    def test_init_process(self):
        """Test init process"""
        print("### Init Process")
        # Test steps for init process
        self.assertEqual(init_status, "complete")

    def test_daemons_startup(self):
        """Test starting daemons"""
        print("### Start Daemons")
        # Test steps for starting required daemons
        self.assertEqual(daemons_status, "running")

    def test_interface_initialization(self):
        """Test initializing interfaces"""
        print("### Initialize Interfaces")
        # Test steps for initializing interfaces
        self.assertEqual(interfaces_status, "ready")

    def test_routing_protocols_start(self):
        """Test starting routing protocols"""
        print("### Start Routing Protocols")
        # Test steps for starting required routing protocols
        self.assertEqual(routing_protocols_status, "running")  

if __name__ == '__main__':
    unittest.main()
```

This implements test cases for the major steps in the MX480 bootup process like power on, loading bootloader, kernel, init process, daemons startup, interface initialization, and routing protocol startup. The test steps and assertions would need to be implemented according to the actual bootup flow. Here is a python script that creates a separate test file for each unit test for the bootup process on the MX480 router:

```python
import os

# List of tests
tests = [
    'Test boot config',
    'Test interfaces up', 
    'Test BGP neighbors',
    'Test OSPF neighbors'
]

# Create test files
for test in tests:
    # Create file
    test_file = f'test_{test.lower().replace(" ", "_")}.md'
    with open(test_file, 'w') as f:
        f.write(f'# {test}\n')
        f.write('\n')
        f.write('## Test Steps\n')
        f.write('\n')
        f.write('## Expected Results\n')
        f.write('\n')
        f.write('## Actual Results\n')
        f.write('\n')
        f.write('## Pass/Fail\n')
        
    print(f"Created test file: {test_file}")
```

This will generate the following test files:

- test_boot_config.md
- test_interfaces_up.md  
- test_bgp_neighbors.md
- test_ospf_neighbors.md

Each file contains markdown headers for the test name, test steps, expected results, actual results, and pass/fail status. These can be updated with the actual test details during verification.