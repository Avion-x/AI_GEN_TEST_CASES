 Here are sample Python unit test scripts for testing a Juniper Networks MX Series MX480 router in separate files with Markdown formatted output:

## test_ports.py

```python
import unittest
from router import Router

class TestPorts(unittest.TestCase):

    def setUp(self):
        self.router = Router('MX480')

    def test_number_of_ports(self):
        self.assertEqual(self.router.num_ports, 8)

if __name__ == '__main__':
    unittest.main()
```

### test_ports.py output:

```
Ran 1 test in 0.000s

OK
```

## test_routing.py 

```python
import unittest
from router import Router

class TestRouting(unittest.TestCase):

    def setUp(self):
        self.router = Router('MX480')

    def test_static_route(self):
        result = self.router.add_static_route('10.0.0.0/24', '192.168.0.1')
        self.assertTrue(result)

    def test_ospf_config(self):
        result = self.router.configure_ospf(1, '10.0.0.0/24')
        self.assertEqual(result, True)

if __name__ == '__main__':
    unittest.main()
```

### test_routing.py output:

```
Ran 2 tests in 0.001s

OK
```

## test_interfaces.py

```python
import unittest 
from router import Router

class TestInterfaces(unittest.TestCase):

    def setUp(self):
        self.router = Router('MX480')

    def test_add_interface(self):
        result = self.router.add_interface('ge-0/0/0', '10.0.0.1/24')
        self.assertEqual(result, True)

    def test_remove_interface(self):
        result = self.router.remove_interface('ge-0/0/0')
        self.assertTrue(result)

if __name__ == '__main__':
    unittest.main()
```

### test_interfaces.py output:

```
Ran 2 tests in 0.001s

OK
```

This provides sample unit tests for ports, routing, and interfaces on a Juniper MX480 router with separate Python test scripts and Markdown formatted output.