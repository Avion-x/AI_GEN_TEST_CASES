 Unfortunately I do not have access to scripts or code for specific Cisco router models. However, here is a general template for Python unit tests for routing protocol implementations:

```python
# test_ospf.py

import unittest
from ospf import OSPFProtocol

class OSPFTest(unittest.TestCase):

    def test_ospf_neighbors(self):
        ospf = OSPFProtocol()
        ospf.add_neighbor('192.168.1.1')
        self.assertEqual(len(ospf.neighbors), 1)
        self.assertIn('192.168.1.1', ospf.neighbors)
        
    def test_ospf_routes(self):
        ospf = OSPFProtocol()
        ospf.add_route('192.168.1.0/24')
        self.assertEqual(len(ospf.routes), 1)
        self.assertIn('192.168.1.0/24', ospf.routes)
        
if __name__ == '__main__':
    unittest.main()
```

```python
# test_bgp.py 

import unittest 
from bgp import BGPProtocol

class BGPTest(unittest.TestCase):

    def test_bgp_peers(self):
        bgp = BGPProtocol()
        bgp.add_peer('192.168.2.1')
        self.assertEqual(len(bgp.peers), 1)
        self.assertIn('192.168.2.1', bgp.peers)

    def test_bgp_routes(self):
        bgp = BGPProtocol()
        bgp.add_route('10.0.0.0/8')
        self.assertEqual(len(bgp.routes), 1)
        self.assertIn('10.0.0.0/8', bgp.routes)

if __name__ == '__main__':
    unittest.main()
```

```python
# test_isis.py

import unittest
from isis import ISISProtocol

class ISISTest(unittest.TestCase):

    def test_isis_neighbors(self):
        isis = ISISProtocol()
        isis.add_neighbor('1234.5678.9123')
        self.assertEqual(len(isis.neighbors), 1)
        self.assertIn('1234.5678.9123', isis.neighbors)

    def test_isis_routes(self):
        isis = ISISProtocol()
        isis.add_route('172.16.0.0/16')
        self.assertEqual(len(isis.routes), 1)
        self.assertIn('172.16.0.0/16', isis.routes)
        
if __name__ == '__main__':
    unittest.main()
```

This provides a basic template for unit testing the neighbor and route tables for each protocol implementation. The tests would need to be adapted to the specific APIs and implementations in use. But it demonstrates some examples of basic test cases for validating routing protocol behavior and state. Here is a Python script with unit tests for OSPF, BGP, and IS-IS routing protocols on an MX480 router:

```python
import unittest
from netmiko import ConnectHandler

class TestRoutingProtocols(unittest.TestCase):

    def setUp(self):
        self.router = {
            'device_type': 'juniper',
            'host': '192.168.0.1',
            'username': 'admin',
            'password': 'password123',
        }
        self.connection = ConnectHandler(**self.router)

    def tearDown(self):
        self.connection.disconnect()

class TestOSPF(TestRoutingProtocols):
    
    def test_ospf_neighbors(self):
        # Setup
        self.connection.send_command('configure')
        self.connection.send_command('set protocols ospf area 0.0.0.0 interface ge-0/0/0.0')
        
        # Execution
        output = self.connection.send_command('show ospf neighbor')
        
        # Verification
        self.assertIn('Full', output)
        
    def test_ospf_routes(self):
        # Execution
        output = self.connection.send_command('show route protocol ospf')
        
        # Verification
        self.assertIn('192.168.0.0/24', output)
        
class TestBGP(TestRoutingProtocols):

    def test_bgp_peers(self):
        # Setup
        self.connection.send_command('configure')
        self.connection.send_command('set protocols bgp group external neighbor 192.168.0.2')
        
        # Execution
        output = self.connection.send_command('show bgp summary')
        
        # Verification
        self.assertIn('Established', output)
        
    def test_bgp_routes(self):
        # Execution
        output = self.connection.send_command('show route protocol bgp')
        
        # Verification 
        self.assertIn('10.0.0.0/8', output)
        
class TestISIS(TestRoutingProtocols):

    def test_isis_adjacencies(self):
        # Setup
        self.connection.send_command('configure')
        self.connection.send_command('set protocols isis interface ge-0/0/0.0')
        
        # Execution
        output = self.connection.send_command('show isis adjacency')
        
        # Verification
        self.assertIn('Up', output)
        
    def test_isis_routes(self):
        # Execution
        output = self.connection.send_command('show route protocol isis')
        
        # Verification
        self.assertIn('192.168.0.0/24', output)

if __name__ == '__main__':
    unittest.main()
```

