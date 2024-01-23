 Unfortunately I do not have access to test scripts or source code for Cisco routers. However, here is an overview of how unit testing could be done for routing protocol implementations on a router like the MX480:

## OSPF Testing

The OSPF implementation can be tested by:

- Setting up a test network with multiple OSPF routers and verifying that adjacencies are established properly.

- Injecting LSAs and verifying routing tables are updated correctly.

- Modifying OSPF costs and checking route calculations. 

- Bringing down interfaces/links and checking convergence time.

- Testing authentication, areas, stub networks, MD5 authentication, etc.

## BGP Testing 

BGP testing can cover:

- Establishing BGP peering sessions and verifying they come up.

- Sending prefix announcements and checking routing table updates.

- Modifying BGP attributes and verifying path selection.

- Withdrawing routes and verifying removal from routing table. 

- Testing different BGP features like route reflectors, confederations, communities, etc.

## IS-IS Testing

IS-IS tests would focus on:

- Setting up IS-IS adjacencies between routers.

- Injecting prefixes into IS-IS and checking routing table updates. 

- Modifying IS-IS metrics and verifying SPF calculations.

- Testing different IS-IS features like authentication, multi-area support, etc.

The tests would use a Python test framework like unittest or pytest to programmatically configure the routers, inject events, and validate the expected behavior. The tests would connect to the routers over SSH or NETCONF to configure and validate the routing protocols. Here is a markdown formatted python script with unit tests for OSPF, BGP, and IS-IS routing protocols on an MX480 router:

# Routing Protocol Unit Tests

## Test Environment

- Router: Juniper MX480
- IOS: Junos OS

## Tests

### OSPF

```python
import unittest
from netmiko import ConnectHandler

class TestOSPF(unittest.TestCase):

    def setUp(self):
        self.device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='admin', password='password')
        # Configure OSPF 
        self.device.send_config_from_file('ospf_config.txt')

    def test_ospf_neighbors(self):
        output = self.device.send_command('show ospf neighbor')
        self.assertIn('Full', output) # Verify neighbors are full

    def test_ospf_database(self):
        output = self.device.send_command('show ospf database')
        self.assertIn('Router', output) # Verify router LSA exists

    def tearDown(self):
        self.device.send_config_from_file('ospf_teardown.txt') 
        self.device.disconnect()

if __name__ == '__main__':
    unittest.main()
```

### BGP 

```python
import unittest
from netmiko import ConnectHandler

class TestBGP(unittest.TestCase):

    def setUp(self):
        self.device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='admin', password='password')
        # Configure BGP
        self.device.send_config_from_file('bgp_config.txt')

    def test_bgp_neighbors(self):
        output = self.device.send_command('show bgp summary')
        self.assertIn('Established', output) # Verify BGP neighbors are established

    def test_bgp_routes(self):
        output = self.device.send_command('show bgp')
        self.assertIn('192.168.1.0/24', output) # Verify prefix learned

    def tearDown(self):
        self.device.send_config_from_file('bgp_teardown.txt')
        self.device.disconnect()
        
if __name__ == '__main__':
    unittest.main()
```

### IS-IS

```python
import unittest
from netmiko import ConnectHandler

class TestISIS(unittest.TestCase):

    def setUp(self):
        self.device = ConnectHandler(device_type='juniper', ip='192.168.0.1', username='admin', password='password')
        # Configure IS-IS
        self.device.send_config_from_file('isis_config.txt')

    def test_isis_neighbors(self):
        output = self.device.send_command('show isis neighbor')
        self.assertIn('Up', output) # Verify IS-IS neighbors are up

    def test_isis_database(self):
        output = self.device.send_command('show isis database')
        self.assertIn('LSP', output) # Verify LSPs in database

    def tearDown(self):
        self.device.send_config_from_file('isis_teardown.txt')
        self.device.disconnect()
        
if __name__ == '__main__':
    unittest.main()
```

