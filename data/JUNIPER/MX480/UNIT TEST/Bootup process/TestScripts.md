 Here are sample unit test python scripts for testing the bootup process on a Juniper Networks MX480 router, separated into different files:

### test_bootup_poweron.py

```python
import unittest

class TestBootupPowerOn(unittest.TestCase):

    def test_power_on(self):
        # Test powering on the device
        print("Powering on device...")
        self.assertTrue(power_on_device()) 

if __name__ == '__main__':
    unittest.main()
```

### test_bootup_bios.py 

```python
import unittest

class TestBootupBIOS(unittest.TestCase):

    def test_bios_post(self):
        # Test BIOS power on self test
        print("Verifying BIOS POST...")
        self.assertTrue(get_bios_post_result())

if __name__ == '__main__':
    unittest.main()
```

### test_bootup_loader.py

```python
import unittest 

class TestBootupLoader(unittest.TestCase):

    def test_loader(self):
        # Test loader initialization
        print("Verifying loader initialization...")
        self.assertTrue(get_loader_version())

if __name__ == '__main__':
   unittest.main()
```

### test_bootup_kernel.py

```python
import unittest

class TestBootupKernel(unittest.TestCase):

    def test_kernel_load(self):
        # Test kernel loading
        print("Verifying kernel load...")  
        self.assertTrue(get_kernel_version())

if __name__ == '__main__':
    unittest.main() 
```

This provides sample unit tests for the key stages of the bootup process - power on, BIOS, loader, and kernel loading. The test functions would need to be implemented to interact with the router and validate the bootup. Here are sample Python unit test scripts with setup, execution, verification and teardown for bootup process test cases on MX480 router:

```python
import unittest
from netmiko import ConnectHandler

class TestMx480Bootup(unittest.TestCase):

    def setUp(self):
        print('Setup: Connect to MX480 and initialize') 
        self.mx480 = {
            'device_type': 'juniper',
            'host': 'mx480.example.com',
            'username': 'netconf',
            'password': 'juniper123',
        }
        self.conn = ConnectHandler(**self.mx480)

    def test_bootup_time(self):
        print('Executing: Check bootup time is under 5 minutes')
        output = self.conn.send_command('show system boot-messages')
        bootup_time = parse_bootup_time(output) 
        self.assertLess(bootup_time, 300)

        print('Verification: Pass')

    def test_processes_startup(self):
        print('Executing: Verify key processes started')
        output = self.conn.send_command('show system processes')
        self.assertIn('rpd', output)
        self.assertIn('dfwd', output)  

        print('Verification: Pass')

    def test_interfaces_ready(self):
        print('Executing: Check all interfaces are ready')
        output = self.conn.send_command('show interfaces terse')
        interfaces = parse_interfaces(output)
        for intf in interfaces:
            self.assertEqual(intf['status'], 'up')
        
        print('Verification: Pass')    

    def tearDown(self):
        print('Teardown: Disconnect from MX480')
        self.conn.disconnect()

if __name__ == '__main__':
    unittest.main()
```

This shows sample test cases to check bootup time, verify key processes startup, and check interfaces readiness after reboot. The setup initializes the SSH connection, the test cases execute commands and verify the output, and the teardown closes the connection. Here is a Python script with unit tests for the bootup process of the MX480 router in markdown format:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):
    
    def test_power_on_self_test(self):
        """Test power on self test"""
        # Mock POST completion 
        self.assertEqual(POST_status, 'Passed')
        
    def test_load_boot_loader(self):
        """Test loading boot loader""" 
        # Mock boot loader load
        self.assertTrue(bootloader_loaded)
        
    def test_load_junos_kernel(self):
        """Test Junos kernel load"""
        # Mock Junos kernel load
        self.assertTrue(junos_kernel_loaded)
        
    def test_check_filesystems(self):
        """Test checking filesystems"""
        # Mock filesystem check
        self.assertEqual(fsck_status, 'Passed')
        
    def test_mount_filesystems(self):
        """Test mounting filesystems"""
        # Mock mounting root and var filesystems
        self.assertEqual(root_mounted, True)
        self.assertEqual(var_mounted, True)
        
    def test_load_daemons(self):
        """Test loading system daemons"""
        # Mock daemon loading
        self.assertTrue(daemons_loaded)
        
    def test_start_services(self):
        """Test starting system services"""
        # Mock services start
        self.assertEqual(services_started, True)
```

This script contains a unittest test case with separate test methods for each step in the MX480 bootup process like POST, loading bootloader, mounting filesystems etc. The methods mock each step and validate the expected output. This provides basic unit test coverage for the router bootup. Here are sample Python unit test scripts for testing the bootup process on an MX480 router:

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def test_bootup(self):
        device = {
            'device_type': 'juniper',
            'host': 'mx480.example.com',
            'username': 'testuser',
            'password': 'testpass'
        }
        
        net_connect = ConnectHandler(**device)
        output = net_connect.send_command('show version')
        
        # Verify successful boot by checking version output
        self.assertIn('Junos: 18.3R1.9', output)  
        
        # Verify default config loaded  
        self.assertIn('JUNOS software default', output)
        
        net_connect.disconnect()
        
if __name__ == '__main__':
    unittest.main()
```

```python  
import unittest
from netmiko import ConnectHandler

class TestMX480Interfaces(unittest.TestCase):

    def test_interfaces(self):
        device = {
            'device_type': 'juniper',
            'host': 'mx480.example.com', 
            'username': 'testuser',
            'password': 'testpass'
        }
        
        net_connect = ConnectHandler(**device)
        output = net_connect.send_command('show interfaces terse')
        
        # Verify all expected interfaces present
        self.assertIn('ge-0/0/0', output)
        self.assertIn('ge-0/0/1', output)
        
        net_connect.disconnect()
        
if __name__ == '__main__':
    unittest.main() 
```

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Routing(unittest.TestCase):

    def test_routing(self):
        device = {
            'device_type': 'juniper',
            'host': 'mx480.example.com',
            'username': 'testuser', 
            'password': 'testpass'
        }
        
        net_connect = ConnectHandler(**device)
        output = net_connect.send_command('show route')
        
        # Verify default routing table
        self.assertIn('0.0.0.0/0',[192.0.2.1] ', output)
        
        net_connect.disconnect()
        
if __name__ == '__main__':
    unittest.main()
```

This provides sample unit tests to verify the bootup configuration for version, interfaces and routing table on an MX480 router. The tests could be extended to validate additional aspects of bootup as needed.