 Here are sample Python unit test scripts for bootup process test cases for the MX480 router, separated into individual files and output in Markdown format:

## test_bootup_poweron.py

```python
import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.is_powered_on())
```

## test_bootup_post.py 

```python
import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_post(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.post_completed())
```

## test_bootup_os_load.py

```python 
import unittest
from router import MX480

class TestBootup(unittest.TestCase):

    def test_os_loaded(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.os_loaded()) 
```

## test_bootup_protocols_start.py

```python
import unittest
from router import MX480 

class TestBootup(unittest.TestCase):

    def test_protocols_start(self):
        router = MX480()
        router.power_on()
        self.assertTrue(router.protocols_started())
```

This provides sample unit tests to validate power on, POST completion, OS load, and protocol startup during the bootup process for the MX480 router. The tests are separated into individual files and formatted as Markdown for easy sharing. Here is the python script with unit tests for the MX480 bootup process in separate files:

**test_bootup.py**

```python
import unittest
from mx480 import MX480

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        print("Setting up")
        self.mx480 = MX480()

    def test_power_on(self):
        print("Executing power on test")
        self.mx480.power_on()
        self.assertTrue(self.mx480.is_powered_on())
        print("Verified power on successful")
    
    def test_load_boot_config(self):
        print("Executing load boot config test")
        self.mx480.load_boot_config()
        self.assertEquals(self.mx480.boot_config, "stored_config.cfg")
        print("Verified loading boot config successful")

    def test_load_junos(self):
        print("Executing Junos load test")
        self.mx480.load_junos()
        self.assertTrue(self.mx480.junos_loaded)
        print("Verified Junos load successful")

    def test_boot_completion(self):
        print("Executing boot completion test")
        self.mx480.complete_bootup()
        self.assertTrue(self.mx480.is_booted())
        print("Verified bootup completion")

    def tearDown(self):
        print("Cleaning up")
        del self.mx480

if __name__ == '__main__':
    unittest.main()
```

**test_power_on.py**

```python
import unittest
from mx480 import MX480

class TestMX480PowerOn(unittest.TestCase):

    def setUp(self):
        print("Setting up")
        self.mx480 = MX480()

    def test_power_on(self):
        print("Executing power on test")
        self.mx480.power_on()
        self.assertTrue(self.mx480.is_powered_on())
        print("Verified power on successful")
    
    def tearDown(self):
        print("Cleaning up")
        del self.mx480 

if __name__ == '__main__':
    unittest.main()
```

**test_load_boot_config.py**

```python
import unittest
from mx480 import MX480

class TestMX480LoadBootConfig(unittest.TestCase):

    def setUp(self):
        print("Setting up")
        self.mx480 = MX480()

    def test_load_boot_config(self):
        print("Executing load boot config test")
        self.mx480.load_boot_config()
        self.assertEquals(self.mx480.boot_config, "stored_config.cfg")
        print("Verified loading boot config successful")

    def tearDown(self):
        print("Cleaning up")
        del self.mx480

if __name__ == '__main__':
    unittest.main()
```

**test_load_junos.py**

```python
import unittest
from mx480 import MX480 

class TestMX480LoadJunos(unittest.TestCase):

    def setUp(self):
        print("Setting up")
        self.mx480 = MX480()

    def test_load_junos(self):
        print("Executing Junos load test") 
        self.mx480.load_junos()
        self.assertTrue(self.mx480.junos_loaded)
        print("Verified Junos load successful")

    def tearDown(self):
        print("Cleaning up")
        del self.mx480

if __name__ == '__main__':
    unittest.main()
```

**test_boot_completion.py**

```python
import unittest
from mx480 import MX480

class TestMX480BootCompletion(unittest.TestCase):

    def setUp(self):
        print("Setting up")
        self.mx480 = MX480()

    def test_boot_completion(self):
        print("Executing boot completion test")
        self.mx480.complete_bootup()
        self.assertTrue(self.mx480.is_booted())
        print("Verified bootup completion")

    def tearDown(self):
        print("Cleaning up")
        del self.mx480

if __name__ == '__main__':
    unittest.main()
```

This provides separate test case files for each step in the MX480 bootup process, with setup/teardown and logging to validate each stage. The tests could be run independently or together using a test runner. Here is a Python script with unit tests for the bootup process of the Juniper MX480 router, along with sample outputs in Markdown format:

```python
import unittest

class TestMX480Bootup(unittest.TestCase):

    def test_power_on(self):
        """Test powering on the device"""
        print("## Powering on the device")
        # Code to power on device
        self.assertEqual(device.power_state, "on")

    def test_boot_loader(self):
        """Test loading boot loader""" 
        print("## Loading boot loader")
        # Code to load boot loader
        self.assertTrue(device.bootloader_loaded)

    def test_kernel_load(self):
        """Test loading kernel"""
        print("## Loading kernel")
        # Code to load kernel
        self.assertTrue(device.kernel_loaded)

    def test_init_process(self):
        """Test initialization process"""
        print("## Initializing processes")
        # Code to initialize processes
        self.assertEqual(device.init_status, "complete")

    def test_routing_engine_online(self):
        """Test routing engine coming online"""
        print("## Bringing routing engine online")
        # Code to bring routing engine online 
        self.assertTrue(device.re_online)

if __name__ == '__main__':
    unittest.main()
```

## Sample Markdown Output

### Powering on the device
- Power on device
- Verify power state is "on"

### Loading boot loader 
- Load boot loader
- Verify bootloader is loaded

### Loading kernel
- Load kernel
- Verify kernel is loaded

### Initializing processes
- Initialize system processes
- Verify initialization status is "complete"

### Bringing routing engine online
- Bring routing engine online
- Verify routing engine status is online Here is a Python script to perform unit testing of the bootup process on an MX480 router:

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        self.device = ConnectHandler(
            device_type='juniper',
            host='mx480',
            username='netconf', 
            password='juniper123'
        )

    def test_save_startup_config(self):
        """Test saving startup config"""
        save_output = self.device.send_command("save /var/home/overlay/config/juniper.conf")
        self.assertIn("Wrote", save_output)

    def test_check_licenses(self):
        """Test checking licenses"""
        license_output = self.device.send_command("show system license")
        self.assertIn("Licenses", license_output)

    def test_check_interfaces(self):
        """Test checking interfaces"""
        interface_output = self.device.send_command("show interfaces terse")
        self.assertIn("ge-0/0/0", interface_output)

    def test_check_routing(self):
        """Test checking routing table"""
        routing_output = self.device.send_command("show route")
        self.assertIn("192.168.0.0/24", routing_output)

    def tearDown(self):
        self.device.disconnect()

if __name__ == "__main__":
    unittest.main()
```

This script uses the Netmiko library to connect to the MX480 device and execute show commands to verify:

- Saving the startup configuration
- Checking licenses 
- Checking interfaces
- Checking routing table

The assertions in each test case validate the expected output. The setUp() and tearDown() methods establish and close the Netmiko connection.