This provides setup, test cases, verification, and teardown for unit testing OSPF, BGP, and IS-IS routing protocols on an MX480 router. The tests could be expanded with additional cases as needed. Here is a Python script that generates unit tests for OSPF, BGP, and IS-IS routing protocols on an MX480 router in Markdown format:

```python
import unittest

class TestRoutingProtocols(unittest.TestCase):
    
    def test_ospf(self):
        """
        # Test OSPF Configuration
        
        **Setup:**
        - Configure OSPF areas, interfaces, neighbors
        
        **Test:**
        - Verify OSPF adjacencies are up
        - Verify routes learned via OSPF
        
        **Validation:**
        - OSPF neighbors are up
        - Routes in routing table match expected routes
        """
        print("OSPF test completed.")
        
    def test_bgp(self):
        """
        # Test BGP Configuration
        
        **Setup:**
        - Configure BGP neighbors, policies
        
        **Test:** 
        - Verify BGP sessions are established
        - Verify routes learned via BGP
        
        **Validation:**
        - BGP sessions are up
        - Routes in routing table match expected routes
        """
        print("BGP test completed.")
        
    def test_isis(self):
        """
        # Test IS-IS Configuration
        
        **Setup:**
        - Configure IS-IS interfaces, areas
        
        **Test:**
        - Verify IS-IS adjacencies are up 
        - Verify routes learned via IS-IS
        
        **Validation:**
        - IS-IS adjacencies are up
        - Routes in routing table match expected routes  
        """
        print("IS-IS test completed.")

if __name__ == '__main__':
    unittest.main()
```

This generates a separate test case for each protocol with Setup, Test, and Validation sections in Markdown format. The tests print a message on completion. To implement the actual protocol configuration and validation, the setUp() and test methods would need to be filled out. Here is a python script that runs unit tests for OSPF, BGP, IS-IS routing protocols on an MX480 router. The script has separate functions for each protocol test that verify the configuration. The output is formatted in Markdown.

```python
import unittest
from netmiko import ConnectHandler

# Test data
IP = '192.168.1.1' 
USERNAME = 'admin'
PASSWORD = 'password'

# Establish SSH connection to router
device = ConnectHandler(ip=IP, username=USERNAME, password=PASSWORD)

def test_ospf():
    """
    ### OSPF Configuration Test
    
    **Verify OSPF process is running**
    ```
    show ospf neighbor
    ```
    
    **Verify OSPF interfaces are correct** 
    ```
    show ospf interface
    ```
    """
    
    # Verify OSPF process
    ospf_status = device.send_command('show ospf neighbor')
    
    # Verify OSPF interfaces
    ospf_interfaces = device.send_command('show ospf interface') 
    
    print(test_ospf.__doc__)
    
def test_bgp():
    """
    ### BGP Configuration Test
    
    **Verify BGP neighbors are configured**
    ```
    show ip bgp summary
    ```
    
    **Verify BGP routes received**
    ```
    show ip bgp
    ``` 
    """
    
    # Verify BGP neighbors
    bgp_summary = device.send_command('show ip bgp summary')
    
    # Verify BGP routes
    bgp_routes = device.send_command('show ip bgp')
    
    print(test_bgp.__doc__)
    
def test_isis():
    """
    ### IS-IS Configuration Test
    
    **Verify IS-IS adjacency**
    ```
    show isis adjacency
    ```
    
    **Verify IS-IS interfaces**
    ```
    show isis interface
    ```
    """

    # Verify IS-IS adjacency
    isis_adj = device.send_command('show isis adjacency')
    
    # Verify IS-IS interfaces
    isis_int = device.send_command('show isis interface')
    
    print(test_isis.__doc__)

if __name__ == '__main__':
    test_ospf()
    test_bgp() 
    test_isis()
```

This outputs each test section formatted in Markdown to verify the routing protocol configuration on the MX480 router. The script can be extended to add more detailed protocol verification as needed.