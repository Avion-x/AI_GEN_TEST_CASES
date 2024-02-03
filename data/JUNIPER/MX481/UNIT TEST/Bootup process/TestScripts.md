 Here are sample unit tests for the bootup process of the Juniper Networks MX Series MX480 router, split into separate Python files:

### test_power_on.py

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_power_on(self):
        # Test powering on the device
        self.assertTrue(power_on_device()) 

if __name__ == '__main__':
    unittest.main()
```

### test_post.py 

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_post(self):
        # Test POST completing successfully
        self.assertEqual(get_post_status(), 'PASS')

if __name__ == '__main__':
   unittest.main()
```

### test_load_boot_config.py

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_load_boot_config(self):
        # Test loading boot configuration from flash
        self.assertTrue(load_boot_config())

if __name__ == '__main__':
    unittest.main()  
```

### test_routing_engine_online.py

```python
import unittest

class TestBootup(unittest.TestCase):

    def test_routing_engine_online(self):
        # Test routing engine coming online 
        self.assertTrue(check_routing_engine_status())

if __name__ == '__main__':
    unittest.main()
```

This provides sample unit tests for power on, POST, loading boot configuration, and routing engine online steps of the bootup process for the Juniper MX480 router. The tests would need to be fleshed out with actual implementation code and assertions for your specific environment.