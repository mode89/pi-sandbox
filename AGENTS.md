# pi-sandbox

Single-file Python script (`pi-sandbox`) that runs the `pi` agent inside a
bubblewrap sandbox.

## Usage

```
pi-sandbox [pi args...]   # run pi in the sandbox (args forwarded to pi)
pi-sandbox --bash [...]   # run bash instead of pi (env testing/debugging)
```

## Configuration

At startup, execs each config that exists in order:
- `~/.pi/agent/sandbox/config.py`
- `./.pi/sandbox/config.py`
- `./.pi/sandbox/config.local.py`

Config script can tweak sandbox behavior by overriding `pi_sandbox` functions using `@pi_sandbox.override` decorator, for example:

```python
import pi_sandbox

@pi_sandbox.override
def nix_shell_packages(orig):
    return [*orig(), "git"]
```
