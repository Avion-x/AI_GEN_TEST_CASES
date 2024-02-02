 ###STARTLIST###

[
    {
        "testname": "Boot Time Test", 
        "testcases": {
            "testname": "Boot Time Test",
            "objective": "To validate boot time of MX480 is within expected limit", 
            "steps": [
                "- Power on the MX480 router", 
                "- Note start time",
                "- Wait for router to come up with login prompt",
                "- Note end time", 
                "- Calculate difference between start and end times",
                "- Boot time should be less than 300 seconds"
            ],
            "test_data": {
                "start_time": "", 
                "end_time": "", 
                "boot_time_limit": 300 
            }
        },
        "testscripts": {
            "testname": "Boot Time Test Script",
            "objective": "To automate validation of MX480 boot time",
            "file_name": "test_boottime.py",
            "init_scripts": "pip install datetime",
            "script": """
            import datetime
            
            start_time = datetime.datetime.now()
            print(f"Start time: {start_time}")
            
            # Code to power on and boot router
                
            end_time = datetime.datetime.now() 
            print(f"End time: {end_time}")
            
            boot_time = (end_time - start_time).seconds
            print(f"Boot time: {boot_time} seconds")
            
            boot_time_limit = 300
            assert boot_time < boot_time_limit
            """,
            "run_command": "python test_boottime.py", 
            "expected_result": "Boot time logged. Assertion passes if boot time is less than 300 seconds."
        }
    },
    {
        "testname": "Power Draw Test",
        "testcases": {
            "testname": "Power Draw Test",
            "objective": "Validate power draw of MX480 during bootup is within limits",
            "steps": [
                "- Connect power meter to MX480 power supply",
                "- Power on MX480", 
                "- Note power draw reading on meter when login prompt appears",
                "- Power draw should be less than 1200 W"  
            ],
            "test_data": {
                "power_draw_limit": 1200 
            }
        },
        "testscripts": {
            "testname": "Power Draw Automation Script", 
            "objective": "Automate power draw validation during MX480 boot",
            "file_name": "test_powerdraw.py",
            "init_scripts": "pip install pyvisa", 
            "script": """
            import pyvisa
            
            rm = pyvisa.ResourceManager()
            power_meter = rm.open_resource("USB0::0x1AB1::0x0588::DM3R19290138::INSTR")
            
            power_meter.write(":MEASure:POWer?")
            power_draw = float(power_meter.read())
            
            power_draw_limit = 1200
            assert power_draw < power_draw_limit
            
            print(f"Power draw: {power_draw} W") 
            """,
           "run_command": "python test_powerdraw.py",
            "expected_result": "Power draw value logged. Test passes if power draw is less than 1200W."
        }
    }
]

###ENDLIST### ###STARTLIST###
[
{
  "testname": "Boot Device Detection Test",
  "testcases": {
    "testname": "Boot Device Detection Test", 
    "objective": "Verify that the router detects all connected boot devices during the boot process",
    "steps": [
      "- Power on the router",
      "- Check console logs for boot device detection messages", 
      "- Validate all connected boot devices are detected"
    ],
    "test_data": {
      "boot_devices": ["USB drive", "hard disk"]
    }
  },
  "testscripts": {
    "testname": "Boot Device Detection Test",
    "objective": "Automate validation of boot device detection",
    "file_name": "test_boot_devices.py",
    "init_scripts": "pip install paramiko",
    "script": """
import paramiko
import re

IP = "192.168.1.1"
USERNAME = "admin"
PASSWORD = "admin123"

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect(IP, username=USERNAME, password=PASSWORD)

stdin, stdout, stderr = ssh.exec_command("show boot-devices")
output = stdout.read().decode()

boot_devices = ["USB drive", "hard disk"]
for device in boot_devices:
  assert re.search(device, output), f"{device} not detected in boot devices"

print("All expected boot devices detected")
""",
    "run_command": "python test_boot_devices.py", 
    "expected_result": "All expected boot devices detected"
  }
},
{
  "testname": "Boot Configuration Validation Test",
  "testcases": {
    "testname": "Boot Configuration Validation Test",
    "objective": "Validate boot configuration parameters", 
    "steps": [
      "- Retrieve current boot configuration",
      "- Validate config values match expected values",
      "- If mismatch, report issue"  
    ],
    "test_data": {
      "expected_config": {
        "primary": "hard-disk", 
        "secondary": "usb"
      }
    }
  },
  "testscripts": {
    "testname": "Boot Configuration Validation Test",
    "objective": "Automate boot configuration validation",
    "file_name": "test_boot_config.py",
    "init_scripts": "pip install paramiko PyYAML",  
    "script": """  
import paramiko
import yaml

IP = "192.168.1.1"
USERNAME = "admin"
PASSWORD = "admin123"
  
ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect(IP, username=USERNAME, password=PASSWORD)
  
stdin, stdout, stderr = ssh.exec_command("show boot configuration")
output = stdout.read().decode()
config = yaml.safe_load(output)

expected_config = yaml.safe_load(f\"\"\"
primary: hard-disk  
secondary: usb
\"\"\")
  
assert config == expected_config, "Boot configuration mismatch"
  
print("Boot configuration validated successfully")
""",
    "run_command": "python test_boot_config.py",
    "expected_result": "Boot configuration validated successfully" 
  }
}
]
###ENDLIST###