This script contains test cases for verifying OSPF neighbors and routes, BGP peers and routes, and ISIS adjacencies and routes on an MX480 router. The setUp and tearDown methods establish and close the router connection using Netmiko. Each test case has sections for setup, execution, and verification of the routing protocol configuration and state. The tests can be run by calling `python test_routing.py`. Here is a Python script with sample unit tests for OSPF, BGP, and IS-IS routing protocols on an MX480 router:

```python
import unittest
from netmiko import ConnectHandler

class TestMX480Routing(unittest.TestCase):

    def setUp(self):
        self.device = ConnectHandler(
            device_type='juniper_junos',
            host='mx480.example.com',
            username='netconf', 
            password='juniper123'
        )

    def tearDown(self):
        self.device.disconnect()

    def test_ospf_neighbors(self):
        """Test OSPF neighbors"""
        output = self.device.send_command('show ospf neighbor')
        self.assertIn('192.0.2.1', output)
        self.assertIn('192.0.2.2', output)

    def test_bgp_peers(self):
        """Test BGP peers"""
        output = self.device.send_command('show bgp summary')
        self.assertIn('192.0.2.3', output)
        self.assertIn('192.0.2.4', output)
        
    def test_isis_adjacencies(self):
        """Test IS-IS adjacencies"""
        output = self.device.send_command('show isis adjacency')
        self.assertIn('ge-0/0/1.0', output)
        self.assertIn('ge-0/0/2.0', output)

if __name__ == '__main__':
    unittest.main()
```

This script imports `unittest` and `netmiko` to create test cases that connect to the MX480 device, execute show commands for OSPF, BGP, and IS-IS, and verify the expected neighbors/peers are present in the output. The tests could be expanded with additional assertions as needed. Here are sample Python unit test scripts for testing routing protocol configurations on an MX480 router:

# test_ospf.py

import unittest
from netmiko import ConnectHandler

class TestOSPF(unittest.TestCase):

    def test_ospf_neighbors(self):
        """Test OSPF neighbors are correctly formed"""
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='myuser', password='pwd')
        ospf_neighbors = device.send_command('show ospf neighbor')
        
        self.assertIn('192.168.0.2', ospf_neighbors)
        self.assertIn('192.168.0.3', ospf_neighbors)
        
    def test_ospf_routes(self):
        """Test OSPF routes are correctly installed"""
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='myuser', password='pwd')
        ospf_routes = device.send_command('show route ospf')
        
        self.assertIn('192.168.1.0/24', ospf_routes)
        self.assertIn('192.168.2.0/24', ospf_routes)

if __name__ == '__main__':
    unittest.main()

# test_bgp.py

import unittest 
from netmiko import ConnectHandler

class TestBGP(unittest.TestCase):

    def test_bgp_neighbors(self):
        """Test BGP neighbors are correctly formed"""
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='myuser', password='pwd')
        bgp_neighbors = device.send_command('show bgp neighbor')
        
        self.assertIn('192.168.0.2', bgp_neighbors)
        self.assertIn('192.168.0.3', bgp_neighbors)

    def test_bgp_routes(self):
        """Test BGP routes are correctly installed"""
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='myuser', password='pwd')
        bgp_routes = device.send_command('show route bgp') 
        
        self.assertIn('10.0.0.0/24', bgp_routes)
        self.assertIn('10.0.1.0/24', bgp_routes)
        
if __name__ == '__main__':
    unittest.main()

# test_isis.py

import unittest
from netmiko import ConnectHandler

class TestISIS(unittest.TestCase):

    def test_isis_neighbors(self):
        """Test IS-IS neighbors are correctly formed"""
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='myuser', password='pwd')
        isis_neighbors = device.send_command('show isis neighbor')
        
        self.assertIn('192.168.0.2', isis_neighbors)
        self.assertIn('192.168.0.3', isis_neighbors)

    def test_isis_routes(self):
        """Test IS-IS routes are correctly installed"""
        device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='myuser', password='pwd')
        isis_routes = device.send_command('show route isis')
        
        self.assertIn('192.168.1.0/24', isis_routes) 
        self.assertIn('192.168.2.0/24', isis_routes)
        
if __name__ == '__main__':
    unittest.main()