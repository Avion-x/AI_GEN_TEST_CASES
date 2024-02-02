 Here are sample Python unit test scripts for testing the bootup process on a Juniper Networks MX480 router, split into separate files:

### test_bootup.py

```python
import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.is_powered_on())

    def test_bios_post(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.bios_post())

    def test_load_junos(self):
        router = MX480()
        router.power_on()
        router.bios_post()
        self.assertTrue(router.load_junos())

if __name__ == '__main__':
    unittest.main()
```

### test_interfaces.py

```python
import unittest
from router import MX480

class TestInterfaces(unittest.TestCase):

    def test_interfaces_up(self):
        router = MX480()
        router.power_on()
        router.bios_post()
        router.load_junos()
        interfaces = router.get_interfaces()
        for intf in interfaces:
            self.assertTrue(intf.is_up()) 

if __name__ == '__main__':
    unittest.main()
```

### test_routing.py

```python
import unittest
from router import MX480

class TestRouting(unittest.TestCase):

    def test_routing_table(self):
        router = MX480()
        router.power_on()
        router.bios_post() 
        router.load_junos()
        routing_table = router.get_routing_table()
        self.assertGreater(len(routing_table), 0)

if __name__ == '__main__':
    unittest.main() 
```

This provides sample unit tests to validate power on, BIOS post, Junos bootup, interfaces status, and routing table population during the bootup process. The tests are split across 3 files for booting up, interfaces, and routing. Here is a Python script with unit tests for the bootup process on an MX480 router, with each test case split into separate files:

## test_bootup.py

```python
import unittest
from router import Router

class TestBootup(unittest.TestCase):

    def setUp(self):
        self.router = Router('MX480')

    def test_power_on(self):
        self.router.power_on()
        self.assertTrue(self.router.is_powered_on())

    def test_load_boot_config(self):
        self.router.power_on()
        self.router.load_boot_config()
        self.assertEqual(self.router.get_config(), 'boot_config') 

    def test_load_junos(self):
        self.router.power_on()
        self.router.load_junos()
        self.assertEqual(self.router.get_os(), 'JunOS')

    def test_check_interfaces(self):
        self.router.power_on()
        self.router.load_junos()
        interfaces = self.router.get_interfaces()
        self.assertEqual(len(interfaces), 480)

    def tearDown(self):
        self.router.power_off()

```

## router.py

```python
class Router:

    def __init__(self, model):
        self.model = model
        self.powered_on = False

    def power_on(self):
        print(f"Powering on {self.model} router")
        self.powered_on = True

    def power_off(self):
        print(f"Powering off {self.model} router")
        self.powered_on = False 

    def load_boot_config(self):
        print("Loading boot configuration...")
        self.config = 'boot_config'

    def load_junos(self):
        print("Loading JunOS...")
        self.os = 'JunOS'

    def get_config(self):
        return self.config

    def get_os(self):
        return self.os

    def get_interfaces(self):
        if self.model == 'MX480':
            return 480
        else:
            return 0
        
    def is_powered_on(self):
        return self.powered_on

```

This splits the test code from the implementation code for better organization. The setUp and tearDown methods are used to initialize and clean up the router for each test case. Here is a Python script with sample unit tests for the bootup process of the Juniper MX480 router:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):

    def test_power_on(self):
        """Test powering on the device"""
        # Mock power on function
        self.assertTrue(power_on_device()) 

    def test_bootloader(self):
        """Test loading the bootloader"""
        # Mock bootloader load function
        self.assertTrue(load_bootloader())

    def test_kernel_load(self):
        """Test loading the Junos kernel"""
        # Mock kernel load function
        self.assertTrue(load_kernel()) 

    def test_routing_engine_boot(self):
        """Test bootup of routing engines"""
        # Mock routing engine boot function
        self.assertTrue(boot_re0())
        self.assertTrue(boot_re1())

    def test_linecard_boot(self):
        """Test bootup of linecards"""
        # Mock linecard boot function
        self.assertTrue(boot_lc0())
        self.assertTrue(boot_lc1())
        self.assertTrue(boot_lc2())

    def test_forwarding_engine_boot(self):
        """Test bootup of forwarding engines""" 
        # Mock forwarding engine boot function
        self.assertTrue(boot_fe0())
        self.assertTrue(boot_fe1())

    def test_switch_fabric_boot(self):
        """Test bootup of switch fabric"""
        # Mock switch fabric boot function
        self.assertTrue(boot_sf())

    def test_interface_initialization(self):
        """Test initialization of network interfaces"""
        # Mock interface initialization function
        self.assertTrue(init_interfaces())

    def test_routing_protocol_start(self):
        """Test start of routing protocols"""
        # Mock routing protocol start function
        self.assertTrue(start_bgp())
        self.assertTrue(start_ospf())

    def test_system_ready_state(self):
        """Test system ready state"""
        # Mock function to check system ready state
        self.assertTrue(system_ready())

if __name__ == '__main__':
    unittest.main()
```

This implements some sample unit tests to validate the critical steps in the MX480 bootup process like:

- Powering on 
- Loading bootloader
- Loading Junos kernel 
- Booting routing engines
- Booting linecards
- Booting forwarding engines
- Booting switch fabric 
- Initializing network interfaces
- Starting routing protocols
- Reaching overall system ready state

Each test case mocks the corresponding bootup function and asserts the expected result to validate successful bootup. Here are sample Python unit test scripts for testing the bootup process on an MX480 router:

```python
# test_bootup.py

import unittest
from router import MX480

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        self.router = MX480()

    def test_bootup(self):
        self.router.power_on()
        self.assertEqual(self.router.get_state(), 'BOOTING')
        
        self.router.load_config()
        self.assertEqual(self.router.get_state(), 'READY')
        
    def test_bootup_failure(self):
        self.router.power_on()
        self.assertEqual(self.router.get_state(), 'BOOTING')
        
        self.router.corrupt_config()
        self.router.load_config()
        self.assertEqual(self.router.get_state(), 'FAILURE')
        
if __name__ == '__main__':
    unittest.main()
```

```python
# test_interfaces.py 

import unittest
from router import MX480

class TestMX480Interfaces(unittest.TestCase):

    def setUp(self):
        self.router = MX480()
        self.router.bootup()

    def test_interface_status(self):
        interfaces = self.router.get_interfaces()
        
        for intf in interfaces:
            self.assertEqual(intf.get_status(), 'UP')
            
    def test_interface_failure(self):
        intf = self.router.get_interface('ge-0/0/0')
        
        intf.set_status('DOWN')
        self.assertEqual(intf.get_status(), 'DOWN')
        
if __name__ == '__main__':
    unittest.main()   
```

```python
# test_routing.py

import unittest 
from router import MX480

class TestMX480Routing(unittest.TestCase):

    def setUp(self):
        self.router = MX480()
        self.router.bootup()

    def test_add_static_route(self):
        self.router.add_static_route('10.0.0.0/24', '192.168.1.1')
        routes = self.router.get_routing_table()
        self.assertIn('10.0.0.0/24', routes)
        
    def test_remove_static_route(self):
        self.router.add_static_route('10.0.0.0/24', '192.168.1.1')
        self.router.remove_static_route('10.0.0.0/24')
        routes = self.router.get_routing_table()
        self.assertNotIn('10.0.0.0/24', routes)
        
if __name__ == '__main__':
    unittest.main()
```

This provides sample unit tests to validate bootup, interface status, and routing configuration on the MX480 router. The tests are split into separate files for easier organization and execution.