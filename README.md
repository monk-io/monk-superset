# Apache Superset & Monk
This repository contains Monk.io template to deploy Apache Superset & Monk either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running.
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository
```bash
git clone https://github.com/monk-io/monk-superset
```

## Load Template
```bash
cd monk-superset
monk load MANIFEST
```


#### Let's take a look at the themes I have installed.
```bash
foo@bar:~$ monk list monk-superset
✔ Got the list
Type      Template                      Repository  Version  Tags
runnable  monk-superset/db               local       -         -
runnable  monk-superset/rds              local       1.000000  -
group     monk-superset/stack            local       -         -
runnable  monk-superset/superset         local       -         -
runnable  monk-superset/superset-beat    local       -         -
runnable  monk-superset/superset-init    local       -         -
runnable  monk-superset/superset-worker  local       -         -
```

## Deploy Stack
```bash
foo@bar:~$ monk run monk-superset/stack
?✔ Starting the job: local/monk-superset/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% apache/superset:latest monk-1
✔ [================================================] 100% apache/superset:latest monk-2
✔ [================================================] 100% bitnami/redis:latest monk-2
✔ [================================================] 100% postgres:latest monk-1
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Starting containers DONE
✔ Starting containers DONE
✔ Starting containers DONE
✔ Starting containers DONE
✔ Started local/monk-superset/stack

🔩 templates/local/monk-superset/stack
 ├─🧊 Peer monk-2
 │  ├─🔩 templates/local/monk-superset/superset-init
 │  │  └─📦 7cb7190b873ffa07d7da9a11b44b3d4d-et-superset-init-monk-superset
 │  │     └─🧩 apache/superset:latest
 │  ├─🔩 templates/local/monk-superset/superset-worker
 │  │  └─📦 2cc2af06f53a3ba804541e2f27396d2b--superset-worker-monk-superset
 │  │     └─🧩 apache/superset:latest
 │  └─🔩 templates/local/monk-superset/rds
 │     └─📦 f6ea507bb3781294df604c6101c1204b-cal-monk-superset-rds-monk-rds
 │        ├─🧩 bitnami/redis:latest
 │        ├─💾 /var/lib/monkd/volumes/redis/mysql -> /bitnami/redis/data
 │        └─🔌 open 16.170.240.192:6389 (0.0.0.0:6389) -> 6379
 └─🧊 Peer monk-1
    ├─🔩 templates/local/monk-superset/db
    │  └─📦 8964742a6369615abb9de865817dbc7a-ocal-monk-superset-db-postgres
    │     ├─🧩 postgres:latest
    │     └─🔌 open 13.53.134.32:5432 (0.0.0.0:5432) -> 5432
    ├─🔩 templates/local/monk-superset/superset
    │  └─📦 61e819e36129d28a0ebe10ca68b2cb4c-uperset-superset-monk-superset
    │     ├─🧩 apache/superset:latest
    │     └─🔌 open 13.53.134.32:8088 (0.0.0.0:8088) -> 8088
    └─🔩 templates/local/monk-superset/superset-beat
       └─📦 a3666e5f6b05c0d679c3c3c01009f8e3-et-superset-beat-monk-superset
          └─🧩 apache/superset:latest

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) local/monk-superset/stack - Inspect logs
	monk shell     local/monk-superset/stack - Connect to the container's shell
	monk do        local/monk-superset/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Check web gui

`http://16.170.240.192:8088/`






## Stop, remove and clean up workloads and templates

```bash
monk purge -x -a
```

