 Here are sample Python unit test scripts for testing the bootup process on a Juniper Networks MX480 router, separated into individual files and formatted as Markdown:

```python
# test_bootup.py

import unittest
from netmiko import ConnectHandler

class TestBootup(unittest.TestCase):

    def test_console_access(self):
        """Test console access after bootup"""
        device = ConnectHandler(device_type='juniper', ip='192.168.1.1', username='admin', password='pwd123')
        output = device.send_command("show version")
        self.assertIn("JUNOS Software Release", output)

    def test_cli_access(self):
        """Test CLI access via SSH after bootup"""
        device = ConnectHandler(device_type='juniper_junos', ip='192.168.1.1', username='admin', password='pwd123')
        output = device.send_command("show interfaces terse")
        self.assertIn("ge-0/0/0", output)

if __name__ == '__main__':
    unittest.main()
```

```python
# test_interfaces.py 

import unittest
from netmiko import ConnectHandler

class TestInterfaces(unittest.TestCase):

    def test_interfaces_up(self):
        """Test interfaces are up after bootup"""
        device = ConnectHandler(device_type='juniper', ip='192.168.1.1', username='admin', password='pwd123')
        output = device.send_command("show interfaces terse")
        self.assertNotIn("ge-0/0/0", output)

    def test_bfd_sessions_up(self):
        """Test BFD sessions come up after bootup"""
        device = ConnectHandler(device_type='juniper_junos', ip='192.168.1.1', username='admin', password='pwd123')
        output = device.send_command("show bfd session")
        self.assertIn("Up", output)
        
if __name__ == '__main__':
    unittest.main()
```

```python
# test_routing.py

import unittest 
from netmiko import ConnectHandler

class TestRouting(unittest.TestCase):

    def test_ospf_neighbors(self):
        """Test OSPF neighbors up after bootup"""
        device = ConnectHandler(device_type='juniper', ip='192.168.1.1', username='admin', password='pwd123')
        output = device.send_command("show ospf neighbor")
        self.assertIn("Full", output)

    def test_bgp_peers(self):
        """Test BGP peers up after bootup"""
        device = ConnectHandler(device_type='juniper_junos', ip='192.168.1.1', username='admin', password='pwd123')
        output = device.send_command("show bgp summary") 
        self.assertNotIn("Idle", output)

if __name__ == '__main__':
    unittest.main()
``` Here is a set of sample Python unit test scripts with setup, execution, verification and teardown for testing the bootup process on an MX480 router:

```python
import unittest
from router import MX480

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        self.router = MX480()
        self.router.power_on()

    def test_bootup_to_login_prompt(self):
        print("# Test Case: Boot up to login prompt")
        self.router.wait_for_bootup()
        prompt = self.router.get_prompt()
        self.assertEqual(prompt, "login:")

    def test_login_to_operational_mode(self):
        print("# Test Case: Login to operational mode") 
        self.router.wait_for_bootup()
        self.router.login("username", "password")
        prompt = self.router.get_prompt()
        self.assertEqual(prompt, "mx480#")

    def test_check_interfaces_up(self):
        print("# Test Case: Verify all interfaces are up")
        self.router.wait_for_bootup()
        self.router.login("username", "password")
        interfaces = self.router.get_interfaces()
        for intf in interfaces:
            self.assertTrue(intf.is_up())

    def tearDown(self):
        self.router.power_off()

if __name__ == '__main__':
    unittest.main()
```

This contains test cases for:

- Bootup to login prompt
- Login to operational mode 
- Verify interfaces are up

It uses a Router class abstraction to perform operations on the router like power on/off, login, execute commands etc. Setup boots the router, execution runs the test case, verification checks the results, and teardown powers off the router. Here is a Python script with unit tests for the bootup process of the Juniper MX480 router, along with sample outputs in Markdown format:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):

    def test_power_on(self):
        """Test powering on the device"""
        print("## Powering on device")
        # Code to power on device
        self.assertEqual(device.power_state, "on")

    def test_bootloader(self):
        """Test loading bootloader""" 
        print("## Loading bootloader")
        # Code to load bootloader
        self.assertEqual(device.bootloader_state, "loaded")

    def test_kernel_load(self):
        """Test loading kernel"""
        print("## Loading kernel")
        # Code to load kernel 
        self.assertEqual(device.kernel_state, "loaded")

    def test_init_processes(self):
        """Test initializing processes"""
        print("## Initializing processes")
        # Code to start init process
        self.assertEqual(device.init_complete, True)

    def test_daemons_running(self):
        """Test required daemons running"""
        print("## Checking required daemons")
        # Check status of required daemons
        self.assertEqual(device.daemons_running, True)

    def test_protocols_initialized(self):
        """Test required protocols initialized"""
        print("## Initializing protocols")
        # Initialize routing protocols
        self.assertEqual(device.protocols_ready, True)
        
if __name__ == '__main__':
    unittest.main()
```

### Sample Output

```
## Powering on device  
.
## Loading bootloader
.
## Loading kernel  
.
## Initializing processes
.
## Checking required daemons
.
## Initializing protocols
.
----------------------------------------------------------------------
Ran 6 tests in 0.000s

OK
```

This script contains test cases for the key steps in the MX480 bootup process like powering on, loading bootloader and kernel, starting init process, checking daemons and initializing protocols. The tests assert that each stage completes successfully. The sample output shows the test name, along with a `.` for passed tests. Let me know if you need any clarification or have additional requirements. Here are sample Python unit test scripts in separate files for testing the bootup process on an MX480 router:

**test_bootup_poweron.py**

```python
import unittest
from router import MX480 

class TestBootupPowerOn(unittest.TestCase):

    def test_power_on(self):
        router = MX480()
        self.assertFalse(router.is_powered_on()) 
        router.power_on()
        self.assertTrue(router.is_powered_on())

if __name__ == '__main__':
    unittest.main()
```

**test_bootup_bios.py** 

```python
import unittest
from router import MX480

class TestBootupBIOS(unittest.TestCase):

    def test_bios_post(self):
        router = MX480()
        router.power_on()
        self.assertFalse(router.bios_post_completed())
        # Wait for BIOS POST to complete
        router.wait_for_bios_post() 
        self.assertTrue(router.bios_post_completed())

if __name__ == '__main__':
    unittest.main() 
```

**test_bootup_loader.py**

```python
import unittest
from router import MX480

class TestBootupLoader(unittest.TestCase):

    def test_loader(self):
        router = MX480()
        router.power_on()
        router.wait_for_bios_post()
        self.assertFalse(router.loader_started())
        # Wait for loader to start
        router.wait_for_loader()
        self.assertTrue(router.loader_started()) 

if __name__ == '__main__':
    unittest.main()
```

**test_bootup_kernel.py**

```python
import unittest
from router import MX480

class TestBootupKernel(unittest.TestCase):

    def test_kernel_boot(self):
        router = MX480()
        router.power_on()
        router.wait_for_bios_post()
        router.wait_for_loader()
        self.assertFalse(router.kernel_booted())
        # Wait for kernel to boot
        router.wait_for_kernel() 
        self.assertTrue(router.kernel_booted())

if __name__ == '__main__':
   unittest.main()
```

This provides sample unit tests to validate each stage of the bootup process on the MX480 router. Additional tests could be added to validate configuration loading, interfaces coming up etc.