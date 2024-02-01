 Here are the Python unit test scripts for bootup process test cases for the Juniper Networks MX480 router, split into separate files and provided in Markdown format:

### test_bootup.py

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        # Test powering on the router
        self.assertTrue(power_on_router())

    def test_boot_loader(self):
        # Test loading boot loader
        self.assertEqual(get_boot_loader_version(), "18.3R1-S2.1") 

if __name__ == '__main__':
    unittest.main()
```

### test_bios.py  

```python
import unittest

class TestBIOS(unittest.TestCase):

    def test_bios_version(self):
        # Test BIOS version
        self.assertEqual(get_bios_version(), "1.22")

    def test_bios_settings(self):
        # Test BIOS settings 
        self.assertTrue(set_bios_settings())

if __name__ == '__main__':
    unittest.main() 
```

### test_boot_image.py

```python
import unittest

class TestBootImage(unittest.TestCase):

    def test_boot_image_load(self):
        # Test boot image loading
        self.assertTrue(load_boot_image())

    def test_image_version(self):
        # Test correct image version loaded
        self.assertEqual(get_image_version(), "18.3R1-S2.1")

if __name__ == '__main__':
    unittest.main()
```

### test_startup_config.py

```python
import unittest 

class TestStartupConfig(unittest.TestCase):

    def test_load_startup_config(self):
        # Test loading startup config 
        self.assertTrue(load_startup_config())

    def test_validate_startup_config(self):
        # Validate startup config
        self.assertTrue(validate_startup_config())

if __name__ == '__main__':
   unittest.main()
```

This provides unit test cases for the key aspects of the bootup process like power on, BIOS, boot loader, boot image loading and startup configuration loading. The tests are split into logical files covering each area. Here is a python script with unit tests for the bootup process of an MX480 router, split into separate files for each test case:

## test_power_on.py

```python
import unittest
from router import MX480

class PowerOnTest(unittest.TestCase):

    def setUp(self):
        self.router = MX480()

    def test_power_on(self):
        self.router.power_on()
        self.assertTrue(self.router.is_powered_on())

    def tearDown(self):
        self.router.power_off()

if __name__ == '__main__':
    unittest.main()
```

This test cases checks that the router powers on correctly.

## test_boot_loader.py

```python 
import unittest
from router import MX480

class BootLoaderTest(unittest.TestCase):

    def setUp(self):
        self.router = MX480()
        self.router.power_on()

    def test_boot_loader(self):
        self.assertTrue(self.router.boot_loader_loaded())

    def tearDown(self):
        self.router.power_off()
        
if __name__ == '__main__':
    unittest.main()
```

This test checks that the boot loader is loaded after power on.

## test_kernel_load.py

```python
import unittest 
from router import MX480

class KernelLoadTest(unittest.TestCase):

    def setUp(self):
        self.router = MX480()
        self.router.power_on()
        self.router.load_boot_loader()

    def test_kernel_load(self):
        self.router.load_kernel()
        self.assertTrue(self.router.is_kernel_loaded())
        
    def tearDown(self):
        self.router.power_off()
        
if __name__ == '__main__':
    unittest.main()
```

This test checks that the kernel loads correctly after the boot loader.

## test_routing_engine_boot.py

```python
import unittest
from router import MX480

class RoutingEngineBootTest(unittest.TestCase):

    def setUp(self):
        self.router = MX480()
        self.router.power_on()
        self.router.load_boot_loader()
        self.router.load_kernel()

    def test_routing_engine_boot(self):
        self.router.boot_routing_engine()
        self.assertTrue(self.router.is_routing_engine_ready())

    def tearDown(self):
        self.router.power_off()
        
if __name__ == '__main__':
    unittest.main()
```

This test checks that the routing engine boots correctly after loading the kernel.

## test_complete_boot.py

```python
import unittest
from router import MX480 

class CompleteBootTest(unittest.TestCase):

    def test_complete_bootup(self):
        router = MX480()
        router.power_on()
        router.load_boot_loader()
        router.load_kernel()
        router.boot_routing_engine()
        
        self.assertTrue(router.is_powered_on())
        self.assertTrue(router.boot_loader_loaded())
        self.assertTrue(router.is_kernel_loaded())
        self.assertTrue(router.is_routing_engine_ready())

    def tearDown(self):
        router.power_off()
        
if __name__ == '__main__':
    unittest.main()
```

This test runs through the complete bootup process and checks that each stage completes successfully. Here is a Python script with unit tests for the bootup process of the Juniper MX480 router in markdown format:

## Unit Tests for MX480 Bootup Process

### Test POWER ON Self Test (POST)

```python
import unittest

class TestMX480POST(unittest.TestCase):

    def test_power_on(self):
        # Simulate power on
        print("Powering on MX480")
        
        # Check POST completes successfully
        self.assertTrue(post_passed)

if __name__ == '__main__':
    unittest.main()
```

### Test Loading Boot Loader

```python  
import unittest

class TestMX480Bootloader(unittest.TestCase):

    def test_load_bootloader(self):
        # Simulate POST completion
        post_passed = True
        
        # Load boot loader
        print("Loading boot loader")
        
        # Check boot loader loaded successfully
        self.assertTrue(bootloader_loaded)

if __name__ == '__main__':
    unittest.main()
```

### Test Loading Operating System

```python
import unittest

class TestMX480OSLoad(unittest.TestCase):

    def test_load_os(self):
        # Simulate boot loader loading
        bootloader_loaded = True
        
        # Load JUNOS operating system
        print("Loading JUNOS OS")
        
        # Check OS loaded successfully 
        self.assertTrue(os_loaded)

if __name__ == '__main__':
    unittest.main()
```

### Test Basic OS Functionality 

```python
import unittest

class TestMX480OSSetup(unittest.TestCase):

    def test_os_functions(self):
        # Simulate OS load
        os_loaded = True
        
        # Check basic OS functions
        print("Checking basic OS functionality")
        self.assertTrue(networking_works)
        self.assertTrue(routing_works)

if __name__ == '__main__':
   unittest.main()
```

This provides basic unit tests for the key stages of the MX480 router bootup process including POST, bootloader loading, OS loading, and high-level OS functionality. The tests simulate each stage and validate that it completed successfully. Here are sample Python scripts in separate files for unit testing the bootup process on an MX480 router:

**test_bootup.py**

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def test_check_interfaces(self):
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='admin', password='password')
        output = device.send_command('show interfaces terse')
        self.assertIn('ge-0/0/0', output)
        self.assertIn('ge-0/0/1', output)
        device.disconnect()
        
    def test_check_bgp(self):
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='admin', password='password')
        output = device.send_command('show bgp summary')
        self.assertIn('External', output)
        self.assertIn('Internal', output)
        device.disconnect()

if __name__ == '__main__':
    unittest.main()
```

**test_routing.py**

```python
import unittest  
from netmiko import ConnectHandler

class TestMX480Routing(unittest.TestCase):

    def test_ospf_neighbors(self):
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='admin', password='password')
        output = device.send_command('show ospf neighbor')
        self.assertIn('192.168.1.2', output)
        self.assertIn('192.168.3.4', output)
        device.disconnect()

    def test_bgp_routes(self):
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='admin', password='password')
        output = device.send_command('show route protocol bgp')
        self.assertIn('10.0.0.0/8', output) 
        self.assertIn('172.16.0.0/16', output)
        device.disconnect()
        
if __name__ == '__main__':
    unittest.main()
```

This provides two sample test files, one to test interfaces and BGP status, and another to test OSPF neighbors and BGP routes during the bootup process. The scripts use Netmiko to connect to the router and assert expected output is present in the command output.