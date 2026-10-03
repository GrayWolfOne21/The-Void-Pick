# The Void Pick

A local process supervisor for a miner binary you already have.

It loads a config, starts that binary, streams stdout to a page on `127.0.0.1:8742`, reads a temperature file, and kills the process on a thermal limit or a manual halt. It does not build block templates, negotiate Stratum V2, filter pools, or route traffic. Optional flags append arguments to the miner command. Those flags are off by default. The program does not implement the protocols they name.

No miner binary is included. Point `miner.binary_path` at one you own.

## States

`INITIALIZE` → `EVALUATE` → `EXECUTE_MINER` → `MONITOR`

From `MONITOR`:

- temperature over the limit → `THERMAL_THROTTLE` (kill, wait, return to `EVALUATE`)
- operator halt → `MANUAL_HALT` until re-engage
- about every 30 seconds → `DATA_LOGGING`, then back to `MONITOR`

`VOID_DREDGE` and shadow evaluation are placeholders. Shadow evaluation sleeps and reports that no route changed. It does not pre-warm a connection.

## Run

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
# set miner.binary_path and pool.user in config/void_pick.yaml
python -m backend.server
```

Open http://127.0.0.1:8742

- SEVER UPLINK kills the process and enters `MANUAL_HALT`
- RE-ENGAGE leaves the halt and restarts at `INITIALIZE`

Mining uses electricity and makes heat. Run it only on hardware you own and are allowed to use. The kill switch and thermal stop are there so you can test them. This is as-is software.

License: AGPL-3.0. See [LICENSE](LICENSE).
