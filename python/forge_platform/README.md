# forge_platform - Platform Backend Abstraction

Unified interface for MCC interaction (simulation and hardware backends).

## Purpose

Provides consistent API for:
- Setting Control Registers (CR0-CR15)
- Reading Status Registers (SR0-SR15, future)
- Capturing oscilloscope outputs
- Switching between simulation and hardware

## Backends

**SimulationBackend** (`simulation_backend.py`)
- Pure GHDL simulation
- Control Registers set directly via DUT signals
- Fast, no hardware required
- Default for component testing

**Cloud Compile Backend** (`simulators/cloud_compile.py`, future)
- Compiles to bitstream and deploys to real Moku hardware
- Network-accessible Control Registers via MCC API
- Physical oscilloscope capture
- "Train like you fight" - same code for dev and production

## Core Abstractions

**backend.py**
- `PlatformBackend` base class
- Common interface for all backends

**network_cr.py**
- Network Control Register API
- HTTP/REST interface to MCC (future)

**simulators/oscilloscope.py**
- Oscilloscope capture abstraction
- Voltage decoding (HVS decoder integration)

## Usage

```python
from forge_platform import SimulationBackend

# In CocoTB test
backend = SimulationBackend(dut)
backend.set_control_register(0, 0xE0000000)  # FORGE FULLY_ENABLED
status = backend.get_status_register(0)
```

## Platform Tests

Platform tests use these backends to validate FORGE control scheme and oscilloscope debugging.

See `cocotb_tests/platform/README.md` for platform testing patterns.
