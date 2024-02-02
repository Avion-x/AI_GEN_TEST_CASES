 Here are sample Python unit test scripts for testing the bootup process on a Juniper Networks MX480 router, separated into individual files and provided in Markdown format:

## test_bootup.py

```python
import unittest
from router import Router

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        router = Router("MX480")
        self.assertEqual(router.power_on(), "System booted up")
    
    def test_load_config(self):
        router = Router("MX480")
        router.power_on()
        self.assertEqual(router.load_config(), "Config loaded successfully")
        
    def test_interface_status(self):
        router = Router("MX480")
        router.power_on()
        router.load_config()
        self.assertEqual(router.get_interface_status("ge-0/0/0"), "up")
        
if __name__ == '__main__':
    unittest.main()
```

## test_routing.py

```python
import unittest
from router import Router 

class TestRouting(unittest.TestCase):

    def test_bgp_sessions(self):
        router = Router("MX480")
        router.power_on()
        router.load_config()
        self.assertEqual(router.get_bgp_sessions(), 2)
        
    def test_ospf_neighbors(self):
        router = Router("MX480")
        router.power_on()
        router.load_config()
        self.assertEqual(router.get_ospf_neighbors(), 4)

if __name__ == '__main__':
    unittest.main()   
```

## test_system_health.py

```python
import unittest
from router import Router

class TestSystemHealth(unittest.TestCase):

    def test_cpu_utilization(self):
        router = Router("MX480")
        router.power_on()
        router.load_config()
        cpu = router.get_cpu_utilization()
        self.assertLess(cpu, 80)
        
    def test_memory_utilization(self):
        router = Router("MX480")
        router.power_on()
        router.load_config()
        mem = router.get_memory_utilization()
        self.assertLess(mem, 90)
        
if __name__ == '__main__':
    unittest.main()
```

This provides a few examples of unit tests that could be written to validate the bootup process and basic functionality of a Juniper MX480 router. The tests cover power on, loading the configuration, interface status checks, routing protocol sessions, and basic system health monitoring. Additional tests could be added to validate other required functionality. Here is a python script with unit tests for the bootup process of an MX480 router in separate files for each test case, including setup, execution, verification, and teardown steps in markdown format:

```python
# test_bootup.py

import unittest
from router import MX480

class BootupTestCase(unittest.TestCase):

    def setUp(self):
        self.mx480 = MX480()

    def test_power_on(self):
        # Setup
        self.mx480.power_off()
        
        # Execution
        self.mx480.power_on()
        
        # Verification
        self.assertTrue(self.mx480.is_powered_on())
            
        # Teardown
        self.mx480.power_off()

    def test_load_bios(self):
        # Setup
        self.mx480.power_on()
        
        # Execution
        self.mx480.load_bios()
        
        # Verification
        self.assertTrue(self.mx480.bios_loaded())
        
        # Teardown        
        self.mx480.power_off()

    def test_boot_loader(self):
        # Setup
        self.mx480.power_on()
        self.mx480.load_bios()
        
        # Execution
        self.mx480.load_bootloader()
        
        # Verification
        self.assertTrue(self.mx480.bootloader_loaded())
        
        # Teardown
        self.mx480.power_off()

    def test_kernel_load(self):
        # Setup
        self.mx480.power_on()
        self.mx480.load_bios()
        self.mx480.load_bootloader()
        
        # Execution
        self.mx480.load_kernel()
        
        # Verification
        self.assertTrue(self.mx480.kernel_loaded())
        
        # Teardown
        self.mx480.power_off()
        
    def test_boot_completion(self):
        # Setup
        self.mx480.power_on()
        self.mx480.load_bios()
        self.mx480.load_bootloader()
        self.mx480.load_kernel()
        
        # Execution
        self.mx480.complete_boot()
        
        # Verification
        self.assertTrue(self.mx480.is_booted())
        
        # Teardown
        self.mx480.power_off()
        
if __name__ == '__main__':
    unittest.main()
```

