 Here are sample unit tests for testing the bootup process on a Juniper Networks MX480 router, separated into individual Python files:

## test_bootup_coldstart.py

```python
import unittest
from netmiko import ConnectHandler

class TestColdBoot(unittest.TestCase):

    def setUp(self):
        self.router = {
            'device_type': 'juniper',
            'host': 'mx480.example.com', 
            'username': 'netconf', 
            'password': 'password123'
        }
    
    def test_cold_boot(self):
        net_connect = ConnectHandler(**self.router)
        output = net_connect.send_command("request chassis power cycle cold")
        
        self.assertIn("Chassis performing cold reboot", output)
        
        # Wait for device to come back up
        net_connect.disconnect()  
        net_connect.establish_connection()
        
        self.assertIsNotNone(net_connect.find_prompt())

if __name__ == '__main__':
    unittest.main()
```

## test_bootup_rescue_config.py

```python
import unittest
from netmiko import ConnectHandler

class TestRescueConfigBoot(unittest.TestCase):

    def setUp(self):
        self.router = {
            'device_type': 'juniper',
            'host': 'mx480.example.com',
            'username': 'netconf', 
            'password': 'password123' 
        }
    
    def test_rescue_config_boot(self):
        net_connect = ConnectHandler(**self.router)
        output = net_connect.send_command("request chassis power cycle rescue-configuration")

        self.assertIn("Chassis performing rescue configuration reboot", output)
        
        # Wait for device to come up with rescue config
        net_connect.disconnect()
        net_connect.establish_connection()

        prompt = net_connect.find_prompt()
        self.assertIn("#", prompt)

if __name__ == '__main__':
    unittest.main()
```

## test_bootup_on_demand_rescue.py

```python
import unittest
from netmiko import ConnectHandler

class TestOnDemandRescueBoot(unittest.TestCase):

    def setUp(self):
        self.router = {
            'device_type': 'juniper',
            'host': 'mx480.example.com',
            'username': 'netconf',
            'password': 'password123' 
        }
    
    def test_on_demand_rescue_boot(self):
        net_connect = ConnectHandler(**self.router)
        net_connect.send_command("request chassis power rescue on-demand")
        
        # Wait for device to come up in rescue mode
        net_connect.disconnect()
        net_connect.establish_connection()

        prompt = net_connect.find_prompt()
        self.assertIn("RESCUE", prompt)

if __name__ == '__main__':
    unittest.main()  
```

This provides three sample test cases for testing different bootup scenarios on the Juniper MX480 router - cold boot, rescue configuration boot, and on-demand rescue boot. The tests use Netmiko to connect to the device and issue reboot commands, then validate the router came back up as expected. Here are sample Python unit test scripts for bootup process of MX480 router with setup, execution, verification and teardown for each test case in Markdown format:

## Test Bootup with valid startup-config

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        print("### SETUP: Connect to device") 
        self.device = ConnectHandler(device_type='juniper', ip='192.168.1.1', username='testuser', password='test123')

    def test_bootup_valid_startupconfig(self):
        print("### TEST: Bootup with valid startup-config")
        print("#### ACTION: Reload device with valid startup-config")
        self.device.send_command('request system reboot')
        
        print("#### VERIFY: Check if device is reachable after reboot")
        reboot_done = False
        while not reboot_done:
            try:
                self.device.find_prompt()
                reboot_done = True
            except:
                pass
        
        print("#### VERIFY: Check show version for expected config")
        output = self.device.send_command('show version')
        self.assertIn('JUNOS version', output)

        print("TEST PASSED")
        
    def tearDown(self):
        print("### TEARDOWN: Disconnect from device")
        self.device.disconnect()
        
if __name__ == '__main__':
    unittest.main()
