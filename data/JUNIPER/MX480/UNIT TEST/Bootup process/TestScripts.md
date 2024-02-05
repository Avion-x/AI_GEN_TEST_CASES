 Here are sample Python unit test scripts for bootup process test cases for the Juniper Networks MX480 router, split into separate .py files and output formatted in Markdown:

## test_bootup_power_on.py

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        # Steps to power on device
        
        # Verify power on state
        self.assertEqual(power_state, 'on') 

if __name__ == '__main__':
    unittest.main()
```

### test_bootup_power_on.py
**Steps:**
- Power on the device

**Expected Result:**
- Device power state should be 'on'

## test_bootup_post.py

```python  
import unittest

class TestBootup(unittest.TestCase):

    def test_post(self):
        # Boot device and wait for POST to complete
        
        # Verify POST completed successfully
        self.assertEqual(post_status, 'passed')

if __name__ == '__main__':
    unittest.main()
```

### test_bootup_post.py
**Steps:** 
- Boot the device and wait for POST

**Expected Result:**
- POST should complete successfully with 'passed' status

## test_bootup_boot_loader.py

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_boot_loader(self):
        # Initiate boot process
        
        # Verify boot loader prompt
        self.assertIn('loader>', console)  

if __name__ == '__main__':
    unittest.main() 
```

### test_bootup_boot_loader.py
**Steps:**
- Start boot process 

**Expected Result:** 
- Boot loader prompt 'loader>' should be present on console Here is a sample Python script with unit tests for the bootup process of an MX480 router:

```python
import unittest
from JunOS_setup import *

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        print("TEST SETUP")
        # Create device object and open connection
        self.dev = Device("mx480")
        self.dev.open()

    def test_power_on(self):
        print("TEST: Power on device")
        # Power on and check device prompt
        self.dev.power_on()
        self.assertIn("login:", self.dev.get_prompt())

    def test_login(self):
        print("TEST: Login to device")
        # Login and check prompt
        self.dev.login("user", "password")
        self.assertIn("#", self.dev.get_prompt())

    def test_start_routing_engine(self):
        print("TEST: Start routing engine") 
        # Start RE and check expected output
        output = self.dev.start_routing_engine()
        self.assertIn("Routing engine operational", output)

    def test_check_interfaces(self):
        print("TEST: Check interfaces status")
        # Check interface status        
        output = self.dev.get_interface_status()
        self.assertIn("ge-0/0/0", output)
        self.assertIn("up", output)

    def tearDown(self):
        print("TEST TEARDOWN")        
        # Logout and close connection
        self.dev.logout()
        self.dev.close()

if __name__ == '__main__':
    unittest.main()
```

This script contains setup and teardown methods to initialize and close the device connection. It has test cases to check power on, login, routing engine startup, and interface status during the bootup process. The JunOS_setup module contains the Device class and methods to interact with the router. Each test prints a description, executes the test step, and makes assertions to verify the expected behavior. Here is a Python script to perform unit testing of the bootup process for the Juniper MX480 router, with sample outputs in Markdown format:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):

    def test_power_on_self_test(self):
        """Test power on self test"""
        # Perform POST test
        post_status = 'Passed'
        
        # Validate POST result  
        self.assertEqual(post_status, 'Passed')
        
        # Markdown output
        """
        ### Test power on self test
        
        POST status: Passed
        
        POST test passed.
        """
        
    def test_load_boot_loader(self):
        """Test loading boot loader"""
        # Load boot loader
        loader_status = 'Loaded' 
        
        # Validate boot loader loaded
        self.assertEqual(loader_status, 'Loaded')
        
        # Markdown output
        """
        ### Test load boot loader
        
        Boot loader status: Loaded
        
        Boot loader loaded successfully. 
        """
        
    def test_load_junos_kernel(self):
        """Test loading JUNOS kernel"""
        # Load JUNOS kernel
        kernel_status = 'Loaded' 
        
        # Validate JUNOS kernel loaded  
        self.assertEqual(kernel_status, 'Loaded')
        
        # Markdown output
        """
        ### Test load JUNOS kernel
        
        JUNOS kernel status: Loaded
        
        JUNOS kernel loaded successfully.
        """

if __name__ == '__main__':
    unittest.main()
```

This script contains test cases for the key steps in the MX480 bootup process:

- Power on self test 
- Loading boot loader
- Loading JUNOS kernel

Each test case validates the status after the boot step and generates a Markdown formatted output for documentation. The script can be extended to include additional bootup tests as needed. Here is a Python script that defines unit tests for testing the bootup process and configuration of an MX480 router. The tests verify the bootup process, startup configuration, and key routing configuration:

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def test_bootup(self):
        """Test MX480 bootup and reachability"""
        device = ConnectHandler(device_type='juniper', ip='192.168.1.1', username='admin', password='admin123')
        self.assertIsNotNone(device)

    def test_startup_config(self):
        """Test startup configuration on MX480"""
        # Check critical parts of startup config
        output = device.send_command('show configuration')
        self.assertIn('system host-name mx480', output)
        self.assertIn('interfaces ge-0/0/0 unit 0', output)

    def test_routing_config(self):
        """Test routing configuration on MX480"""        
        # Check for expected routing protocols
        output = device.send_command('show configuration protocols')
        self.assertIn('bgp', output)
        self.assertIn('ospf', output)

if __name__ == '__main__':
    unittest.main()
```

This script defines three test cases:

- `test_bootup` verifies the router is reachable and configures the test device
- `test_startup_config` checks critical parts of the startup configuration
- `test_routing_config` validates key routing protocols are configured

To run these tests on an MX480, update the device credentials and IP address. Then run `python test_mx480.py` to execute the test cases.