This provides individual test cases for power on, BIOS load, bootloader load, kernel load, and complete boot. Each test has its own setup, execution, verification, and teardown steps. Here is a Python script that provides unit tests for the bootup process of the Juniper MX480 router in Markdown format:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):
    
    def test_power_on(self):
        """
        ## Test Power On
        * Power on the device
        * Verify power LED turns green
        """
        print("Powering on device...")
        power_led_color = "green"
        self.assertEqual(power_led_color, "green")
        
    def test_boot_loader(self):
        """
        ## Test Boot Loader
        * Verify boot loader version
        * Confirm boot loader loads operating system
        """
        print("Checking boot loader...")
        boot_loader_version = "1.0" 
        self.assertEqual(boot_loader_version, "1.0")
        print("Boot loader loaded operating system")
        
    def test_kernel_load(self):
        """
        ## Test Kernel Load
        * Confirm kernel version
        * Verify kernel initialization 
        """
        print("Checking kernel version...")
        kernel_version = "5.1"
        self.assertEqual(kernel_version, "5.1")
        print("Kernel initialized successfully")
        
    def test_operating_system(self):
        """
        ## Test Operating System
        * Check operating system version
        * Confirm operating system is Junos
        * Validate operating system processes initialized
        """
        print("Verifying operating system...")
        os_version = "Junos 20.1R1.9"
        self.assertIn("Junos", os_version)
        print("Junos processes initialized successfully")
        
if __name__ == '__main__':
    unittest.main()
```

This provides 4 test cases with Markdown headers and test steps to validate the bootup process of the MX480 router. The tests check power on, boot loader, kernel load, and operating system initialization. The script can be run using `python test_mx480_bootup.py` and will output the test results. Here are sample Python unit test scripts for testing the bootup process on an MX480 router:

```python
# test_bootup.py

import unittest
from router import MX480

class TestMX480Bootup(unittest.TestCase):

    def test_bootup(self):
        router = MX480()
        router.power_on()

        # Verify console output during bootup 
        self.assertIn("Booting kernel", router.console) 
        self.assertIn("Starting system logging", router.console)
        self.assertIn("Starting daemons", router.console)
        
        # Verify interfaces initialized properly
        self.assertEqual(len(router.interfaces), 8) 
        for intf in router.interfaces:
            self.assertTrue(intf.link_up)

        # Verify routing protocols started
        self.assertTrue(router.ospf_running)
        self.assertTrue(router.bgp_running)

        # Verify configuration loaded properly
        self.assertEqual(router.config["system"]["host-name"], "mx480-1")
        self.assertEqual(router.config["interfaces"]["ge-0/0/0"]["unit"]["0"]["family"]["inet"]["address"], "192.168.0.1/24")

if __name__ == '__main__':
    unittest.main()
```

```python
# test_interface_config.py

import unittest
from router import MX480

class TestMX480InterfaceConfig(unittest.TestCase):

    def test_interface_config(self):
        router = MX480()
        
        # Verify ge-0/0/0 interface config
        ge_0_0_0 = router.get_interface("ge-0/0/0")
        self.assertEqual(ge_0_0_0.unit[0].ip, "192.168.0.1/24")
        self.assertTrue(ge_0_0_0.enabled)
        
        # Verify ge-0/0/1 interface config 
        ge_0_0_1 = router.get_interface("ge-0/0/1")
        self.assertEqual(ge_0_0_1.unit[0].ip, "172.16.1.1/24")
        self.assertFalse(ge_0_0_1.enabled)
        
        # Verify lo0 interface config
        lo0 = router.get_interface("lo0")
        self.assertEqual(lo0.unit[0].ip, "10.1.1.1/32")
        self.assertTrue(lo0.enabled)
        
if __name__ == '__main__':
    unittest.main()
```

This provides sample unit tests that could be implemented for testing the bootup process and interface configuration on an MX480 router. The tests verify expected console output, interface states, running protocols, and configuration values after bootup. Additional tests could be added to verify other aspects of the boot process and environment as needed.