```

## Test Bootup with invalid startup-config 

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        print("### SETUP: Connect to device and modify startup-config")
        self.device = ConnectHandler(device_type='juniper', ip='192.168.1.1', username='testuser', password='test123')
        self.device.send_config_set('set system host-name test')
        
    def test_bootup_invalid_startupconfig(self):
        print("### TEST: Bootup with invalid startup-config")
        print("#### ACTION: Reload device with invalid startup-config")
        self.device.send_command('request system reboot')

        print("#### VERIFY: Check if device is reachable after reboot")        
        reboot_done = False
        while not reboot_done:
            try:
                self.device.find_prompt()
                reboot_done = True
            except:
                pass

        print("#### VERIFY: Check show version for failure")
        output = self.device.send_command('show version')
        self.assertNotIn('JUNOS version', output)
        
        print("TEST PASSED")
        
    def tearDown(self):
        print("### TEARDOWN: Rollback changes and disconnect from device")
        self.device.send_config_set('delete system host-name test')
        self.device.commit()
        self.device.disconnect()
        
if __name__ == '__main__':
    unittest.main()
```

## Test Bootup with corrupted filesystem

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def setUp(self):
        print("### SETUP: Connect to device")
        self.device = ConnectHandler(device_type='juniper', ip='192.168.1.1', username='testuser', password='test123')

    def test_bootup_corrupted_filesystem(self):
        print("### TEST: Bootup with corrupted filesystem")
        print("#### ACTION: Corrupt filesystem and reload device")
        self.device.send_command('request system storage cleanup')
        
        print("#### ACTION: Reload device")
        self.device.send_command('request system reboot')

        print("#### VERIFY: Check console logs for storage errors")
        output = self.device.read_channel()
        self.assertIn('% Check system storage', output)
        
        print("TEST PASSED")
        
    def tearDown(self):
        print("### TEARDOWN: Disconnect from device")
        self.device.disconnect()
        
if __name__ == '__main__':
    unittest.main()
``` Here is a Python script with unit tests for the bootup process of the Juniper MX480 router in markdown format:

```python
import unittest
from juniper_pyez import connect

class TestMx480Bootup(unittest.TestCase):
    
    def setUp(self):
        self.dev = connect(host='mx480')
        
    def test_check_power_on(self):
        """
        ## Test power on state
        Check that the router chassis is powered on and operational
        """        
        output = self.dev.rpc.get_chassis_inventory()
        status = output.findtext('.//chassis-module/chassis-sub-module/description')
        
        self.assertEqual(status, 'Online')
        
    def test_check_control_plane_boot(self):
        """
        ## Test control plane boot        
        Check that the control plane has completed booting 
        """
        output = self.dev.rpc.get_route_engine_information()
        status = output.findtext('.//route-engine/mastership-state')
        
        self.assertEqual(status, 'master')
        
    def test_check_data_planes_online(self):
        """
        ## Test data plane status 
        Check all data planes are online
        """
        output = self.dev.rpc.get_route_engine_information()
        
        data_planes = output.findall('.//data-plane')
        for dp in data_planes:
            status = dp.findtext('status')
            self.assertEqual(status, 'Online')
            
if __name__ == '__main__':
    unittest.main()
```

This scripts sets up a PyEZ connection to the device, and contains test cases to check:

- The chassis power is on 
- The control plane has finished booting
- All data planes are online

The tests assert the expected status using PyEZ RPC calls and verify the bootup is complete. Here are sample Python unit test scripts for testing the bootup process on an MX480 router. The tests verify the configuration and provide detailed output in Markdown format:

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Bootup(unittest.TestCase):

    def test_interfaces(self):
        """Test interfaces configuration"""
        
        device = ConnectHandler(device_type='juniper', host='mx480', username='testuser', password='password')
        
        print('## Interfaces')  
        print('### Obtain interfaces configuration')
        interfaces = device.send_command('show interfaces terse')
        
        print('```')
        print(interfaces)
        print('```')
        
        self.assertIn('ge-0/0/0', interfaces)
        self.assertIn('ge-0/0/1', interfaces)
        
        print('Interfaces configuration looks good!')
        
    def test_protocols(self):
        """Test protocols configuration"""
        
        print('## Protocols')
        print('### Obtain OSPF configuration')  
        ospf = device.send_command('show protocols ospf')
        
        print('```')
        print(ospf)
        print('```')
        
        self.assertIn('area 0.0.0.0', ospf)
        
        print('OSPF configuration looks good!')
        
if __name__ == '__main__':
    unittest.main()
```

This provides two sample test cases - one to test interfaces configuration and another to test OSPF protocol configuration. The tests use Netmiko to connect to the router and execute show commands. The output is printed in Markdown format with code blocks. The tests also include assertions to validate the presence of expected configuration.