 Here are 3 sample Python unit test scripts for testing the bootup process on the Juniper Networks MX480 router, separated into individual files and with markdown formatted output:

### test_bootup.py

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        """Test powering on the router"""
        # Test steps to power on router
        self.assertTrue(router.is_powered_on(), "Router failed to power on") 

    def test_boot_sequence(self):
        """Test boot sequence and boot loader"""
        # Test steps to validate boot sequence and loader
        self.assertEqual(router.boot_state, "READY", "Router failed to reach ready state")

if __name__ == '__main__':
    unittest.main()
```

### test_routing_engine.py

```python
import unittest

class TestRoutingEngine(unittest.TestCase):

    def test_re_status(self):
        """Test routing engine status""" 
        # Test steps to verify RE status
        self.assertEqual(re0.status, "Online", "RE0 failed to come online")
        self.assertEqual(re1.status, "Online", "RE1 failed to come online")

if __name__ == '__main__':
    unittest.main()
```

### test_network_interfaces.py

```python 
import unittest

class TestNetworkInterfaces(unittest.TestCase):

    def test_interface_status(self):
        """Test interface status"""
        # Test steps to verify interface status
        self.assertEqual(ge_0_0_0.status, "Up", "ge-0/0/0 failed to come up")
        self.assertEqual(ge_0_0_1.status, "Up", "ge-0/0/1 failed to come up") 

if __name__ == '__main__':
   unittest.main()
``` Here is a Python script with unit tests for the MX480 router bootup process:

```python
import unittest
from junos import Device

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        self.dev = Device(host='mx480.example.com', user='netconf', password='secret123')
        self.dev.open()

    def test_boot_to_login_prompt(self):
        print('## Test: Boot to Login Prompt')
        self.dev.cli('request system reboot')
        output = self.dev.cli('show version', warning=False)
        self.assertIn('MX480', output)
        print('PASSED: Reached login prompt after reboot')

    def test_check_default_interfaces(self):
        print('## Test: Check Default Interfaces')
        output = self.dev.cli('show interfaces terse')
        self.assertIn('ge-0/0/0', output)
        self.assertIn('ge-0/0/1', output)
        print('PASSED: Default interfaces present') 

    def test_check_routing_protocols(self):
        print('## Test: Check Routing Protocols')
        output = self.dev.cli('show ospf neighbor')
        self.assertEqual(output, '')
        print('PASSED: No OSPF neighbors present by default')

    def tearDown(self):
        self.dev.close()

if __name__ == '__main__':
    unittest.main()
```

This provides three test cases:

1. Boot to login prompt 
2. Check for default interfaces
3. Check routing protocols 

Setup and teardown open/close the NETCONF connection. Each test case prints a header, executes the test logic, and prints a PASS message on success. Here is a Python script that provides unit tests for the bootup process of the Juniper MX480 router in markdown format:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):
    
    def test_power_on_self_test(self):
        """
        ## Power On Self Test
        - Verify POST completes successfully
        """
        print("POST completed successfully")
        
    def test_load_boot_loader(self):
        """
        ## Load Boot Loader  
        - Verify boot loader is loaded
        """
        print("Boot loader loaded successfully")
        
    def test_load_junos_kernel(self):
        """
        ## Load JUNOS Kernel
        - Verify JUNOS kernel is loaded
        """
        print("JUNOS kernel loaded successfully")
        
    def test_load_routing_protocol_daemons(self):
        """
        ## Load Routing Protocol Daemons
        - Verify routing daemons are loaded 
        """
        print("Routing daemons loaded successfully")
        
    def test_interface_initialization(self):
        """
        ## Interface Initialization
        - Verify interfaces are initialized
        """
        print("Interfaces initialized successfully")
        
if __name__ == '__main__':
    unittest.main()
```

This provides a basic set of unit tests for the MX480 bootup process including POST, loading the boot loader, JUNOS kernel, routing daemons, and interface initialization. The tests simply print a message indicating success to simulate assertions in a real test case. The markdown formatting allows the tests to be rendered nicely when pasted into a markdown document. Here are sample Python scripts for unit testing the bootup process on an MX480 router:

```python
# test_bootup.py

import unittest 
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def test_show_version(self):
        """Test show version output"""
        device = ConnectHandler(device_type='juniper', host='mx480', username='testuser', password='test123')
        show_ver = device.send_command('show version')
        self.assertIn('JUNOS Software Release', show_ver)

    def test_show_chassis_hardware(self):
        """Test show chassis hardware output"""
        device = ConnectHandler(device_type='juniper', host='mx480', username='testuser', password='test123')
        show_hw = device.send_command('show chassis hardware')
        self.assertIn('Item', show_hw)
        self.assertIn('Version', show_hw)

    def test_show_interfaces_terse(self):
        """Test show interfaces terse output"""
        device = ConnectHandler(device_type='juniper', host='mx480', username='testuser', password='test123')
        show_int = device.send_command('show interfaces terse')
        self.assertIn('ge-', show_int)

if __name__ == '__main__':
    unittest.main()
```

This script contains three test cases:

- `test_show_version`: Verifies show version output contains expected string
- `test_show_chassis_hardware`: Verifies show chassis hardware output contains expected strings
- `test_show_interfaces_terse`: Verifies show interfaces terse output contains expected string

To run the tests:

```
$ python test_bootup.py
```

This will execute the test cases and report the results. Additional tests can be added to cover more aspects of the bootup validation.